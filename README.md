# login-demo

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

# dev install dependencies
cnpm install axios --save
cnpm install element-ui --save (npm i element-ui -S)
cnpm install sass-loader node-sass --save-dev (npm i sass-loader node-sass -D)




# main.js

import ElementUI from 'element-ui'
import axios from 'axios'
import 'element-ui/lib/theme-chalk/index.css'
import 'font-awesome/css/font-awesome.min.css'


Vue.use(ElementUI)
Vue.prototype.axios = axios
axios.defaults.withCredentials=true
Vue.config.productionTip = false

new Vue({
  el: '#app',
  router,
  render: h => h(App)
})


# dev-tools

git clone -b master https://github.com/vuejs/vue-devtools.git

cnpm install

# 注意浏览器console不输出时查看是否有filter


For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
