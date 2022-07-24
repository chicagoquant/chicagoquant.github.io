
# Typescript

keyword: typescript tsc tsconfig.json nodejs

https://khalilstemmler.com/blogs/typescript/node-starter-project/

```shell
mkdir typescript1
cd typescript1

npm init -y # create package.json --> -y answers yes for prompts
npm install typescript --save-dev
npm install @types/node --save-dev # install ambient node.js types

# create a tsconfig.json
npx tsc --init --rootDir src --outDir build \
--esModuleInterop --resolveJsonModule --lib es6 \
--module commonjs --allowJs true --noImplicitAny true

# create 1st typescript file
cat src/index.ts
console.log('Hello world!')

# compile ts -> js
npx tsc      # creats build/index.js from src/index.ts

# cold reloading
npm install --save-dev ts-node nodemon

cat nodemon.json
{
  "watch": ["src"],
  "ext": ".ts,.js",
  "ignore": [],
  "exec": "ts-node ./src/index.ts"
}

# to start nodemon
npm run start:dev

# for creating production build, rimraf is like rm -rf
npm install --save-dev rimraf

# add to package.json
"build": "rimraf ./build && tsc",

# add to package.json
"start": "npm run build && node build/index.js"

# alternatively
node_modules/.bin/tsc --outDir build src/index.ts
node build/index.js
```

# Introduction

```typescript
console.log("...")

let isDone: boolean = false;

let decimal: number = 6;
let big: bigint = 100n;
let color: string = "red";

let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];

let x: [string, number];
x = ["hello", 10];

enum Color { Red=0, Green, Blue };
let c: Color = Color.Green;
```

# data types
```typescript
number // integral or floating point
boolean
string
string[], number[] // arrays
Date // .toDateString()
any // don't do any type checking

let obj: any = { x: 0 };
const x: number = 10;
var x: number = 10;

function funcname(var1: type, var2: type) { ... }
function funcname(var1: type) : returntype { ... return val; }

applyAnonymousFunc( function (s) { ... } );
applyArrowFunc( (s) => { ... });
```

# object as function param
```typescript
function funcname(obj: { field1: type, optionalfield2?: type}) {...}
funcname({field1: val1, optionalfield2: val2});
```

# classes

# modules


# windows env
```shell
set NVM_HOME=c:\tools\nvm-windows\v1.1.7
nvm ls available
nvm use v14.17.5
set NVM_SYMLINK=c:\tools\nvm-windows\v1.1.7\v14.17.5
PATH=%NVM_SYMLINK%;%NVM_HOME%;%PATH%
npm start
```
