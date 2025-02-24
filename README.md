# 项目基建
## 1. tsconfig相关配置

```json
//tsconfig.base.json
{
  "compilerOptions": {
    //指定编译后的文件输出的目录，所有的 .js、.d.ts 文件将输出到 dist 目录。
    "outDir": "dist",
    //指定编译后的 JavaScript 代码的目标版本。
    "target": "es2018",
    //指定模块系统，决定如何处理模块导入和导出 使用 ESNext 模块系统，这意味着使用 import 和 export 语法，并生成符合未来 ECMAScript 标准的模块。
    "module": "esnext",
    //设置模块解析时的基准目录 这个选项指定从哪个目录开始查找模块。如果设置为 "."，表示从当前目录开始。
    "baseUrl": ".",
    //指定是否为编译后的代码生成源映射文件
    "sourceMap": false,
    //指定如何解析模块。 "node" 是 Node.js 的模块解析策略。它会按 Node.js 的规则查找模块（首先检查文件，若没有则查找目录中的 package.json 等）。
    "moduleResolution": "node",
    //指定是否允许编译 JavaScript 文件
    "allowJs": false,
    //启用所有严格的类型检查选项。
    "strict": true,
    //检查并报告未使用的局部变量
    "noUnusedLocals": true,
    //允许导入 JSON 文件 启用此选项后，允许通过 import 语法引入 .json 文件，TypeScript 会将它们当作模块来处理。
    "resolveJsonModule": true,
    //允许从没有默认导出的模块中使用默认导入语法。
    "allowSyntheticDefaultImports": true,
    //启用 ES 模块与 CommonJS 模块之间的兼容性。 它允许你在使用 import 语法时，能够兼容 CommonJS 风格的模块，即使该模块没有使用 export 和 import 语法。
    "esModuleInterop": true,
    //指定是否删除注释。
    "removeComments": false,
    //设置项目的根目录,此选项指定输入文件（.ts）的根目录，通常是项目的根目录。它用于构建目录结构。  这个目录被认为是项目的根目录，所有输入文件都应相对于这个目录来查找。
    "rootDir": ".",
    "types": [],
    "paths": {
      "@element-plus/*": [
        "packages/*"
      ],
      "element-plus": [
        "packages/element-plus"
      ]
    },
    "preserveSymlinks": true
  }
}

```

```json
//tsconfig.json
{
  "files": [],
  "references": [
    {
      "path": "./tsconfig.web.json"
    },
    {
      "path": "./tsconfig.play.json"
    },
    {
      "path": "./tsconfig.node.json"
    },
    {
      "path": "./tsconfig.vite-config.json"
    },
    {
      "path": "./tsconfig.vitest.json"
    }
  ]
}

```

```json
//tsconfig.web.json
{
  "extends": "./tsconfig.base.json",
  "compilerOptions": {
    "composite": true,
    "jsx": "preserve",
    "lib": [
      "ES2018",
      "DOM",
      "DOM.Iterable"
    ],
    "types": [
      "unplugin-vue-macros/macros-global"
    ],
    "skipLibCheck": true
  },
  "include": [
    "packages",
    "typings/env.d.ts"
  ],
  "exclude": [
    "node_modules",
    "**/dist",
    "**/__tests__/**/*",
    "**/gulpfile.ts",
    "**/test-helper",
    "packages/test-utils",
    "**/*.md"
  ]
}


```

```json
//tsconfig.node.json
{
  "extends": "./tsconfig.base.json",
  "compilerOptions": {
    "composite": true,
    "lib": [
      "ESNext"
    ],
    "types": [
      "node"
    ],
    "skipLibCheck": true
  },
  "include": [
    "internal/**/*",
    "internal/**/*.json",
    "scripts/**/*",
    "packages/theme-chalk/*",
    "packages/element-plus/version.ts",
    "packages/element-plus/package.json"
  ],
  "exclude": [
    "**/__tests__/**",
    "**/tests/**",
    "**/dist"
  ]
}


```

## 2. monopreo相关配置

```js
//pnpm-workspace.yaml
packages:
  -'packages/*'
  - 'play'
  - 'docs'

```

```json
//package.json 中也可以配置
"workspaces": [
"packages/*",
"play",
"docs"
],
```

> 如果两个配置文件都存在，pnpm 会优先读取 pnpm-workspace.yaml 文件中的配置。package.json 中的 workspaces 字段更多的是为兼容性考虑。

## 3. vitest暂时没接触，需要下去拓展







## 4. husky

```
pnpm add --save-dev husky  // 如果是monopreo的情况下 需要加 -w ，表示确认加在跟目录下
```

直接修改 .git/hooks：适合小型项目或者没有协作的情况，但不方便版本控制，也不容易管理。
使用 Husky：提供自动化、版本控制、一致性和跨平台支持，尤其适合团队协作项目。

> Husky是一个用于设置Githooks的工具，它在提交代码前后执行自定义脚本，如代码格式化、质量检查。通过简单配置，与ESLint等配合，提升开发团队的代码质量和流程一致性。

当我们依赖安装好了 想要执行他的命令时
pnpm命令是这样：pnpm exec husky init
npm命令是这样的：npx husky init



> npm 和 pnpm 都有一个特殊的 prepare 脚本，它会在安装依赖后执行。这个脚本会在以下场景触发 !!!!!!!!!!!! 所以在prepare脚本下 进行husky的初始化


## 5. commitlint工具使用

```
pnpm add --save-dev  commitlint @commitlint/config-conventional @commitlint/cli
```
1. commitlint：用于检查 Git 提交信息的格式。
2. @commitlint/config-conventional：提供了一些常见的提交规范配置。
3. @commitlint/cli：用于执行 commitlint 检查。

> 在项目根目录下，创建一个 commitlint.config.ts 文件，配置 commitlint 规则。
```js
// commitlint.config.ts
module.exports = {
  extends: ['@commitlint/config-conventional']
}

```
@commitlint/config-conventional 是一个流行的标准，它要求提交信息遵循 Conventional Commits 规范，例如：

feat: add new feature
fix: fix bug
docs: update documentation




然后进入.husky/commit-msg 文件里 粘贴  pnpm exec commitlint --config commitlint.config.ts --edit "$1"



## 6. cz-conventional-changelog 和 cz-git

`cz-conventional-changelog` 和 `cz-git (czg)` 都是 **Commitizen** 适配器，作用类似，都是用于生成符合 **Conventional Commits 规范** 的提交信息，但它们有一些区别：

---


---

### **总结**
| 适配器 | 作用 | 主要区别 |
|--------|------|---------|
| `cz-conventional-changelog` | 传统 Commitizen 适配器 | 仅支持标准 Conventional Commits，不支持 GitMoji，自定义能力较弱 |
| `cz-git (czg)` | 增强版 Commitizen 适配器 | 支持 GitMoji、scope 补全、简洁模式，更灵活 |

如果你的项目只是简单遵循 Conventional Commits 规范，`cz-conventional-changelog` 就够了。  
如果你想要更强大的功能（GitMoji、补全、自定义配置），推荐使用 `cz-git`！ 🚀



> cz-conventional-changelog 和 cz-git 两个依赖的区别
> cz-conventional-changelog	传统 Commitizen 适配器	仅支持标准 Conventional Commits，***不支持 GitMoji***，自定义能力较弱
> cz-git (czg)	增强版 Commitizen 适配器	***支持 GitMoji***、scope 补全、简洁模式，更灵活



### 6.1 cz-conventional-changelog
---
🔹 **作用**：
- 它是一个传统的 Commitizen 适配器，主要用于 **交互式生成符合 Conventional Commits 规范的提交信息**。
- 适用于标准的 `commitizen` 工作流。

🔹 **用法**：
1. 安装：
   ```sh
   pnpm add -D cz-conventional-changelog
   ```
2. 在 `package.json` 里配置：
   ```json
   {
     "config": {
       "commitizen": {
         "path": "cz-conventional-changelog"
       }
     }
   }
   ```
3. 运行：
   ```sh
   npx git-cz
   ```

🔹 **特点**：
- 提供交互式 CLI，帮助用户选择 **类型（feat/fix/docs等）** 并填写提交信息。
- 适用于和 **commitlint、semantic-release** 结合使用。
- 但它比较**传统、功能固定**，不能自定义配置提交规则。

其实我们配置的commitlint.config.ts文件 他结合commitizen后可以触发交互式提示
在package.json中配置
```json
{
  "config": {
    "commitizen": {
      "path": "./node_modules/cz-conventional-changelog"
    }
  }
}

```
然后执行git cz就可以了,但是他不支持gitMoJi，现在我们要切成cz-git

### 6.2 cz-git
🔹 **作用**：
- `cz-git` 是 `cz-conventional-changelog` 的 **增强版**，提供更强大的功能，支持 **GitMoji、scope 自动补全、自定义配置**，适用于现代化项目。

🔹 **用法**：
1. 安装：
   ```sh
   pnpm add -D cz-git
   ```
2. 在 `package.json` 里配置：
   ```json
   {
     "config": {
       "commitizen": {
         "path": "node_modules/cz-git"
       }
     }
   }
   ```
3. 运行：
   ```sh
   npx cz
   ```

🔹 **特点**：
✅ **支持 GitMoji** 🎉（比如 `✨ feat:` 这种 emoji 形式的提交信息）  
✅ **可自定义类型**，比如增加 `test: `、`wip: ` 等  
✅ **可配置 scope 自动补全**，比如 `fix(auth): 修复认证问题`  
✅ **支持简洁模式**，可以直接 `czg "feat: 新功能"` 快速提交



## 7. type-fest 
是一个 TypeScript 类型工具库，提供了许多实用的类型定义，可以帮助开发者在 TypeScript 中更有效地使用类型。它包含了许多常用的类型组合和实用工具类型，使得 TypeScript 的类型系统更加丰富和灵活

## 8. resize-observer-polyfill 
是一个用于提供 ResizeObserver 功能的 polyfill。ResizeObserver 是一种浏览器 API，用于异步观察元素的大小变化。它允许开发者监听特定元素的尺寸变化，便于动态调整布局或进行其他操作。

## 9. Prettier
主要用于代码格式化。它会自动调整代码的风格，使其一致，例如缩进、换行、分号使用等。Prettier 的目标是确保代码的可读性，并通过统一的格式减少代码风格上的争议。
Prettier 通常不涉及代码的逻辑或语义检查，而是专注于格式化。
> pnpm install --save-dev prettier -w

.prettierrc文件下添加如下内容
```json
{
   "semi": false,
   "singleQuote": true,
   "overrides": [
      {
         "files": ".prettierrc",
         "options": {
            "parser": "json"
         }
      }
   ]
}

```

.prettierignore文件下添加如下内容,表示下面这些内容不做prettier格式化
```
dist
node_modules
coverage
CHANGELOG.en-US.md
pnpm-lock.yaml
docs/components.d.ts
docs/.vitepress/cache
```




## 10. ESLint
主要用于代码质量检查和 linting（代码检查）。ESLint 会根据配置的规则分析代码，查找潜在的错误、编码规范问题和不符合最佳实践的代码。
ESLint 可以检测语法错误、变量未定义、未使用的变量、未使用的参数等，并提供建议和警告。
> pnpm add eslint -D

然后初始化eslint
> pnpm exec eslint --init
