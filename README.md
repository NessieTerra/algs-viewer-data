# algs-viewer-data

MyALGSday 观赛页的数据仓库。网页通过 `current.json` 发现当前赛事，再加载对应文件。

```text
current.json                       ← 当前指向哪一届（切届只改这个文件）
events/y6-split2-playoffs/
  ├─ schedule.json                 ← 赛程（页面侧维护）
  ├─ teams.json                    ← 分组名单（40 队，含 teamId）
  └─ results.json                  ← 赛果（定时任务自动更新，含 eventId）
```

- `results.json` / `teams.json` 均含 `eventId`，网页读取时与 `current.json` 核对，防止串届或缓存串页。
- 赛果数据来源：Liquipedia（CC-BY-SA 3.0），由自动化脚本按比赛日频率更新（比赛日每 15 分钟，非比赛日每日一次）。
- 切换下一届：新建 `events/<新eventId>/` 填入三份文件 → 修改 `current.json` 的 `eventId` 与三个路径。网页代码不用改。
