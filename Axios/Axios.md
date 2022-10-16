# 为什么要用Axios发送网络请求?
- axios: ajax i/o system
- 原生需要自己封装拦截功能等
- 适配浏览器和Node，JS->浏览器/Node
- fetch -> http
# axios请求方式
支持多种请求方式:
 - axios(config)
 - axios.request(config) 
 - axios.get(url[, config]) 
 - axios.delete(url[, config]) 
 - axios.head(url[, config]) 
 - axios.post(url[, data[, config]]) 
 - axios.put(url[, data[, config]]) 
 - axios.patch(url[, data[, config]])
同时发送多个请求:
 - axios.all([])
# 常见的配置选项
- 请求地址
 url: '/user',
- 请求类型
 method: 'get',
- 请根路径
 baseURL: 'http://www.mt.com/api',
- 请求前的数据处理
 transformRequest:[function(data){}],
- 请求后的数据处理
 transformResponse: [function(data){}],
- 自定义的请求头
 headers:{'x-Requested-With':'XMLHttpRequest'},
- URL查询对象
 params:{ id: 12 }
 - 查询对象序列化函数
 paramsSerializer: function(params){ }
 request body
 data: { key: 'aa'},
- 超时设置
 timeout: 1000,
 ```js
axios.request({
  url: "url",
  method: "get"
}).then(res => {
  console.log("res:", res.data)
})
 ```
 ```js
axios.post("http://123.207.32.32:1888/02_param/postjson", {
  data: {
    name: "YQ",
    password: 123456
  }
}).then(res => {
  console.log("res", res.data)
})
 ```
# axios的创建实例
```js
// 1.baseURL
const baseURL = "http://yongqi.ml"
// 给axios实例配置公共的基础配置
axios.defaults.baseURL = baseURL
axios.defaults.timeout = 10000
axios.defaults.headers = {}
axios.all([
  axios.get("/home/multidata"),
  axios.get("http://123.207.3/lyric?id=500665346")
]).then(res => {
  console.log("res:", res)
})
```
# 请求和响应拦截器
```js
// 对实例配置拦截器
axios.interceptors.request.use((config) => {
  console.log("请求成功的拦截")
  // 1.开始loading的动画

  // 2.对原来的配置进行一些修改
  // 2.1. header
  // 2.2. 认证登录: token/cookie
  // 2.3. 请求参数进行某些转化
  return config
}, (err) => {
  console.log("请求失败的拦截")
  return err
} 
})
```
# axios请求库封装
service/index.js
```js
import axios from 'axios'

class URLRequest {
    constructor(baseURL, timeout=10000){
        this.instance = axios.create({
            baseURL,
            timeout
        })
    }
    request(config){
        return new Promise((resolve,reject)=>{
            this.instance.request(config).then(res=>{
                resolve(res.data)
            }).catch(err => {
                reject(err)
            })
        })
    }
    get(config) {
        return this.request({ ...config, method: "get" })
    }

    post(config) {
        return this.request({ ...config, method: "post" })
    }
}

export default new URLRequest("http://123.207.32.32:9001")

```
使用URLRequest: main.js
```js
import URLRequest from './service'
URLRequest.request({
    url: "/lyric?id=500665346"
}).then(res => {
  console.log("res:", res)
})
URLRequest.get({
  url: "/lyric",
  params: {
    id: 500665346
  }
}).then(res => {
  console.log("res:", res)
})
```