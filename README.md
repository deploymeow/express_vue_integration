# express_vue_integration

frontend : vue3
@vue/cli 로 뷰 프로젝트 설치
```
vue create myapp
```

voe-router 추가
```
yarn add vue-router
```

webpack config 파일 생성
output destination dir 을 백엔드로 설정
프록시 설정으로 express api 접근
+ add vue.config.js
```
const path = require("path")
module.exports = {
    outputDir: path.resolve(__dirname, '../backend/public/'),
    devServer: {
        proxy: {
            '/api': {
                target: 'http://localhost:3000/api',
                changeOrigin: true,
                pathRewrite: {
                    "^/api": ''
                }
            }
        }
    }
}
```

backend : express

express-generator 로 express 설치
npm 으로 pkg 설치
```
npm i -g express-generator
express --view=pug backend

cd backend
npm install
DEBUG=backend:* npm start
```

라우터가 프론트엔트에서 webpack이 만든 인덱스파일을 response로 보내도록 함
```
router.get('/', function(req, res, next) {
  res.sendFile(path.join(__dirname, '../public/index.html'))
});
```
