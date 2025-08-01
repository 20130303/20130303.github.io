
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <link rel="icon" href="/favicon.ico">
  <script>

        const domains = [
            'oj.tudoubiancheng.top',
        ];

        const retryInfo = {};

        window.addEventListener('error', function(event) {
            const tag = event.target;
            
            if (tag.tagName === 'SCRIPT' || tag.tagName === 'LINK') {
                // 排除脚本内部错误
                if (event instanceof ErrorEvent) return;
                
                const url = new URL(tag.src || tag.href);
                const path = url.pathname;
                
                if (!retryInfo[path]) {
                    retryInfo[path] = {
                        times: 0,
                        nextIndex: 0
                    };
                    addLog(`资源加载失败: ${path}，开始重试...`, 'warning');
                }
                
                const info = retryInfo[path];
                
                if (info.times < domains.length) {
                    // 阻塞式加载 - 使用document.write实现同步加载
                    const newUrl = new URL(url);
                    newUrl.host = domains[info.nextIndex];
                    
                    if (tag.tagName === 'SCRIPT') {
                        // 使用document.write阻塞后续解析
                        document.write(`<script src="${newUrl.toString()}"><\/script>`);
                        addLog(`重试JS: ${path} (${info.times+1}/3) 使用 ${domains[info.nextIndex]}`, 'info');
                    } else if (tag.tagName === 'LINK') {
                        // CSS使用阻塞式加载
                        document.write(`<link rel="stylesheet" href="${newUrl.toString()}">`);
                        addLog(`重试CSS: ${path} (${info.times+1}/3) 使用 ${domains[info.nextIndex]}`, 'info');
                    }
                    
                    // 更新重试信息
                    info.times++;
                    info.nextIndex++;
                } else {
                    addLog(`资源 ${path} 所有重试失败`, 'error');
                }
            }
        }, true);
        
        // 日志功能
        function addLog(message, type = 'info') {
          console.log(type, message)
        }
  </script>
  <link href="https://cdn.bootcdn.net/ajax/libs/element-ui/2.14.0/theme-chalk/index.min.css" rel="stylesheet">
  <link href="https://cdn.bootcdn.net/ajax/libs/github-markdown-css/4.0.0/github-markdown.min.css" rel="stylesheet">
  <link href="https://cdn.bootcdn.net/ajax/libs//KaTeX/0.12.0/katex.min.css" rel="stylesheet">
  <link href="https://cdn.bootcdn.net/ajax/libs/muse-ui/3.0.2/muse-ui.min.css" rel="stylesheet">
  <title>Hcode OnlineJudge</title>
  <script>// IE 10 and earlier
    if (window.navigator.userAgent.indexOf('MSIE ') > 0 &&
      window.confirm('Your browser is not supported, click \'OK\' to update')) {
      window.location = 'http://outdatedbrowser.com'
    }</script>
  <style>
    @-webkit-keyframes enter {
      0% {
        opacity: 0;
        top: -10px;
      }

      5% {
        opacity: 1;
        top: 0px;
      }

      50.9% {
        opacity: 1;
        top: 0px;
      }

      55.9% {
        opacity: 0;
        top: 10px;
      }
    }

    @keyframes enter {
      0% {
        opacity: 0;
        top: -10px;
      }

      5% {
        opacity: 1;
        top: 0px;
      }

      50.9% {
        opacity: 1;
        top: 0px;
      }

      55.9% {
        opacity: 0;
        top: 10px;
      }
    }

    @-moz-keyframes enter {
      0% {
        opacity: 0;
        top: -10px;
      }

      5% {
        opacity: 1;
        top: 0px;
      }

      50.9% {
        opacity: 1;
        top: 0px;
      }

      55.9% {
        opacity: 0;
        top: 10px;
      }
    }

    body {
      background: #f8f8f9;
    }

    #app-loader {
      position: absolute;
      left: 50%;
      top: 50%;
      margin-left: -27.5px;
      margin-top: -27.5px;
    }

    #app-loader .square {
      background: #2d8cf0;
      width: 15px;
      height: 15px;
      float: left;
      top: -10px;
      margin-right: 5px;
      margin-top: 5px;
      position: relative;
      opacity: 0;
      -webkit-animation: enter 6s infinite;
      animation: enter 6s infinite;
    }

    #app-loader .enter {
      top: 0px;
      opacity: 1;
    }

    #app-loader .square:nth-child(1) {
      -webkit-animation-delay: 1.8s;
      -moz-animation-delay: 1.8s;
      animation-delay: 1.8s;
    }

    #app-loader .square:nth-child(2) {
      -webkit-animation-delay: 2.1s;
      -moz-animation-delay: 2.1s;
      animation-delay: 2.1s;
    }

    #app-loader .square:nth-child(3) {
      -webkit-animation-delay: 2.4s;
      -moz-animation-delay: 2.4s;
      animation-delay: 2.4s;
      background: #ff9900;
    }

    #app-loader .square:nth-child(4) {
      -webkit-animation-delay: 0.9s;
      -moz-animation-delay: 0.9s;
      animation-delay: 0.9s;
    }

    #app-loader .square:nth-child(5) {
      -webkit-animation-delay: 1.2s;
      -moz-animation-delay: 1.2s;
      animation-delay: 1.2s;
    }

    #app-loader .square:nth-child(6) {
      -webkit-animation-delay: 1.5s;
      -moz-animation-delay: 1.5s;
      animation-delay: 1.5s;
    }

    #app-loader .square:nth-child(8) {
      -webkit-animation-delay: 0.3s;
      -moz-animation-delay: 0.3s;
      animation-delay: 0.3s;
    }

    #app-loader .square:nth-child(9) {
      -webkit-animation-delay: 0.6s;
      -moz-animation-delay: 0.6s;
      animation-delay: 0.6s;
    }

    #app-loader .clear {
      clear: both;
    }

    #app-loader .last {
      margin-right: 0;
    }

    #app-loader .loader-content {
      color: #3498db;
      font-size: 16px;
      font-weight: 600;
    }
  </style>
  <link href="/assets/css/chunk-0086f3a0.b3d43316.css" rel="prefetch">
  <link href="/assets/css/chunk-09b28fc1.26d92151.css" rel="prefetch">
  <link href="/assets/css/chunk-0a8a2980.99ad07c7.css" rel="prefetch">
  <link href="/assets/css/chunk-0b6ade82.cb46c73a.css" rel="prefetch">
  <link href="/assets/css/chunk-0bbfbd24.ec8c8358.css" rel="prefetch">
  <link href="/assets/css/chunk-0f8b7bfd.7c8a3a23.css" rel="prefetch">
  <link href="/assets/css/chunk-13a6f402.1f6fb654.css" rel="prefetch">
  <link href="/assets/css/chunk-1e276e24.e2899e10.css" rel="prefetch">
  <link href="/assets/css/chunk-2cb459fd.a21b9c93.css" rel="prefetch">
  <link href="/assets/css/chunk-34c1a4a4.ada2d265.css" rel="prefetch">
  <link href="/assets/css/chunk-369055a7.7cf1d248.css" rel="prefetch">
  <link href="/assets/css/chunk-390f0eb1.b4b66214.css" rel="prefetch">
  <link href="/assets/css/chunk-3f9747a1.93a40251.css" rel="prefetch">
  <link href="/assets/css/chunk-44cf3624.fa91b10e.css" rel="prefetch">
  <link href="/assets/css/chunk-4505762e.3776f1a6.css" rel="prefetch">
  <link href="/assets/css/chunk-59e34fe3.879dab52.css" rel="prefetch">
  <link href="/assets/css/chunk-5d4c4c68.e8780b64.css" rel="prefetch">
  <link href="/assets/css/chunk-5f8b03e6.9f909ead.css" rel="prefetch">
  <link href="/assets/css/chunk-61f421e0.eec5fec6.css" rel="prefetch">
  <link href="/assets/css/chunk-6e6ca986.2904e50e.css" rel="prefetch">
  <link href="/assets/css/chunk-9d05a348.00056d7d.css" rel="prefetch">
  <link href="/assets/css/chunk-9f8738ee.eac0a445.css" rel="prefetch">
  <link href="/assets/css/chunk-ce81f1e2.680c1d97.css" rel="prefetch">
  <link href="/assets/css/chunk-d9f11fcc.5414209e.css" rel="prefetch">
  <link href="/assets/css/chunk-ecfec440.4e86982e.css" rel="prefetch">
  <link href="/assets/css/chunk-f23c508c.bc078d4e.css" rel="prefetch">
  <link href="/assets/js/chunk-0086f3a0.19453f4e.js" rel="prefetch">
  <link href="/assets/js/chunk-09b28fc1.331f9c06.js" rel="prefetch">
  <link href="/assets/js/chunk-0a8a2980.4ec6f492.js" rel="prefetch">
  <link href="/assets/js/chunk-0b6ade82.a9e264c7.js" rel="prefetch">
  <link href="/assets/js/chunk-0bbfbd24.ce51ceb1.js" rel="prefetch">
  <link href="/assets/js/chunk-0f8b7bfd.bc1984e1.js" rel="prefetch">
  <link href="/assets/js/chunk-13a6f402.24dc9de2.js" rel="prefetch">
  <link href="/assets/js/chunk-1e276e24.14067b86.js" rel="prefetch">
  <link href="/assets/js/chunk-2cb459fd.574488f9.js" rel="prefetch">
  <link href="/assets/js/chunk-2d0afe0f.a8d03c92.js" rel="prefetch">
  <link href="/assets/js/chunk-2d0d362a.3cb728b7.js" rel="prefetch">
  <link href="/assets/js/chunk-34c1a4a4.a5ece8f2.js" rel="prefetch">
  <link href="/assets/js/chunk-369055a7.1125de80.js" rel="prefetch">
  <link href="/assets/js/chunk-390f0eb1.4b34223b.js" rel="prefetch">
  <link href="/assets/js/chunk-3f9747a1.55832072.js" rel="prefetch">
  <link href="/assets/js/chunk-44cf3624.4512917c.js" rel="prefetch">
  <link href="/assets/js/chunk-4505762e.3311cc8c.js" rel="prefetch">
  <link href="/assets/js/chunk-59e34fe3.e514b8fb.js" rel="prefetch">
  <link href="/assets/js/chunk-5d4c4c68.376d213c.js" rel="prefetch">
  <link href="/assets/js/chunk-5f8b03e6.cb10c18b.js" rel="prefetch">
  <link href="/assets/js/chunk-61f421e0.97dbf224.js" rel="prefetch">
  <link href="/assets/js/chunk-6e6ca986.a426ca06.js" rel="prefetch">
  <link href="/assets/js/chunk-74597c67.54e454b8.js" rel="prefetch">
  <link href="/assets/js/chunk-9d05a348.b3d9fd13.js" rel="prefetch">
  <link href="/assets/js/chunk-9f8738ee.e60a6bd6.js" rel="prefetch">
  <link href="/assets/js/chunk-ce81f1e2.486b2891.js" rel="prefetch">
  <link href="/assets/js/chunk-d9f11fcc.f472d83c.js" rel="prefetch">
  <link href="/assets/js/chunk-ecfec440.e54353fe.js" rel="prefetch">
  <link href="/assets/js/chunk-f23c508c.b720a617.js" rel="prefetch">
  <link href="/assets/css/app.cee4614b.css" rel="preload" as="style">
  <link href="/assets/css/chunk-vendors.c9fb66ba.css" rel="preload" as="style">
  <link href="/assets/js/app.4e3a6fe7.js" rel="preload" as="script">
  <link href="/assets/js/chunk-vendors.4a231350.js" rel="preload" as="script">
  <link href="/assets/css/chunk-vendors.c9fb66ba.css" rel="stylesheet">
  <link href="/assets/css/app.cee4614b.css" rel="stylesheet">
</head>

<body><noscript><strong>We're sorry but hoj-vue doesn't work properly without JavaScript enabled. Please enable it to
      continue.</strong></noscript>
  <div id="app"></div>
  <div id="app-loader">
    <div class="square"></div>
    <div class="square"></div>
    <div class="square last"></div>
    <div class="square clear"></div>
    <div class="square"></div>
    <div class="square last"></div>
    <div class="square clear"></div>
    <div class="square"></div>
    <div class="square last"></div>
    <div class="loader-content"><span>Loading...</span></div>
  </div>
  <script src="https://cdn.bootcdn.net/ajax/libs//vue/2.6.11/vue.min.js"></script>
  <script src="https://cdn.bootcdn.net/ajax/libs//vue-router/3.2.0/vue-router.min.js"></script>
  <script src="https://cdn.bootcdn.net/ajax/libs//axios/0.26.0/axios.min.js"></script>
  <script src="https://cdn.bootcdn.net/ajax/libs//element-ui/2.15.3/index.min.js"></script>
  <script src="https://cdn.bootcdn.net/ajax/libs//highlight.js/10.3.2/highlight.min.js"></script>
  <script src="https://cdn.bootcdn.net/ajax/libs//moment.js/2.29.1/moment.min.js"></script>
  <script src="https://cdn.bootcdn.net/ajax/libs//moment.js/2.29.1/locale/zh-cn.min.js"></script>
  <script src="https://cdn.bootcdn.net/ajax/libs//moment.js/2.29.1/locale/en-gb.min.js"></script>
  <script src="https://cdn.bootcdn.net/ajax/libs//echarts/4.9.0-rc.1/echarts.min.js"></script>
  <script src="https://cdn.bootcdn.net/ajax/libs//vue-echarts/5.0.0-beta.0/vue-echarts.min.js"></script>
  <script src="https://cdn.bootcdn.net/ajax/libs//vuex/3.5.1/vuex.min.js"></script>
  <script src="https://cdn.bootcdn.net/ajax/libs//KaTeX/0.12.0/katex.min.js"></script>
  <script src="https://cdn.bootcdn.net/ajax/libs//KaTeX/0.12.0/contrib/auto-render.min.js"></script>
  <script src="https://cdn.bootcdn.net/ajax/libs//muse-ui/3.0.2/muse-ui.min.js"></script>
  <script src="https://cdn.bootcdn.net/ajax/libs//jquery/3.5.1/jquery.min.js"></script>
  <script src="/assets/js/chunk-vendors.4a231350.js"></script>
  <script src="/assets/js/app.4e3a6fe7.js"></script>
</body>

</html>
