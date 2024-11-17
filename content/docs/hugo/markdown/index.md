+++
title = 'Markdown'
linktitle = ''
date = 2024-11-16T14:56:14+03:00
categories = 'docs'
series = 'markdown'
tags = ['markdown','text']
summary = 'Основной синтаксис Markdown для HUGO'
description = ''
images = ['markdown.jpg']
+++

## Заголовки

<h1>H1</h1>
<h2>H2</h2>

Header1
=======

Header2
-------
```markdown
<h1>H1</h1>

<h2>H2</h2>

# H1
## H2

Header1
=======

Header2
-------
```

## Цитаты



{{< bs/config-toggle toml >}}
[params]
  [params.hb]
    [params.hb.blockquotes]
      border_style = 'primary'
      border_width = 4
      bordered = true
{{< /bs/config-toggle >}}

### Цитата без аттрибутов

```markdown
> Tiam, ad mint andaepu dandae nostion secatur sequo quae.
> 
> **Note** that you can use *Markdown syntax* within a blockquote.
```

> Tiam, ad mint andaepu dandae nostion secatur sequo quae.
> 
> **Note** that you can use *Markdown syntax* within a blockquote.

### Цитата с аттрибутами
```markdown
> Don't communicate by sharing memory, share memory by communicating.
{caption="The above quote is excerpted from Rob Pike's [talk](https://www.youtube.com/watch?v=PAAkCSZUG1c) during Gopherfest, November 18, 2015."}
```
> Don't communicate by sharing memory, share memory by communicating.
{caption="The above quote is excerpted from Rob Pike's [talk](https://www.youtube.com/watch?v=PAAkCSZUG1c) during Gopherfest, November 18, 2015."}


> Align to the center
{align=center}
