# Hello Guide

```go
func main() {
    fmt.Println("hello world")
}
```

!> 一段重要的内容，可以和其他 **Markdown** 语法混用。

?> _TODO_ 完善示例

## Github 任务列表
- [ ] foo
- bar
- [x] baz
- [] bam <~ not working
  - [ ] bim
  - [ ] lim

## 图片处理
![logo](https://docsify.js.org/_media/icon.svg ':size=WIDTHxHEIGHT')
![logo](https://docsify.js.org/_media/icon.svg ':size=50x100')
![logo](https://docsify.js.org/_media/icon.svg ':size=100')

<!-- 支持按百分比缩放 -->

![logo](https://docsify.js.org/_media/icon.svg ':size=10%')


你需要在 html 和 Markdown 内容中插入空行。 当你需要在 details 元素中渲染 Markdown 时很有用
```markdown
<details>
<summary>自我评价（点击展开）</summary>

- Abc
- Abc

</details>
```
<details>
<summary>自我评价（点击展开）</summary>

- Abc
- Abc

</details>

Markdown 内容也可以被 html 标签包裹。
<div style='color: red'>

- listitem
- listitem
- listitem

</div>