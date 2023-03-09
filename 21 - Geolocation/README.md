# Geolocation

## 挑战任务
本次的挑战任务，是利用浏览器内置Web Geolocation API,将获取到的地理位置及相关坐标，与index-start.html中的可视化指南针连接在一起。

## 相关知识
1. 有关地理位置接口Geolocation的说明，可查看MDN中的相关解释。
https://developer.mozilla.org/zh-CN/docs/Web/API/Geolocation
2. getCurrentPosition()方法和watchPosition()方法 getCurrentPosition()方法在调用时返回一次相关信息，watchPosition()方法调用后将持续返回相关信息，两个方法调用时除了传入相关的回调函数外，还需要传入options配置对象作为第三参数，options相关键值如下：
enableHighAccuracy参数表示是否高精度可用，为Boolean类型，默认为false，如果开启，响应时间会变慢，同时，在手机设备上会用掉更多的流量。
timeout参数表示等待响应的最大时间，默认是0毫秒，表示无穷时间。
maximumAge表示应用程序的缓存时间。单位毫秒，默认是0，意味着每次请求都是立即去获取一个全新的对象内容。