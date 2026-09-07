---
name: write-valid-mdx
description: Write pages in ReadMe with valid MDX content. Use when writing any ReadMe documentation to ensure that you are writing valid MDX that will render correctly on ReadMe docs sites.
---

## Page content format instructions
### Close unclosed tags
Place closing tags as early as possible. Close self-closing tags (br, hr, img, etc.) with />.
INPUT: <p><b>This is bold</p>
FIX: <p><b>This is bold</b></p>
INPUT: <br>
FIX: <br />
INPUT: <ul><li>Test</li>
FIX: <ul><li>Test</li></ul>

### Format HTML block elements on separate lines
CRITICAL: If a line has multiple consecutive opening tags, place the FIRST tag on that line and move subsequent tags to new lines.
Work line-by-line while tracking the HTML tree structure.
INPUT:
<details><summary>Test</summary>
</details>
FIX:
<details>
<summary>Test</summary>
</details>
INPUT: <table><tr><td>Test</td></table>
FIX:
<table>
<tr>
<td>Test</td>
</tr>
</table>
INPUT: test<div></div> → FIX: test\n<div></div> (separate text from block)

### Don't allow inline tags to span multiple blocks
INPUT: <span>Text\n\nMore text</span>
FIX: <span>Text</span>\n\n<span>More text</span>

### Convert style attributes of HTML elements to JSX
INPUT: <span style="color: red;">Text</span>
FIX: <span style={{ color: "red" }}>Text</span>

### Markdown isn't parsed inside HTMLBlock, so don't use backticks to escape
If there are escape characters in the HTMLBlock opening bracket, remove them.
INPUT:
<HTMLBlock>\\{\\\`
  <div>Returns { "hello": "test" }</div>
\`}</HTMLBlock>
FIX:
<HTMLBlock>{\`
  <div>Returns { "hello": "test" }</div>
\`}</HTMLBlock>

### Escape open brackets that aren't HTML tags/attributes, ONLY when they are 1) OUTSIDE code blocks 2) NOT on HTMLBlock tags
Angle brackets: escape if not HTML tags. Curly brackets: escape if not variables
INPUT: <api key> → FIX: &lt;api key>;
INPUT: <= hi → FIX: &lt;= hi
INPUT: hi/{hash} -> FIX: hi/&#123;hash&#125;
INPUT: \`\`\`<variable>\`\`\` → FIX: \`\`\`<variable>\`\`\` (no change - inside code block)
INPUT: \`\`\`{hi}\`\`\` → FIX: \`\`\`{hi}\`\`\` (no change - inside code block)

If ERROR says "Expected closing tag for <X>" where X is not HTML, escape: <X> → &lt;X&gt; instead of creating a closing tag (but ONLY if outside code blocks).

### Other conversions
- Remove trailing space HTML entity: Test.&#x20; → Test.
- Links flanked by <>: <https://google.com> → [https://google.com](https://google.com)
- Remove extraneous closing tags: Text</div> → Text
- HTML comments to JSX: <!-- comment --> → {/* comment */}
- <<PRODUCT_NAME>> → {user.PRODUCT_NAME} (except in code/HTML blocks)
- Attribute values: <th colspan=2> → <th colspan={2}>
- Hard line breaks: Use two spaces at end of line
