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
cnpm install axios --save<br>
cnpm install element-ui --save (npm i element-ui -S)<br>
cnpm install sass-loader node-sass --save-dev (npm i sass-loader node-sass -D)<br>




# main.js

import ElementUI from 'element-ui'<br>
import axios from 'axios'<br>
import 'element-ui/lib/theme-chalk/index.css'<br>
import 'font-awesome/css/font-awesome.min.css'<br>


Vue.use(ElementUI)<br>
Vue.prototype.axios = axios<br>
axios.defaults.withCredentials=true<br>
Vue.config.productionTip = false<br>

new Vue({<br>
  el: '#app',<br>
  router,<br>
  render: h => h(App)<br>
})<br>


# dev-tools

git clone -b master https://github.com/vuejs/vue-devtools.git<br>

cnpm install<br>

# 注意浏览器console不输出时查看是否有filter


For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
