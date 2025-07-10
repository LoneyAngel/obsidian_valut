重新开坑

**如有问题，重新启动**
# 和后端交互
- 使用axios进行http交互
- 后端用过body进行接受，因为这里并没有采取拼接字符串的方法

- 前端请求
```js
async function sendRequest() {
    try {
        console.log(phone.value)
        let temp = {
            phone: phone.value
        }
        const response = await axios.post('http://localhost:3000/user/yan', temp);
        console.log('服务器响应:', response.data);
    } catch (error) {
        console.error('发送失败:', error.response ? error.response.data : error.message);
    }
}
```
- 后端接受
```js
router.post("/yan", async (req, res) => {
  try {
    const number = req.body.phone;//通过body获取
    console.log(number);
    const yan_number = await sendSmsMessage(number);
    if (yan_number) {
      console.log(yan_number);
      res.json({ yan_number });
    } else {
      res.status(500).json({ message: "验证码发送失败" });
    }
  } catch (err) {
    res.status(500).json({ message: "验证码发送失败" });
  }
});
```



## 文件交互存储解决方案
- 前端接受文件
```js
<input type="file" multiple accept=".jpg,.STL,.zip" @change="handleFileUpload" />
```
- 添加文件到变量
```js
const handleFileUpload = (event) => {
    const selectedFiles = event.target.files;
    for (let i = 0; i < selectedFiles.length; i++) {
        files.value.push(selectedFiles[i]);
    }
};
```
- 移除文件
```js
const removeFile = (fileToRemove) => {

    files.value = files.value.filter(file => file !== fileToRemove);

};
```
- 提交文件到后端
```js
const handleSubmit = async () => {
    if (files.value.length === 0) {
        alert('请选择至少一个文件！');
        return;
    }
    const formData = new FormData();
    files.value.forEach(file => formData.append('files', file));
    try {
        const response = await axios.post('http://localhost:3000/resource/upload', formData, {
            headers: { 'Content-Type': 'multipart/form-data' }
        });
        if (response.data.success) {
            alert('文件上传成功！');
        }

    } catch (error) {
        console.error('文件上传失败:', error);
        alert('文件上传失败，请重试！');
    }

};
```




# 高级组件
//建议提前规划好空间
## css部分
### 参考
- 参考一些网站
- 特殊的居中样式
	- aligin-items:center
	- justify-content:center

## padding,margin
padding：内边距（框）
margin:外边距


### flex
- 方便的布局方式
- flex-content
- flex-items
- flex-flow
- gap

### 动效


### 图片
```js
<img>
css部分的img选项
```
大小调整，max-width，height:auto，保持宽高比的动态调整大小

### z-index
- 越大层次越高，就像ps的图层一样，形成遮罩



### 位置“微调”
- transition，或者padding,margin


### 图标
- svg
- 其他图片
- 图标库

### 去除默认的html样式
默认的html格式一般会影响我们的调试
建议直接去除


### 字体
#### 样式
下载字体到本地进行使用
font-size
font-weight

#### 间距
word_spacing
letter_spacing

## js部分
### 响应式数据
ref
const data=ref('')
### prop
可以在使用子组件的时候向其传递参数，实现组件的复用
```js
<script setup>
const props = defineProps({
    ni: {
        type: String,
        default: "login" // 默认值
    }
});
<template>
    <button><text>{{ ni }}</text></button>//父组件传递的参数会直接传递到这里
</template>

//父组件
<loginbutton ni="验证码" @click="sendRequest"
                        style="margin-top: 15px;transform:  translateX(160px);width: 65px;padding:2px;" />
```


### vue指令
- v-model实现双向的数据绑定
- v-bind实现响应式的显示数据
- v-on进行事件的绑定



### 实现跳转
```js
const handleClick = () => {
    console.log(router.getRoutes().map(route => route.path)); // 展示所有路径
    router.back()//实现回退
}
```


# 实现页面跳转的方法：router
## 前端路由示例
```js
import { createMemoryHistory, createRouter } from "vue-router";
import home from "@/components/HomeVue.vue";
import file from "@/components/FiledealVue.vue";
import verify from "@/components/VerifyVue.vue";
const routes = [
  {
    path: "/",
    redirect: "/home",
    children{
	    ...
    }
  },
  {
    path: "/home",
    component: home,
    name: "home",
  },
  {
    path: "/file",
    component: file,
    name: "file",
  },
  {
    path: "/verify",
    component: verify,
    name: "verify",
  },
];
const router = createRouter({
  history: createMemoryHistory()
  routes,
});
export default router;
```
## 后端路由示例
```js
const test = require("./modules/testRouter");
const user = require("./modules/userRouter");
const resource = require("./modules/resource");
module.exports = (app) => {
  app
  .use("/test", test)
  .use("/user", user)
  .use("/resource", resource)
};
```

## 解决方案

- 通过主页面放置
```js
<router-view></router-view>
```
进行页面的替换，当只有一个这个时，无论在哪里进行跳转都会将新的页面加载到这里
当有多个时，可以使用路由嵌套的方式

## 路由嵌套





# 功能
## 接入支付宝的相关sdk
实现发送短信或者支付功能
```js
//发送验证码示例
const accessKeyId = process.env.KEYID;
const secretAccessKey = process.env.SECRET;
const signName = process.env.SIGNNAME;
const templateCode = process.env.TEMPLATECODE;

// 引入依赖
const SMSClient = require('@alicloud/sms-sdk')
/**
 * 发送短信验证码
 * @param phone 接收用户的手机号
 */
async function sendSmsMessage (phone) {
    try {
        console.log("开始发送短信验证码");
        let verify = Math.random().toString().slice(-6) // 随机6位验证码
        let phoneNum = phone // 手机号
        // 初始化 sms_client
        const smsClient = new SMSClient({accessKeyId, secretAccessKey})
        // 发送短信
        smsClient.sendSMS({
            PhoneNumbers: phoneNum, // 发送对象手机号
            SignName: signName, // 签名名称
            TemplateCode: templateCode, // 模版CODE
            TemplateParam: `{"code":'${verify}'}`, // 短信模板变量对应的实际值，JSON格式
        })
        console.log("发送短信sendSmsMessage执行完成.")
        return verify
    }catch (error) {
        console.log("发送短信sendSmsMessage异常错误：" + err);
        // console.log()
        return false
    }
}
module.exports = {
    sendSmsMessage
}
```




## 数据库相关功能
