# chatgpt-wechat-personal
**在微信个人订阅号中通过调用OpenAI最新接口和gpt-3.5-turbo模型实现ChatGPT聊天机器人的功能**

微信个人订阅号有很多限制，最大的问题是无法主动给用户推送消息，只能在用户发起请求的15秒内回复用户。微信官方会在15秒内发3次请求，为了能在个人订阅号中实现用调用OpenAI的接口返回消息，回复消息必须在15秒的时间内生成。随着OpenAI开放了全新的gpt-3.5-turbo模型，这个需求终于可以实现。

![微信图片_20230309160529](https://user-images.githubusercontent.com/5563148/223959556-b9970db1-66fb-46fa-b3af-54d51c74cd5b.jpg)

- **实现原理：**

1. 腾讯服务器推送用户消息过来时，调用OpenAI的API接口，并将用户的问题和返回的结果存到日志文件中。
2. 在5秒内很可能收不到OpenAI返回的消息。没关系，直接让腾讯服务器发过来的请求响应超时。
3. 等腾讯第二次或第三次查询的时候，第一次请求调用OpenAI的结果也返回并写到文件中了，直接从文件中获取结果返回给用户。

基于以上的原理，建议只做一次性对话，不联系上下文。并且在极端情况下还是可能会出现超时的情况，一般重新问一次就好了。

所有用户的消息都是有日志的。所以，把它发给朋友，看看他们关心的问题，也是很有意思的……

- **功能体验**

![qrcode_for_gh_7d9f69d300ab_258](https://user-images.githubusercontent.com/5563148/223959051-3cbb2c9b-6e37-436a-95c2-7c998379d06c.jpg)

欢迎关注我其他关于ChatGPT的项目！
