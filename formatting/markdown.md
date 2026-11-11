# Markdown source layout

Read before creating or editing Markdown files, including list and blockquote prose.

- In every Markdown file you create or edit, keep each prose paragraph on one physical source line, regardless of its length. Never hard-wrap paragraphs to a column limit or put each sentence on a separate line; let the editor or viewer wrap text to the available width.
- Separate paragraphs with blank lines. Keep each prose paragraph within a list item or blockquote on one physical line as well, preserving the required Markdown prefix and indentation.
- Do not insert explicit line breaks inside prose paragraphs, including trailing double spaces, backslash line breaks, or HTML `<br>` tags, unless the user explicitly requests them.
- Preserve structural newlines required by Markdown, including headings, separate list items, tables, fenced code blocks, and literal or preformatted content. These are not prose wrapping.
- When editing Markdown, remove hard wrapping from paragraphs you touch. Do not reflow unrelated content unless requested. Configure any formatter or generator used for Markdown to preserve this rule, and check the resulting diff for newly introduced prose wrapping before finishing.
