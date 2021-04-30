# File browsing 전용 페이지 만들기

#### Purpose, 목적
S3에 있는 데이터를 폴더 구조로 확인할 수 있는 웹 페이지를 간단하게 만든다. Public 용도로 사용한다고 가정하고 작업한다. 아래 주소를 참조했다.
  * https://github.com/rufuspollock/s3-bucket-listing

```html
<!DOCTYPE html>
<html>
<head>  
  <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>  
</head>
<body>

  <div id="listing"></div>

  <script type="text/javascript">
    var S3BL_IGNORE_PATH = true;  
    var BUCKET_URL = '버킷 URL';
    var EXCLUDE_FILE = '메인 파일';
  </script>
  <script type="text/javascript">

      if (typeof AUTO_TITLE != 'undefined' && AUTO_TITLE == true) {
        document.title = location.hostname;
      }

      if (typeof S3_REGION != 'undefined') {
        var BUCKET_URL = 'http://' + location.hostname + '.' + S3_REGION + '.amazonaws.com';
        var BUCKET_WEBSITE_URL = location.protocol + '//' + location.hostname;
      }

      if (typeof S3BL_IGNORE_PATH == 'undefined' || S3BL_IGNORE_PATH != true) {
        var S3BL_IGNORE_PATH = false;
      }

      if (typeof BUCKET_URL == 'undefined') {
        var BUCKET_URL = location.protocol + '//' + location.hostname;
      }

      if (typeof BUCKET_NAME != 'undefined') {
        if (!~BUCKET_URL.indexOf(location.protocol + '//' + BUCKET_NAME)) {
          BUCKET_URL += '/' + BUCKET_NAME;
        }
      }

      if (typeof BUCKET_WEBSITE_URL == 'undefined') {
        var BUCKET_WEBSITE_URL = BUCKET_URL;
      }

      if (typeof S3B_ROOT_DIR == 'undefined') {
        var S3B_ROOT_DIR = '';
      }

      if (typeof S3B_SORT == 'undefined') {
        var S3B_SORT = 'DEFAULT';
      }

      if (typeof EXCLUDE_FILE == 'undefined') {
        var EXCLUDE_FILE = [];
      } else if (typeof EXCLUDE_FILE == 'string') {
        var EXCLUDE_FILE = [EXCLUDE_FILE];
      }

      if (!Array.prototype.includes) {
        Object.defineProperty(Array.prototype, 'includes', {
          value: function(searchElement, fromIndex) {

            if (this == null) {
              throw new TypeError('"this" is null or not defined');
            }            
            var o = Object(this);
            var len = o.length >>> 0;
            if (len === 0) { return false; }
            var n = fromIndex | 0;
            var k = Math.max(n >= 0 ? n : len - Math.abs(n), 0);

            function sameValueZero(x, y) {
              return x === y || (typeof x === 'number' && typeof y === 'number' && isNaN(x) && isNaN(y));
            }

            while (k < len) {
              if (sameValueZero(o[k], searchElement)) {
                return true;
              }
              k++;
            }

            return false;
          }
        });
      }

      jQuery(function($) { getS3Data(); });

      function sortFunction(a, b) {
        switch (S3B_SORT) {
          case "OLD2NEW":
            return a.LastModified > b.LastModified ? 1 : -1;
          case "NEW2OLD":
            return a.LastModified < b.LastModified ? 1 : -1;
          case "A2Z":
            return a.Key < b.Key ? 1 : -1;
          case "Z2A":
            return a.Key > b.Key ? 1 : -1;
          case "BIG2SMALL":
            return a.Size < b.Size ? 1 : -1;
          case "SMALL2BIG":
            return a.Size > b.Size ? 1 : -1;
        }
      }

      function getS3Data(marker, html) {

        var s3_rest_url = createS3QueryUrl(marker);
        $('#listing')
            .html('<img src="//assets.okfn.org/images/icons/ajaxload-circle.gif" />');
        $.get(s3_rest_url)
            .done(function(data) {
              $('#listing').html('');
              var xml = $(data);
              var info = getInfoFromS3Data(xml);
              if (S3B_SORT != 'DEFAULT') {
                var sortedFiles = info.files;
                sortedFiles.sort(sortFunction);
                info.files = sortedFiles;
              }

              buildNavigation(info);

              html = typeof html !== 'undefined' ? html + prepareTable(info) : prepareTable(info);
              if (info.nextMarker != "null") {
                getS3Data(info.nextMarker, html);
              } else {
                document.getElementById('listing').innerHTML =
                    '<pre>' + html + '</pre>';
              }
            }
          )
          .fail(function(error) {
            console.error(error);
            $('#listing').html('<strong>Error: ' + error + '</strong>');
          });
      }

      function buildNavigation(info) {
        var root = '<a href="?prefix=">' + BUCKET_WEBSITE_URL + '</a> / ';
        if (info.prefix) {
          var processedPathSegments = '';
          var content = $.map(info.prefix.split('/'), function(pathSegment) {
            processedPathSegments =
                processedPathSegments + encodeURIComponent(pathSegment) + '/';
            return '<a href="?prefix=' + processedPathSegments + '">' + pathSegment +
                   '</a>';
          });
          $('#navigation').html(root + content.join(' / '));
        } else {
          $('#navigation').html(root);
        }
      }

      function createS3QueryUrl(marker) {
        var s3_rest_url = BUCKET_URL;
        s3_rest_url += '?delimiter=/';
        var rx = '.*[?&]prefix=' + S3B_ROOT_DIR + '([^&]+)(&.*)?$';
        var prefix = '';
        if (S3BL_IGNORE_PATH == false) {
          var prefix = location.pathname.replace(/^\//, S3B_ROOT_DIR);
        }
        var match = location.search.match(rx);
        if (match) {
          prefix = S3B_ROOT_DIR + match[1];
        } else {
          if (S3BL_IGNORE_PATH) {
            var prefix = S3B_ROOT_DIR;
          }
        }
        if (prefix) {
          var prefix = prefix.replace(/\/$/, '') + '/';
          s3_rest_url += '&prefix=' + prefix;
        }
        if (marker) {
          s3_rest_url += '&marker=' + marker;
        }
        return s3_rest_url;
      }

      function getInfoFromS3Data(xml) {
        var files = $.map(xml.find('Contents'), function(item) {
          item = $(item);
          return {
            Key: item.find('Key').text(),
                LastModified: item.find('LastModified').text(),
                Size: bytesToHumanReadable(item.find('Size').text()),
                Type: 'file'
          }
        });
        var directories = $.map(xml.find('CommonPrefixes'), function(item) {
          item = $(item);
          return {
            Key: item.find('Prefix').text(),
              LastModified: '',
              Size: '0',
              Type: 'directory'
          }
        });
        if ($(xml.find('IsTruncated')[0]).text() == 'true') {
          var nextMarker = $(xml.find('NextMarker')[0]).text();
        } else {
          var nextMarker = null;
        }
        return {
          files: files,
          directories: directories,
          prefix: $(xml.find('Prefix')[0]).text(),
          nextMarker: encodeURIComponent(nextMarker)
        }
      }

      function prepareTable(info) {
        var files = info.directories.concat(info.files), prefix = info.prefix;
        var cols = [45, 30, 15];
        var content = [];
        content.push(padRight('Last Modified', cols[1]) + '  ' +
                     padRight('Size', cols[2]) + 'Key \n');
        content.push(new Array(cols[0] + cols[1] + cols[2] + 4).join('-') + '\n');

        if (prefix && prefix !== S3B_ROOT_DIR) {
          var up = prefix.replace(/\/$/, '').split('/').slice(0, -1).concat('').join(
                  '/'),  // one directory up
              item =
                  {
                    Key: up,
                    LastModified: '',
                    Size: '',
                    keyText: '../',
                    href: S3BL_IGNORE_PATH ? '?prefix=' + up : '../'
                  },
              row = renderRow(item, cols);
          content.push(row + '\n');
        }

        jQuery.each(files, function(idx, item) {
          item.keyText = item.Key.substring(prefix.length);
          if (item.Type === 'directory') {
            if (S3BL_IGNORE_PATH) {
              item.href = location.protocol + '//' + location.hostname +
                          location.pathname + '?prefix=' + item.Key;
            } else {
              item.href = item.keyText;
            }
          } else {
            item.href = BUCKET_WEBSITE_URL + '/' + encodeURIComponent(item.Key);
            item.href = item.href.replace(/%2F/g, '/');
          }
          var row = renderRow(item, cols);
          if (!EXCLUDE_FILE.includes(item.Key))
            content.push(row + '\n');
        });

        return content.join('');
      }

      function renderRow(item, cols) {
        var row = '';
        row += padRight(item.LastModified, cols[1]) + '  ';
        row += padRight(item.Size, cols[2]);
        row += '<a href="' + item.href + '">' + item.keyText + '</a>';
        return row;
      }

      function padRight(padString, length) {
        var str = padString.slice(0, length - 3);
        if (padString.length > str.length) {
          str += '...';
        }
        while (str.length < length) {
          str = str + ' ';
        }
        return str;
      }

      function bytesToHumanReadable(sizeInBytes) {
        var i = -1;
        var units = [' kB', ' MB', ' GB'];
        do {
          sizeInBytes = sizeInBytes / 1024;
          i++;
        } while (sizeInBytes > 1024);
        return Math.max(sizeInBytes, 0.1).toFixed(1) + units[i];
      }
    </script>
</body>
</html>
```
