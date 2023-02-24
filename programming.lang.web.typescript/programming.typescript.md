TypeScript setup

typscript is a classed superset of javascript and has
- classes
- modules
- interfaces

typescript.ts -> tsc -> javascript.js -> browser

tsc is the typescript compiler and is a node package installed with npm (node package manager)

tsc _transpiles_ `.ts` to `.js`
- **transpile** : also called source-to-source compilers are a subset of compilers that take source code file and translate it to another source code file in another language

vs 

- **compiler:** take source code and turn it into some other language(usually) machine code, notice that this says nothing specifically about source to source because it is more general

node.tsc

e.g.
Helloworld.ts -> tsc -> Helloworld.js -> node

- `tsc Helloworld.ts` 
- `node Helloworld.js`

VSCode has TypeScript language support but does not come with the compiler.

You need to use npm to install the compiler tsc
`npm install -g typescript`

You can also install locally
`npm install --save-dev typescript`

Make a `tsconfig.json` to define project settings

e.g.
``` json
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "sourceMap": true
  }
}
```

Tip: The tsc compiler does not detect the presence of a jsconfig.json file automatically. Use the –p argument to make tsc use your jsconfig.json file, e.g. `tsc -p jsconfig.json`.

[Typescript tutorial](https://code.visualstudio.com/docs/typescript/typescript-tutorial)

[Compiling Typescript](https://code.visualstudio.com/docs/typescript/typescript-compiling)

[transpile vs compile](https://stackoverflow.com/questions/44931479/compiling-vs-transpiling)
