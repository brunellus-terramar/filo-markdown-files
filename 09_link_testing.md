# Link Testing Document

This document tests various types of links to ensure proper handling.

## Web Links (should open in browser)

1. [Google](https://www.google.com) - Simple HTTPS link
2. [HTTP Example](http://example.com) - HTTP link
3. [GitHub README.md](https://github.com/apple/swift/blob/main/README.md) - Web URL ending in .md
4. [GitHub Markdown File](https://raw.githubusercontent.com/apple/swift/main/README.md) - Raw GitHub .md file
5. [MDN Web Docs](https://developer.mozilla.org/en-US/) - Complex URL with trailing slash

## Local Markdown Links (should open in Filo)

1. [Basic Formatting](01_basic_formatting.md) - Relative link to sibling file
2. [Code Blocks](02_code_blocks.md) - Another relative link
3. [Lists Document](03_lists.md) - Third relative link
4. [Technical Docs](04_technical_docs.md) - Fourth relative link

## Local Links with Anchors

1. [Code Blocks - Python Section](02_code_blocks.md#python) - Relative link with anchor
2. [This Document - Web Links](#web-links-should-open-in-browser) - Anchor link only

## Mixed Edge Cases

1. [File with query-like suffix](05_long_form_reading.md) - Ensure it's treated as local
2. [Document A](06_document_a.md) - Cross-reference test
3. [Document B](06_document_b.md) - Cross-reference test

---

## Test Results Checklist

- [ ] Web links open in default browser
- [ ] Web URLs ending in .md open in browser (not treated as local files)
- [ ] Local .md links open within Filo
- [ ] Anchor links scroll to the correct section
- [ ] Local links with anchors open file and scroll to section
- [ ] Cmd+Click opens web/local links in new window
