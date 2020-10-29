### vue 中英文切换  
* 安装 vue-i18n依赖：  
  > npm install vue-i18n --save-dev  
* 创建zh.js和en.js文字包  
  在src/components下新建文件夹language，并在文件夹language下新建zh.js及en.js  
  ```
    //src/components/language/zh.js
      module.exports = {
          text: {
             name: '英文'
          }
      }

      //src/components/language/en.js
      module.exports = {
          text: {
              name: '中文'
          }
      }
  ```

* 挂载（main.js）
  ```
    //导入vue-i18n 并挂载到vue上
    import VueI18n from 'vue-i18n'

    Vue.use(VueI18n)
    const i18n = new VueI18n({
      locale:localStorage.getItem('languageSet')||'zh',   //从localStorage里获取用户中英文选择，没有则默认中文
      messages:{
        'zh':require('./components/language/zh'),
        'en':require('./components/language/en')
      }
    })
    new Vue({
      el: '#app',
      router,
      store,
      i18n,  //挂载到vue实例上
      template: '<App/>',
      components: { App }
    })
  ```

* 切换语言
  ```
    //在需要切换处增加按钮
    //html中使用文字
    {{$t('user.login')}}
    //点击按钮事件
    changeLanguage() {
      if(this.$i18n.locale == 'zh'){
        this.$i18n.locale='en';
      }else{
        this.$i18n.locale='zh';
      }
    },
  ```
