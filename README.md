# Tree-sitter-nodekit

Tree-sitter grammar for [NodeKit](https://github.com/small-tech/nodekit)

Forked from [tree-sitter-svelte](https://github.com/Himujjal/tree-sitter-svelte/).

# Install

```
npm i tree-sitter-nodekit tree-sitter
```

Tree-sitter also requires [nodemon](https://nodemon.io/) to run, so also install that if you don’t already have it:

```
npm i -g nodemon
```

Finally, you will need [pnpm](https://pnpm.io/installation). If you’re running Node 16.13 or later, it comes as part of Node so you can simply run the following to activate it:

```
corepack enable
```

# Dev

After installation (`npm i`),

```
npm run dev
```

# Usage

To get started with exploring the grammar in a web-ui. Run:

NOTE: `emcc` must be installed and in your path

```sh
npm run ui
```

To use the grammar from javascript:

```javascript
const Parser = require("tree-sitter");
const NodeKit = require("tree-sitter-nodekit");

const parser = new Parser();
parser.setLanguage(NodeKit);

const sourceCode = `
<get>
  export default () => {
    return {
      name: 'Laura'
    }
  }
</get>
<script>
  export let data
</script>
<h1>Hello, {data.name}!</h1>
`;

const tree = parser.parse(sourceCode);
console.log(tree.rootNode.toString());

// (document
//   (get_element
//     (start_tag (tag_name))
//     (raw_text)
//     (end_tag (tag_name))
//   )
//   (script_element
//     (start_tag (tag_name))
//     (raw_text)
//     (end_tag (tag_name))
//   )
//   (element
//     (start_tag (tag_name))
//     (text)
//     (expression (raw_text_expr))
//     (text)
//     (end_tag (tag_name))
//   )
// )
```

# Languages supported:

- [x] JavaScript/TypeScript
- [x] Rust
- [ ] Go
- [ ] Nim
- [ ] Python

# LICENSE

[MIT](./LICENSE)
