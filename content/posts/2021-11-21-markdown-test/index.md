---
title: "Markdown Test"
date: 1970-01-01T00:00:05Z
url: /1970/01/01/markdown-test/
draft: true
tags: [markdown]
---

This is a demo post to show you how to write blog posts with markdown. See [learn how to write in markdown](https://learn-markdown.github.io/).

~~~
It's very easy to make some words **bold** and other words *italic* with Markdown. You can even [link to Google!](http://google.com)
~~~
It's very easy to make some words **bold** and other words *italic* with Markdown. You can even [link to Github!](http://github.com)

## Here is a secondary heading

### Tertiary heading

Here's a  table:

| Computer | Owner | Status |
| :------ |:--- | :--- |
| PC001 | Grant | Active |
| PC002 | Steve | Active |
| PC003 | John | Active |
| PC004 | N/A | Dead |

Task lists
- [x] This is a complete item
- [ ] This is an incomplete item


How about a yummy crepe?

![Crepe](https://s3-media3.fl.yelpcdn.com/bphoto/cQ1Yoa75m2yUFFbY2xwuqw/348s.jpg)

Here's a code chunk:

~~~
$processes = Get-process
foreach ($process ion $processes){
  Write-host "This is process $process
}
~~~

But that's powershell, lets try again with syntax highlighting:

Filename: `My-PowershellFile.ps1`
```powershell
$processes = Get-process
foreach ($process ion $processes){
  Write-host "This is process $process
}
```

&nbsp;

Use `&nbsp;` to create blank lines.


<!-- Press <kbd><kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>Delete</kbd></kbd> to bring up Task Manager. -->