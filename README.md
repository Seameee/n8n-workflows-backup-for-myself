# n8n-workflows-backup-for-myself

 自用n8n工作流备份，包括网易云歌单、youtube播放列表、pixiv收藏、x岛指定串最近回复的推送服务

<details>
  <summary>更新日志</summary>

  ### 2024/11/21
  为 **网易云歌单推送** 和 **YouTube播放列表更新** 增加 **[x岛](https://www.nmbxd1.com/)** 推送方式

  ### 2024/09/09
  首次更新

</details>

## 使用方法
在n8n创建新的工作流后，选择 Import from File... ，选择下载好的json文件，继续下面的配置
> [!NOTE]
> 需自行配置好账号凭证，包括Telegram、YouTube、Matstodon等，详见[n8n文档](https://docs.n8n.io/integrations/builtin/credentials/ "n8n文档")

### p站收藏推送到telegram频道
> [!NOTE]
> 需要同时导入 p站收藏推送到telegram频道.json 和 p站收藏推送到telegram频道 错误处理程序.json 两个工作流

- 导入链接后，在两个工作流的 **RSS Feed Trigger 节点** 都填入RSSHub的pixiv收藏夹rss订阅链接，详见 [RSSHub文档](https://docs.rsshub.app/routes/social-media#user-bookmark "RSSHub文档")
- 完成配置后激活 **p站收藏推送到telegram频道** 工作流，错误处理程序不需要激活

![效果图](https://github.com/user-attachments/assets/07612ad4-d838-4e26-b46d-f19b28ebc19e)

### x岛更新提醒推送到telegram
> [!NOTE]
> 该工作流每次运行会向x岛服务器发送三次请求，因此更新较慢的串建议拉长检测时间，减轻岛服务器压力

- 导入链接后，修改 **Schedule Trigger 节点** 和 **Wait 节点** 的检测间隔时间
- 修改所有 **HTTP Request 节点**的串id，如`https://api.nmb.best/api/thread/id/需要检测的串id/page/{{ $json.adjustedReplyCount }}`
- 修改各 **telegram 节点** 的频道id或个人id，测试能否更新成功

![效果图](https://github.com/user-attachments/assets/6a500282-0839-4d75-91d2-f62bbff03899)

### youtube播放列表更新推送

- 与x岛工作流类似，导入链接后，修改 **Schedule Trigger 节点** 和 **Wait 节点** 的检测间隔时间
- 修改所有 **Youtube Videos Node** 的 Playlist ID
- 修改各 **telegram 节点** 的频道id或个人id
- 修改 **nmbxd 节点** 中Headers中的userhash值

![telegram效果图](https://github.com/user-attachments/assets/38a24b94-7a4f-4341-b8be-ef097651b5d3)
![Mastodon效果图](https://img.seaya.link/file/1732198995633_20241121222245.png)
![x岛效果图](https://img.seaya.link/file/1732198903042_20241121222116.png)

### 网易云歌单更新推送

- 与p站工作流类似，导入链接后，在工作流的 **RSS Feed Trigger 节点**都填入RSSHub的网易云音乐歌单rss订阅链接，详见 [RSSHub文档](https://docs.rsshub.app/routes/multimedia#%E7%94%A8%E6%88%B7%E6%AD%8C%E5%8D%95 "RSSHub文档")
- 修改各 **telegram 节点** 的频道id或个人id
- 修改 **nmbxd 节点** 中Headers中的userhash值
- 完成配置后激活 **网易云推送到telegram** 工作流

![telegram效果图](https://github.com/user-attachments/assets/e48c4a74-d6eb-40fc-a9dd-89c3ce5cc55d)
![Mastodon效果图](https://img.seaya.link/file/1732199487712_20241121223104.png)
![x岛效果图](https://img.seaya.link/file/1732199545572_20241121223212.png)

