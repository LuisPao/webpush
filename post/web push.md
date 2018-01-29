web push

- 推送的价值
  - 客户端消息推送对于提升用户体验有很重要作用，我们可以想象1个场景，譬如你用某抢票软件，假如你没有预付，那么抢到后它及时通知你就非常有价值；另外还有到货通知等。这种类型的通知个性化的，一般有电话，短信，或者客户端的推送几种方式选择。对客户端推送更常见的场景就是新闻资讯类的应用，根据用户的订阅或浏览记录，给用户不定时推送一些ta感兴趣的内容，一方面服务了用户，另一方面从运营来说，可以提升了留存，日活，月活。

- PWA带来的web push
  - 我们以往所接收客户端推送基本就只停留在原生应用，虽然我们依旧在移动互联网浪潮里面，但是还是有一部分用户选择浏览器来满足他们的需求。对于web开发人员来说，Google这两年一直在推的PWA，让我们看看了“web一统天下”的一丝丝曙光，但这个信念的落地现在还为时尚早，或者永远都不可能。不过我们更该关注的是PWA到底带来了什么新的标准，让我们可以更好的服务用户。其中web push就是PWA带来的一个重要的特性，让使用浏览器的用户也能享受到推送的服务。
  - PWA现在推的进展如何？我们知道上个月（2017-12）苹果的桌面版 Safari 46 preview 支持了service worker，本月 IOS11.3 也跟上了PC的节奏。首先，service worker是支持web push最基础的功能，其次，我们看到苹果也有心参与到PWA的建设工作中。

- 实现

  深入web push最新标准和具体实现有很多内容可以分享，所以我将分多篇文章来展开。内容主要参照Google web fundamentals，经由笔者的理解并归纳，倘若更新不及时或者有偏差，请以Google web fundamentals为准。

  - 鸟瞰

    ​

    ​

  - 用户订阅

    用户订阅主要包含两个过程。

    第一，要获取用户对通知（notification）的许可。这是非常重要的一步，假如你获取不到用户的许可，对普通的用户来说，你基本上失去了对ta提供推送服务的机会了，因为要改变这个通知的状态，非常困难。所以一定要在合适的时机或选择一种能规避用户deny的方法来征求用户的许可。

    - 特性检测

    - 注册service worker

      ​

    第二，从pushSubscription（后面简写：pushSub）获取endpoint等信息并传给应用的server。那什么是pushSub？一个对象，包含实现Push相关的接口和信息，通过它可以拿到endpoint（url形式，可以理解为你的应用在用户当前浏览器的id）。

  - server端推送

    当client将pushSub给server，server需要将其保存到database。实际推送消息时，server基于web push protocol（IETF standard）调用pushSub里面的endpoint。

    // todo：什么是endpoint？push service？

    push service是由浏览器厂商决定的，开发者无法控制，但这并不是问题，因为每个push service的API调用是相同的（表达欠佳）。

    消息体必须加密，因为是浏览器厂商决定使用哪个push service，不安全

  - client端接收并处理

    当push service接收到一条消息，用户设备在线的话push service就会向client发送消息。client接收到消息会触发service worker里面的push event，再根据情况向用户展示

- 浏览器支持情况