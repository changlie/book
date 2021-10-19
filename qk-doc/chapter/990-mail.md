# 邮件发送

邮件每次发送，只能有一个接送人与抄送人


```js
m = mailer()
m.from("xxx@sohu.com") // 发送人
m.to("xxxx@qq.com") // 收件人
// m.cc("xxxx@163.com") // 抄送

m.subject("TurboX v11") // 主题
m.body("congratulation for you!") // 邮件内容
// m.attach("/home/xp/xxx.txt") // 邮件附件本地路径

m.host("smtp.sohu.com") // 邮箱用户所在的邮件服务器域名或IP
m.port(25) // 邮箱用户所在的邮件服务器端口

m.username("xxxx@sohu.com") // 邮箱用户名
m.password("xxxx") // 邮箱token, 需开启pop3/smtp

m.send()

```