
Web组件
```
forward 前进页面
backward 后退

confirm 弹框

this.webController.refresh() 是刷新页面，会调用onPageBegin  onProgressChange onPageEnd

使用：加载本地html
    webController: WebviewController = new webview.WebviewController();

     Web({
        src: $rawfile('privacy.html'),
        controller: this.webController
      })
      
     
        .onLoadIntercept((event) => {//类似android WebView shouldOverrideUrlLoading
          if (event) {
            let url: string = event.data.getRequestUrl();
            if (url.indexOf('native://') === 0) {
              // 跳转其他界面
              router.pushUrl({ url:url.substring(9) })
              return true; 
            }
          }
          return false; //这个返回false 走onInterceptReqeust 回调，返回true则直接拦截url请求
        })
       
        
```