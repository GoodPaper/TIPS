# find 사용법

#### Terminal에 검색한 파일 결과 이름만 나오게 하고 싶다.
```bash
# https://stackoverflow.com/questions/9202495/have-find-print-just-the-filenames-not-full-paths
# %f     File's name with any leading directories removed (only the last element).
$ find ... -printf "%f\n"
```
