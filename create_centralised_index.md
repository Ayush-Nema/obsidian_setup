# Purpose
We often have several files in the Vault and each file has its own content. But as the number of file increases maintaining the content gets hard.
The idea of the document is to create a centralised index by pulling the headings from all the files in the directory and present them in a single place.


# Instructions
- Get `dataview` extension
- Enable `Enable Javascript queries` from the plugin setting
- Create a new note and paste the following code to it
- Mention the name of directory to be indexed in the 1st line: `const folder =`
- Mention `dataviewjs` beside the 3 ticks (\`\`\`dataviewjs)

---
# Code blocks
## Create interactive index
```
const folder = "Contextual bandits";
const pages = dv.pages(`"${folder}"`).sort(p => p.file.name);

for (let page of pages) {
    const file = app.vault.getAbstractFileByPath(page.file.path);
    if (file && file.path) {
        const content = await app.vault.read(file);
        const lines = content.split("\n");

        dv.header(2, page.file.name); // File name as main section

        let toc = [];

        for (let line of lines) {
            const match = line.match(/^(#+)\s+(.*)/);
            if (match) {
                const level = match[1].length;
                const text = match[2].trim();

                // Generate anchor link
                const anchor = text
                    .toLowerCase()
                    .replace(/[^\w\s-]/g, "")
                    .replace(/\s+/g, "-");

                const indent = " ".repeat(level - 1); // em space for nicer indentation
                const link = `[[${page.file.path}#${text}|${text}]]`; // Obsidian-style link

                toc.push(`${indent}- ${link}`);
            }
        }

        if (toc.length > 0) {
            dv.paragraph(toc.join("\n"));
        } else {
            dv.paragraph("_No headings found in this note._");
        }
    }
}
```



## Create index with interaction and collapsible titles
```
const folder = "Contextual bandits";
const pages = dv.pages(`"${folder}"`).sort(p => p.file.name);

for (let page of pages) {
    const file = app.vault.getAbstractFileByPath(page.file.path);
    if (file && file.path) {
        const content = await app.vault.read(file);
        const lines = content.split("\n");

        let toc = [];

        for (let line of lines) {
            const match = line.match(/^(#+)\s+(.*)/);
            if (match) {
                const level = match[1].length;
                const text = match[2].trim();

                const anchor = text
                    .toLowerCase()
                    .replace(/[^\w\s-]/g, "")
                    .replace(/\s+/g, "-");

                const indent = " ".repeat(level - 1); // em space
                const link = `[[${page.file.path}#${text}|${text}]]`;

                toc.push(`${indent}- ${link}`);
            }
        }

        const contentBlock = toc.length > 0
            ? toc.join("\n")
            : "_No headings found in this note._";

        // Render a collapsible section for each file
        dv.paragraph(
            `<details><summary><strong>${page.file.name}</strong></summary>\n\n${contentBlock}\n\n</details>`
        );
    }
}
```


## Create basic index
```
const folder = "Contextual bandits";
const pages = dv.pages(`"${folder}"`);

for (let page of pages) {
    const file = app.vault.getAbstractFileByPath(page.file.path);
    if (file && file.path) {
        const content = await app.vault.read(file);
        const lines = content.split("\n");

        dv.header(3, page.file.name);
        for (let line of lines) {
            const headingMatch = line.match(/^(#+)\s+(.*)/);
            if (headingMatch) {
                const level = headingMatch[1].length;
                const text = headingMatch[2];
                const anchor = text
                    .toLowerCase()
                    .replace(/[^\w\s-]/g, "")
                    .replace(/\s+/g, "-");

                dv.paragraph(
                    `${"  ".repeat(level - 1)}- [${text}](${page.file.path}#${anchor})`
                );
            }
        }
    }
}
```
