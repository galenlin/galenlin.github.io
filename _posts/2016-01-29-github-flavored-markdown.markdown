---
layout: post
title:  "Github Flavored Markdown"
date:   2016-01-29 15:36:03
categories: jekyll update
---

## Getting Started

Use `kramdown` as markdown processor in `_config.xml`.

```ruby
markdown: kramdown
kramdown:
  input: GFM
  auto_ids: true
```

Add `markdown-body` style for `posts` content.

```html
<article class="post-content markdown-body">
  {\{ content \}}
</article>
```

Add [github-markdown.css](https://github.com/sindresorhus/github-markdown-css) to html header.


## Tests

### Table

A | B
--|---
a | b

### Task List (Unsupport now)

 - [ ] item 1
 - [x] item 2
 - [ ] item 3

### Highlighting

```java
private static final String DEX_SUFFIX = ".dex";
private static final String JAR_SUFFIX = ".jar";
private static final String ZIP_SUFFIX = ".zip";
private static final String APK_SUFFIX = ".apk";
...
private static Element[] makeDexElements(ArrayList<File> files,
        File optimizedDirectory) {
    ArrayList<Element> elements = new ArrayList<Element>();
    /*
     * Open all files and load the (direct or contained) dex files
     * up front.
     */
    for (File file : files) {
        ZipFile zip = null;
        DexFile dex = null;
        String name = file.getName();
        if (name.endsWith(DEX_SUFFIX)) {
            // Raw dex file (not inside a zip/jar).
            ...
        } else if (name.endsWith(APK_SUFFIX) || name.endsWith(JAR_SUFFIX)
                || name.endsWith(ZIP_SUFFIX)) {
            //---------------------------------------------------
            // Archive File Loading Block
            // if (name.endsWith(".so") doFollowingWithReflect();
            //---------------------------------------------------
            try {
                zip = new ZipFile(file);
            } catch (IOException ex) {
                /*
                 * Note: ZipException (a subclass of IOException)
                 * might get thrown by the ZipFile constructor
                 * (e.g. if the file isn't actually a zip/jar
                 * file).
                 */
                System.logE("Unable to open zip file: " + file, ex);
            }
            try {
                dex = loadDexFile(file, optimizedDirectory);
            } catch (IOException ignored) {
                /*
                 * IOException might get thrown "legitimately" by
                 * the DexFile constructor if the zip file turns
                 * out to be resource-only (that is, no
                 * classes.dex file in it). Safe to just ignore
                 * the exception here, and let dex == null.
                 */
            }
        } else {
            System.logW("Unknown file type for: " + file);
        }
        if ((zip != null) || (dex != null)) {
            elements.add(new Element(file, zip, dex));
        }
    }
    return elements.toArray(new Element[elements.size()]);
}
```
