Adding a page break
======================

When converting a markdown file to PDF, content occasionally splits unexpectedly, leaving part on the first page and the rest on the next. 
This can be particularly frustrating, especially when dealing with tables. 
To alleviate this issue, incorporating deliberate page breaks ensures better control over the file's content.

To add a page break, paste the following line before the header (without the ticks "`").
```
<div style="page-break-after: always;"></div>
```

Issue link in Obsidian: https://forum.obsidian.md/t/page-breaks-for-pdfs/13107/2
