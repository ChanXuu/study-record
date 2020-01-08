```javascript
import axios from 'axios'
import qs from 'qs';  //使用qs来格式化请求参数

//axios.defaults.timeout = 10; //超时时间
//axios.defaults.retry = 3; //请求次数
//axios.defaults.retryDelay = 20; //请求间隙

axios.defaults.baseURL = 'http://192.168.20.230:8010/api/v1'
// console.log(axios.defaults.baseURL);
axios.defaults.timeout = 10000;


//http请求拦截器
axios.interceptors.request.use((config) => {
    // console.log(config.headers.Authorization)
    //在这里判断是否又token
    // if (token) { 
    //     config.headers.Authorization = token
    // }
    
    //判断post请求
    if (config.method === 'post') {
        //config.data = qs.stringify(config.data);//格式化,将参数变成 a=1&b=2格式
    }

    //判断get请求
    if (config.method === 'get') {
        config.data = qs.stringify(config.data);
        console.log(config)
    }
    return config; //把config return出去,不然报错
}, (error) => {
    return Promise.reject(error);
});

//http响应拦截器
axios.interceptors.response.use((res) => {
    console.log(res.data)
    return res.data //返回请求到的数据
},error =>{
    //在这里判断状态码
    console.log('请求失败')
    return Promise.reject(error.response.data) //返回错误信息
})


export default axios
```

