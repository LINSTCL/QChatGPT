# QChatGPT🤖

### 🎉现已支持接入ChatGPT网页版，详情请完成部署并查看底部**插件**小节或[此仓库](https://github.com/RockChinQ/revLibs)

- 到[项目Wiki](https://github.com/RockChinQ/QChatGPT/wiki)可了解项目详细信息
- 由bilibili TheLazy制作的[视频教程](https://www.bilibili.com/video/BV15v4y1X7aP)
- 测试号: 2196084348（已加载逆向库插件、每分钟限速）、~~1480613886（已加载逆向库插件）~~（被封）
- 交流、答疑群: ~~204785790~~（已满）、691226829 
  - **进群提问前请您`确保`已经找遍文档和issue均无法解决**  
  - **进群提问前请您`确保`已经找遍文档和issue均无法解决**  
  - **进群提问前请您`确保`已经找遍文档和issue均无法解决**  
- QQ频道机器人见[QQChannelChatGPT](https://github.com/Soulter/QQChannelChatGPT)

通过调用OpenAI GPT-3模型提供的Completion API来实现一个更加智能的QQ机器人  

## ✅功能

<details>
<summary>✅回复符合上下文</summary>

  - 程序向模型发送近几次对话内容，模型根据上下文生成回复
  - 您可在`config.py`中修改`prompt_submit_length`自定义联系上下文的范围

</details>

<details>
<summary>✅支持敏感词过滤，避免账号风险</summary>

  - 难以监测机器人与用户对话时的内容，故引入此功能以减少机器人风险
  - 编辑`sensitive.json`，并在`config.py`中修改`sensitive_word_filter`的值以开启此功能
</details>


<details>
<summary>✅群内多种响应规则，不必at</summary>

  - 默认回复`ai`作为前缀或`@`机器人的消息
  - 详细见`config.py`中的`response_rules`字段
</details>

<details>
<summary>✅使用官方api，不需要网络代理，稳定快捷</summary>

  - 不使用ChatGPT逆向接口，而使用官方的Completion API，稳定性高
  - 您可以在`config.py`中自定义`completion_api_params`字段，设置向官方API提交的参数以自定义机器人的风格

</details>

<details>
<summary>✅完善的多api-key管理，超额自动切换</summary>

  - 支持配置多个`api-key`，内部统计使用量并在超额时自动切换
  - 请在`config.py`中修改`openai_config`的值以设置`api-key`
  - 可以在`config.py`中修改`api_key_fee_threshold`来自定义切换阈值
  - 运行期间向机器人说`!usage`以查看当前使用情况
</details>

<details>
<summary>✅组件少，部署方便，提供一键安装器及Docker安装</summary>

  - 手动部署步骤少
  - 提供自动安装器及docker方式，详见以下安装步骤
</details>

<details>
<summary>✅支持预设指令文字</summary>

  - 支持以自然语言预设文字，自定义机器人人格等信息
  - 详见`config.py`中的`default_prompt`部分
  - 支持设置多个预设情景，并通过!reset、!default等指令控制，详细请查看[wiki指令](https://github.com/RockChinQ/QChatGPT/wiki/%E5%8A%9F%E8%83%BD%E4%BD%BF%E7%94%A8#%E6%9C%BA%E5%99%A8%E4%BA%BA%E6%8C%87%E4%BB%A4)
</details>

<details>
<summary>✅完善的会话管理，重启不丢失</summary>

  - 使用SQLite进行会话内容持久化
  - 最后一次对话一定时间后自动保存，请到`config.py`中修改`session_expire_time`的值以自定义时间
  - 运行期间可使用`!reset` `!list` `!last` `!next` `!prompt`等指令管理会话
</details>
<details>
<summary>✅支持对话、绘图等模型，可玩性更高</summary>

  - 现已支持OpenAI的对话`Completion API`和绘图`Image API`
  - 向机器人发送指令`!draw <prompt>`即可使用绘图模型
</details>
<details>
<summary>✅支持指令控制热重载、热更新</summary>

  - 允许在运行期间修改`config.py`或其他代码后，以管理员账号向机器人发送指令`!reload`进行热重载，无需重启
  - 运行期间允许以管理员账号向机器人发送指令`!update`进行热更新，拉取远程最新代码并执行热重载
</details>
<details>
<summary>✅支持插件加载🧩</summary>

  - 自行实现插件加载器及相关支持
  - 详细查看[插件使用页](https://github.com/RockChinQ/QChatGPT/wiki/%E6%8F%92%E4%BB%B6%E4%BD%BF%E7%94%A8)
</details>
<details>
<summary>✅私聊、群聊黑名单机制</summary>

  - 支持将人或群聊加入黑名单以忽略其消息
  - 详见Wiki`加入黑名单`节
</details>
<details>
<summary>✅回复速度限制</summary>

  - 支持限制单会话内每分钟可进行的对话次数
  - 具有“等待”和“丢弃”两种策略
    - “等待”策略：在获取到回复后，等待直到此次响应时间达到对话响应时间均值
    - “丢弃”策略：此分钟内对话次数达到限制时，丢弃之后的对话
  - 详细请查看config.py中的相关配置
</details>

详情请查看[Wiki功能使用页](https://github.com/RockChinQ/QChatGPT/wiki/%E5%8A%9F%E8%83%BD%E4%BD%BF%E7%94%A8#%E5%8A%9F%E8%83%BD%E7%82%B9%E5%88%97%E4%B8%BE)

## 🔩部署

**部署过程中遇到任何问题，请先在[QChatGPT](https://github.com/RockChinQ/QChatGPT/issues)或[qcg-installer](https://github.com/RockChinQ/qcg-installer/issues)的issue里进行搜索**

### - 注册OpenAI账号

**可以直接进群找群主购买**  
或参考以下文章自行注册

> ~~[只需 1 元搞定 ChatGPT 注册](https://zhuanlan.zhihu.com/p/589470082)~~（已失效）  
> [手把手教你如何注册ChatGPT，超级详细](https://guxiaobei.com/51461)

注册成功后请前往[个人中心查看](https://beta.openai.com/account/api-keys)api_key  
完成注册后，使用以下自动化或手动部署步骤

### - 自动化部署

<details>
<summary>展开查看，以下方式二选一，Linux首选Docker，Windows首选安装器</summary>

#### Docker方式

请查看此仓库[mikumifa/QChatGPT-Docker-Installer](https://github.com/mikumifa/QChatGPT-Docker-Installer)

#### 安装器方式
使用[此安装器](https://github.com/RockChinQ/qcg-installer)（若无法访问请到[Gitee](https://gitee.com/RockChin/qcg-installer)）进行部署

- 安装器目前仅支持部分平台，请到仓库文档查看，其他平台请手动部署

</details>

### - 手动部署
<details>
<summary>手动部署适用于所有平台</summary>

- 请使用Python 3.9.x以上版本  
- 请注意OpenAI账号额度消耗  
  - 每个账户仅有18美元免费额度，如未绑定银行卡，则会在超出时报错  
  - OpenAI收费标准：默认使用的`text-davinci-003`模型 0.02美元/千字  

#### 配置Mirai

按照[此教程](https://yiri-mirai.wybxc.cc/tutorials/01/configuration)配置Mirai及YiriMirai  
启动mirai-console后，使用`login`命令登录QQ账号，保持mirai-console运行状态

#### 配置主程序

1. 克隆此项目

```bash
git clone https://github.com/RockChinQ/QChatGPT
cd QChatGPT
```

2. 安装依赖

```bash
pip3 install yiri-mirai openai colorlog func_timeout
pip3 install dulwich
```

3. 运行一次主程序，生成配置文件

```bash
python3 main.py
```

4. 编辑配置文件`config.py`

按照文件内注释填写配置信息

5. 运行主程序

```bash
python3 main.py
```

无报错信息即为运行成功

**常见问题**

- mirai登录提示`QQ版本过低`，见[此issue](https://github.com/RockChinQ/QChatGPT/issues/38)
- 如提示安装`uvicorn`或`hypercorn`请*不要*安装，这两个不是必需的，目前存在未知原因bug
- 如报错`TypeError: As of 3.10, the *loop* parameter was removed from Lock() since it is no longer necessary`, 请参考 [此处](https://github.com/RockChinQ/QChatGPT/issues/5)

</details>

## 🚀使用

查看[Wiki功能使用页](https://github.com/RockChinQ/QChatGPT/wiki/%E5%8A%9F%E8%83%BD%E4%BD%BF%E7%94%A8#%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F)

## 🧩插件生态

现已支持自行开发插件对功能进行扩展或自定义程序行为  
详见[Wiki插件使用页](https://github.com/RockChinQ/QChatGPT/wiki/%E6%8F%92%E4%BB%B6%E4%BD%BF%E7%94%A8)  
开发教程见[Wiki插件开发页](https://github.com/RockChinQ/QChatGPT/wiki/%E6%8F%92%E4%BB%B6%E5%BC%80%E5%8F%91)

### 示例插件

在`tests/plugin_examples`目录下，将其整个目录复制到`plugins`目录下即可使用

- `cmdcn` - 主程序指令中文形式
- `hello_plugin` - 在收到消息`hello`时回复相应消息
- `urlikethisijustsix` - 收到冒犯性消息时回复相应消息

### 更多

欢迎提交新的插件

- [revLibs](https://github.com/RockChinQ/revLibs) - 将ChatGPT网页版接入此项目，关于[官方接口和网页版有什么区别](https://github.com/RockChinQ/QChatGPT/wiki/%E5%AE%98%E6%96%B9%E6%8E%A5%E5%8F%A3%E4%B8%8EChatGPT%E7%BD%91%E9%A1%B5%E7%89%88)
- [hello_plugin](https://github.com/RockChinQ/hello_plugin) - `hello_plugin` 的储存库形式，插件开发模板
- [dominoar/QchatPlugins](https://github.com/dominoar/QchatPlugins) - dominoar编写的诸多新功能插件（语言输出、Ranimg、屏蔽词规则等）
- [dominoar/QCP-NovelAi](https://github.com/dominoar/QCP-NovelAi) - NovelAI 故事叙述与绘画

## 😘致谢

- [@the-lazy-me](https://github.com/the-lazy-me) 为本项目制作[视频教程](https://www.bilibili.com/video/BV15v4y1X7aP)
- [@mikumifa](https://github.com/mikumifa) 本项目Docker部署仓库开发者
- [@dominoar](https://github.com/dominoar) 为本项目开发多种插件
- [@hissincn](https://github.com/hissincn) 本项目贡献者
- [@LINSTCL](https://github.com/LINSTCL)   GPT-3.5官方模型适配贡献者

以及其他所有为本项目提供支持的朋友们。

## 👍赞赏

<img alt="赞赏码" src="res/mm_reward_qrcode_1672840549070.png" width="400" height="400"/>
