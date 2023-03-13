---

title: Syntax
layout: default

---

**bold text**
*italic text*
~~strikethrough text~~
`code text`

[Common markdown style link to the external page](https://github.com/)

[Wikilink style Obsidian link to the internal page](/obsidian-publish/Syntax%20Target)

![Common markdown style link to the external image](https://unsplash.com/photos/MS932mscdhw)

![Wikilink style Obsidian link to the internal image](/obsidian-publish/Syntax%20image.jpg)

# Header 1

## Header 2

### Header 3

#### Header 4

##### Header 5

###### Header 6

> Blockquote

```js
// Code snippet with highlighting
var log = {
	debug(msg: string) {
		console.log(msg)
	}
}
```

*   Unordered list item 1
*   Unordered list item 2
*   Unordered list item 3
    *   Unordered list item 3.1
        *   Unordered list item 3.1.1
            *   Unordered item list 3.1.1.1

1.  Ordered list item 1

2.  Ordered list item 2

3.  Ordered list item 3
    1.  Ordered list item 3.1
        1.  Ordered list item 3.1.1
            1.  Ordered list item 3.1.1.1

4.  Ordered list item
    *   Unordered list item inside ordered

*   Unordered list item
    1.  Ordered list item inside unordered

*   [ ] Unfinished task list item

*   [x] Finished task list item
    *   [ ] Nested unfinished task list item
        *   [x] Nested finished task list item

1.  Ordered list item
    *   Nested unordered list item
        *   [ ] Nested unfinished task
            *   [x] Nested finished task

***

| col1 | col2 | col3 |
| :--- | :--- | :--- |
| 1    | 2    | 3    |

Mermaid Diagrams

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```
