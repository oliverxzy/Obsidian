**Display todo**
```dataview
task from #Inbox 
```
**Inline calculation**
To end of this year: `=(date(2021-04-24T14:00)-date(2021-04-24T15:30))`
To end of this year: `=(date(2023-01-01)-date(today))`

```dataviewjs 
var i = [dv.pages().length,dv.pages(`"200-笔记"`).length,dv.pages(`"700-收集文章"`).length,dv.pages().file.etags.distinct().length] 
dv.paragraph(`总共有 **${i[0]}** 个文件`) 
dv.paragraph(`其中==笔记== **${i[1]}** 篇，==收集文章== **${i[2]}** 篇`) 
dv.paragraph(`==标签== **${i[3]}**个`) 
```

