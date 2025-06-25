@table.vue#L1-413 @App.vue#L1-109 假设你是一名资深前端开发 现在这里的table组件使用了合并单元格以及异步请求，数据渲染有问题。最开始的数据是这样的：

| Date       | Name  |
| ---------- | ----- |
| 2016-05-01 | 合并1 |
|            | 合并2 |
现在点击箭头展开之后是以下这样
| Date       | Name     |
| ---------- | -------- |
| 2016-05-01 | 合并1    |
|            | 派大星   |
| 2017-05-01 | 海绵宝宝 |
|            | 合并2    |
期望是以下这样
| Date       | Name     |
| ---------- | -------- |
| 2016-05-01 | 合并1    |
|            | 合并2    |
| 2017-05-01 | 派大星   |
|            | 海绵宝宝 |


```
const tmp = [rowRender(row, $index, treeRowData)]
      // 渲染嵌套数据
      if (cur) {
        // currentRow 记录的是 index，所以还需主动增加 TreeTable 的 index
        let i = 0
        const traverse = (children, parent) => {
          if (!(children && children.length && parent)) return
          children.forEach((node) => {
            // 父节点的 display 状态影响子节点的显示状态
            const innerTreeRowData = {
              display: parent.display && parent.expanded,
              level: parent.level + 1,
              expanded: false,
              noLazyChildren: false,
              loading: false,
            }

```