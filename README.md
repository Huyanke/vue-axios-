# vue-axios-跨域解决方案

1、使用node.js在本地做个代理，下载axios-axios,vue.use调用
import axios from 'axios'
import VueAxios from 'vue-axios'
Vue.use(VueAxios, axios)
2、设置代理
打开config/index.js
修改proxyTable: {}部分
修改为

proxyTable: {
      '/api': {
             target: 'https://api.douban.com/v2',
             changeOrigin: true,
             pathRewrite: {
             '^/api': ''
           }
       }
第一行的'/api'指的是虚拟路径
target指的是目标地址，也就是实际api的地址
pathRewrite规则重写
3、然后在代码页面修改一下请求地址  

    
    let _this = this
     //_this.axios.post('/api//book/1220562',{headers:{'TransactionID':'123','XClientIP':'122'}}).then(res => {
     //如果需要加请求头 同上
     
     
     _this.axios.get('/api//book/1220562').then(res => {
         console.log(res.data)
       }).catch(err => {
         console.log(err)
       })

/api/book/1220562上面的这个地址其实就等于https://api.douban.com/v2 +/api/book/1220562

4、修改完，需要重启下服务
