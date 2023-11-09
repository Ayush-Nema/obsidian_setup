# Multiple columns in Obsidian window

Paste the following HTML codeblock to add multiple columns. The example provides generation of two cols.

```html
<div style="width: 100%;">
  <div style="width: 50%; float: left;">This is column 1</div>
  <div style="width: 50%; float: right;">This is column 2</div>
</div>
```

### Example
```markdown
<div style="width: 100%;">
  <img src="attachment:c4ac45af-8d38-4b7b-8dbc-c6fcbf82a001.png"  width="20%" height="20%">
  <div style="width: 50%; float: left;"></div> <!-- Empty Column for spacing -->
    <img width="10%" height="20%">
  <img src="attachment:bf70ebcf-4835-4788-b5b9-8f52d2ae6836.png"  width="35%" height="30%">
</div>

<div style="width: 100%;">
  <img src="attachment:ed77fe46-7593-4bdd-ab74-e4fa1c6cdb42.png"  width="35%" height="30%">
  <img src="attachment:a52abe6b-6052-4066-b751-d24549cca8c0.png"  width="35%" height="30%">
    <img src="attachment:123357d7-b3e1-4932-84df-2b341477ec98.png"  width="25%" height="30%">
</div>
```

- There is an Obsidian extension: [multi-column markdown](https://github.com/ckRobinson/multi-column-markdown) for creating multiple column and customizing them. Check usage in Git page.
