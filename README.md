# Monaco Editor Svelte

An easy to use component that intergrates monaco editor in your svelte application.

## How to use -

```html
<script>
import { MonacoEditor} from "svelte-monaco-editor";

let editorValue;
</script>

<MonacoEditor style="width: 100%; height: 40vh;" language="javascript" bind:value={editorValue}/>
```

## Props that are available -

```html
<!--
    Value - Editor Value, Type - String
-->
<script>
    let value;
</script>

<MonacoEditor value={value}/>
```
```html
<!--
    Style - CSS Styles, Type - String
-->
<MonacoEditor style="width: 100%;/>
```
```html
<!--
    ClassName - CSS Class, Type - String
-->
<MonacoEditor className="editor"/>
```
```html
<!--
    EditorRef - Editor Reference, Type - Any

    Any code that have to be executed on editor, like configuration can be done by editorRef.
-->

<script>
let editor;
</script>

<MonacoEditor editorRef={editor}/>
```
```html
<!--
    Minimap - Minimap in Editor, Type - Boolean
-->
<MonacoEditor minimap={false}/>
```