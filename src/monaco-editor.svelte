<script lang="ts">
    export let value: string;
    export let language: string = "javascript";
    export let editorRef: any = null;
    export let style: string = "height: 240px;";
    export let className: string = "";
    export let minimap: boolean = true;
    import { onMount } from "svelte";
    import editorWorker from "monaco-editor/esm/vs/editor/editor.worker?worker";
    import jsonWorker from "monaco-editor/esm/vs/language/json/json.worker?worker";
    import cssWorker from "monaco-editor/esm/vs/language/css/css.worker?worker";
    import htmlWorker from "monaco-editor/esm/vs/language/html/html.worker?worker";
    import tsWorker from "monaco-editor/esm/vs/language/typescript/ts.worker?worker";
    let divEl: any = null;
    let editor: any;
    let Monaco;
    onMount(async () => {
      self.MonacoEnvironment = {
        getWorker: function(_moduleId, label) {
          if (label === "json") {
            return new jsonWorker();
          }
          if (label === "css" || label === "scss" || label === "less") {
            return new cssWorker();
          }
          if (label === "html" || label === "handlebars" || label === "razor") {
            return new htmlWorker();
          }
          if (label === "typescript" || label === "javascript") {
            return new tsWorker();
          }
          return new editorWorker();
        }
      };
      Monaco = await import("monaco-editor");
      editor = Monaco.editor.create(divEl, {
        value: [
          value
        ].join("\n"),
        language,
        fontSize: 20,
        minimap: {
          enabled: minimap
        },
        lineNumbersMinChars: 3,
        scrollBeyondLastLine: false
      });
      editorRef = editor;
      editor.onDidChangeModelContent(() => {
        value = editor.getValue();
      });
      return () => {
        editor.dispose();
      };
    });
    </script>
    
    <div bind:this={divEl} style={style} class="{className}"/>
    