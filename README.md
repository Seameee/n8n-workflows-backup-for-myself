# n8n-workflows-backup-for-myself

 自用n8n工作流备份，包括网易云歌单、youtube播放列表、pixiv收藏、x岛指定串最近回复的推送服务
 
## 使用方法
在n8n创建新的工作流后，选择 Import from URL... 输入对应文件的Raw链接，继续下面的配置
> [!NOTE]
> 需自行配置好账号凭证，包括Telegram、YouTube、Matstodon等，详见[n8n文档](https://docs.n8n.io/integrations/builtin/credentials/ "n8n文档")

### p站收藏推送到telegram频道
> [!NOTE]
> 需要同时导入 p站收藏推送到telegram频道.json 和 p站收藏推送到telegram频道 错误处理程序.json 两个工作流

- 导入链接后，在两个工作流的 **RSS Feed Trigger 节点** 都填入RSSHub的pixiv收藏夹rss订阅链接，详见 [RSSHub文档](https://docs.rsshub.app/routes/social-media#user-bookmark "RSSHub文档")
- 完成配置后激活 **p站收藏推送到telegram频道** 工作流，错误处理程序不需要激活

### x岛更新提醒推送到telegram
> [!NOTE]
> 该工作流每次运行会向x岛服务器发送三次请求，因此更新较慢的串建议拉长检测时间，减轻岛服务器压力

- 导入链接后，修改 **Schedule Trigger 节点** 和 **Wait 节点** 的检测间隔时间
- 修改所有 **HTTP Request 节点**的串id，如`https://api.nmb.best/api/thread/id/需要检测的串id/page/{{ $json.adjustedReplyCount }}`
- 修改各 **telegram 节点** 的频道id或个人id，测试能否更新成功

### youtube播放列表更新推送到telegram

- 与x岛工作流类似，导入链接后，修改 **Schedule Trigger 节点** 和 **Wait 节点** 的检测间隔时间
- 修改所有 **Youtube Videos Node** 的 Playlist ID
- 修改各 **telegram 节点** 的频道id或个人id，测试能否更新成功

### 网易云推送到telegram

- 与p站工作流类似，导入链接后，在工作流的 **RSS Feed Trigger 节点**都填入RSSHub的网易云音乐歌单rss订阅链接，详见 [RSSHub文档](https://docs.rsshub.app/routes/multimedia#%E7%94%A8%E6%88%B7%E6%AD%8C%E5%8D%95 "RSSHub文档")
- 修改各 **telegram 节点** 的频道id或个人id，测试能否更新成功
- 完成配置后激活 **网易云推送到telegram** 工作流