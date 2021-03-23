# NVIDIA CUDA + UBUNTU 18

#### 목적
UBUNTU Linux에서 NVIDIA + CUDA 환경 설정 방법에 대해 기술한다.

#### 사전 정보
모든 Device는 그에 맞는 Driver를 설치해 주어야 정상적으로 사용할 수 있다. Nvidia Graphic card도 마찬가지 이다. 동일한 모델의 그래픽 카드라 해도 플랫폼, CPU 아케텍쳐 등으로 드라이버는 전부 달라질 수 있다. 그래서 우리가 어떤 Spec의 Server, OS에서 작업할 지 먼저 결정해야 한다.

AWS EC2에는 여러가지 Spec의 인스턴스들이 있는데, 우리가 사용하고자 하는 인스턴스는 GPU 관련 인스턴스이다. 이 글을 작성하는 2020년 하반기 기준 AWS EC2에서 제공하는 GPU 관련 인스턴스의 종류는 P2, P3, P4, G3, G4 총 5개이다.

우선 여기서는 P2 Instance 기반에서 **Nvidia Tesla K80**에 맞는 환경을 설정하는 것을 설명한다.

#### 진행 과정
AWS EC2 P2.XLARGE Instance + Ubuntu 18.04 + Tesla K80 에 맞는 CUDA 10.1 버전을 설치한다. 또 그에 맞는 ML, DL 관련 Python package를 설치한다. 이 글을 작성하는 현재 CUDA의 Version은 11.X 이지만, 프로그램 및 Python package의 호환성 문제로 인해서 CUDA 10.1을 사용한다.
##### 1. 사전 확인
Nvidia HW를 비롯해서 몇 가지 정보를 확인한다.
```bash
$ lspci | grep -i nvidia
 - 00:1e.0 3D controller: NVIDIA Corporation GK210GL [Tesla K80] (rev a1) # NVIDIA Device 붙어 있는지 확인.

$ uname -m && cat /etc/*release
 - x86_64 ... # X86 Architecture 확인

$ gcc --version
 - 7.5.0 ... # GCC version 확인
```
##### 2. CUDA 설치 전 준비
```bash
$ sudo apt-get update
$ sudo apt-get -y upgrade # 이 2 명령어는 의례적으로 한다고 생각하면 된다.

# 이후에 설치될 Cuda 및 Python package 설치에 필요한 패키지들이니 설치 해 둘 것.
$ sudo apt-get install -y build-essential dkms freeglut3 freeglut3-dev libxi-dev libxmu-dev libcurl4-openssl-dev libffi-dev libssl-dev python3-dev python3-pip python3-setuptools
```
##### 3. CUDA 설치
아래 경로로 가서 cuda 10.1 deb package 설치 파일을 다운로드한다.
* https://developer.nvidia.com/cuda-10.1-download-archive-base?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=deblocal

가져와서 아래 과정으로 설치를 진행한다.
```bash
$ sudo dpkg -i cuda-repo-ubuntu1804-10-1-local-10.1.105-418.39_1.0-1_amd64.deb
$ sudo apt-key add /var/cuda-repo-10-1-local-10.1.105-418.39/7fa2af80.pub
$ sudo apt-get update
$ sudo apt-get install cuda-10-1 # 버전을 명시해서 설치하는 것이 좀 더 안전하게 생각됨.
```
아마 무난하게 설치가 완료될 것이다. /usr/local에 가서 cuda-10.1 디렉토리에 설치가 잘 되었는지 확인해 본다.
```bash
$ cd /usr/local/cuda-10.1/bin
$ sudo ./nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2019 NVIDIA Corporation
Built on Fri_Feb__8_19:08:17_PST_2019
Cuda compilation tools, release 10.1, V10.1.105
```
**아마 다른 Reference에서는 nvidia-smi로 설치가 잘 되었는지 확인할 것이다. 틀린 것은 아닌데, 설치된 cuda version을 잘 못 보여주는 경우가 있다. 정확한 것은 nvcc 이니 참고할 것. ( 아래 보면 11.0이라고 나와 있는데, 실제로 설치된 것은 10.1이다. )**
```bash
$ sudo nvidia-smi
Tue Oct 27 06:02:13 2020       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 450.80.02    Driver Version: 450.80.02    CUDA Version: 11.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Tesla K80           Off  | 00000000:00:1E.0 Off |                    0 |
| N/A   50C    P0    62W / 149W |      0MiB / 11441MiB |     81%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```
##### 4. PATH 설정
아래 두 line을 ~/.bashrc에 추가하고, 저장한다음, source ~/.bashrc를 실행하여, PATH 설정을 적용해 준다.
```bash
$ vi ~/.bashrc

...
export PATH=$PATH:/usr/local/cuda-10.1/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-10.1/lib64
...

$ source ~/.bashrc
```
##### 5. pytorch 설치
cuda 10.1에 맞는torch를 설치해야 한다. 설치 후에는 GPU가 정상적으로 사용가능한지 확인한다.
```bash
# torch 설치
$ sudo pip3 install torch==1.5.1+cu101 torchvision==0.6.1+cu101 -f https://download.pytorch.org/whl/torch_stable.html

$ python3
>> import torch
>> torch.cuda.device_count()    # 1
>> torch.cuda.get_device_name(0)    # Tesla K80
>> torch.cuda.is_available()    # True
```
##### 6. tensorflow 설치
cuda 10.1에 맞는 tensorflow를 설치해야 한다. 설치 후 GPU 정상 사용 가능 여부 확인한다.
```bash
$ sudo pip3 install --upgrade pip
$ sudo pip3 install tensorflow==2.3.0

$ python3
>> import tensorflow as tf
>> tf.test.is_gpu_available( cuda_only = False, min_cuda_compute_capability = None )    # True? 1?
```
그런데 위와 같이 Interpreter에서 cuda 연결을 확인할 때 error가 날 것이다. tensorflow는 cuda 뿐만 아니라 CUDNN까지 같이 사용하기 때문에, cudnn so 파일을 못 찾는다고 에러가 날 것이다. 다음 단계로 CUDNN을 설치한다.
##### 7. CUDNN 설치
cudnn 설치에 필요한 파일은 NVIDIA Developer community에 로그인 해서 받아야 한다. 회원 가입해서 필요한 버전의 cudnn 설치 파일을 받는다. 파일은 runtime, development package 둘 다 받는다.
* https://developer.nvidia.com/rdp/form/cudnn-download-survey

아래 명령으로 설치한다.
```bash
$ sudo dpkg -i libcudnn7_7.6.5.32-1+cuda10.1_amd64.deb
$ sudo dpkg -i libcudnn7-dev_7.6.5.32-1+cuda10.1_amd64.deb
```
##### 8. GPU 최적화
AWS에서 Instance 마다 GPU 최적화를 하는 방법을 알려주는데, 이걸 설정해놔야 GPU를 잘 사용할 수 있다.
* https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/WindowsGuide/optimize_gpu.html
```bash
$ sudo ./nvidia-smi --auto-boost-default=0    # 모든 GPU의 자동 부스트 기능을 비활성화
$ sudo ./nvidia-smi -ac "2505,875"            # 모든 GPU 클록 속도를 최대 주파수로 설정
```
설정 후에 nvidia-smi 를 실행하면 이전과는 달리 Nvidia driver의 설정이 뭔가 activate 된 것과 같이 나옴. 03 단계의 nvidia-smi 출력 결과는 이미 이 설정까지 완료된 이후의 출력
##### 9. AI-BENCHMARK 설치 및 Test
GPU HW 별 성능 비교를 할 수 있는 python package가 있는데 ai-benchmark 이다. 이를 설치해서 test를 진행해 본다.
```bash
$ sudo pip3 install ai-benchmark
$ python3
>> from ai_benchmark import AIBenchmark
>> rest = AIBenchmark().run()
...
Device Inference Score: 3096
Device Training Score: 3549
Device AI Score: 6645
...
>>
```
여기서 제시한 Spec으로 설치가 잘 되었다면, run 함수가 실행되는 시간은 대략 16분 정도 소요된다. AI Score는 6645 부근으로 나오면 모든 설치가 정상적으로 된 것이다.

#### Reference
* AWS의 GPU Instance
  * https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/install-nvidia-driver.html#nvidia-driver-instance-type
* CUDA 설치 가이드
  * https://teddylee777.github.io/linux/CUDA-이전버전-삭제후-재설치하기
  * https://coding-groot.tistory.com/87
  * https://github.com/tensorflow/tensorflow/issues/20271#issuecomment-622990424
* Tensorflow version 별 정보
  * https://www.tensorflow.org/install/source#tested_build_configurations
* GPU 사용성 Check
  * https://unix.stackexchange.com/questions/16407/how-to-check-which-gpu-is-active-in-linux
  * https://teddylee777.github.io/tensorflow/딥러닝-framework-GPU사용체크-API
* AI-Benchmark
  * http://ai-benchmark.com/alpha
  * https://pypi.org/project/ai-benchmark/
