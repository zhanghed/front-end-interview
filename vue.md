# vue3

## 创建项目

```txt
pnpm create vue@latest
✔ Project name: …
✔ Add TypeScript? … No / `Yes`✔ Add JSX Support? …`No`/ Yes
✔ Add Vue Router for Single Page Application development? … No /`Yes`✔ Add Pinia for state management? … No /`Yes`✔ Add Vitest for Unit Testing? …`No`/ Yes
✔ Add Cypress for both Unit and End-to-End testing? …`No`/ Yes
✔ Add ESLint for code quality? … No /`Yes`✔ Add Prettier for code formatting? … No /`Yes`
```

## 代码环境

### vscode 插件

```txt
Vue Language Features (Volar)
TypeScript Vue Plugin (Volar)
Eslint
Prettier - Code formatter
禁用vscode内置的ts托管服务（仅使voter的,性能最佳,插件搜索 @builtin ty）
```

### .eslintrc.cjs

```txt
rules: {
  'prettier/prettier': [
    'warn',
    {
      singleQuote: true,
      semi: false,
      printWidth: 80,
      trailingComma: 'none',
      endOfLine: 'auto'
    }
  ],
  'vue/multi-word-component-names': [
    'warn',
    {
      ignores: ['index']
    }
  ],
  'vue/no-setup-props-destructure': ['off']
}
```

### .prettierrc.json

```txt
{
  "$schema": "https://json.schemastore.org/prettierrc",
  "singleQuote": true,
  "semi": false,
  "printWidth": 80,
  "trailingComma": "none",
  "endOfLine": "auto"
}
```

### settings.json（vscode）

```txt
{
  "files.autoSave": "onFocusChange",
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode"
}
```
