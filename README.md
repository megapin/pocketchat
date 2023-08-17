# 스벨트+타입스크립트+비트

빗에서 스벨트와 타입스크립트로 개발하기 위한 템플릿입니다.

## 추천 IDE 설정

[비주얼 스튜디오 코드](https://code.visualstudio.com/) + [스벨트](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode)

## 공식 스벨트 프레임워이 필요하나요?

[스벨트킷](https://github.com/sveltejs/kit#readme)을 확인하세요.
스벨트킷도 빗(vite)으로 무장된 것 입니다. 
Deploy anywhere with its serverless-first approach and adapt to various platforms, 
with out of the box support for TypeScript, SCSS, and Less, 
and easily-added support for mdsvex, GraphQL, PostCSS, Tailwind CSS, and more.

## 기술적인 고려사항

**왜 스벨트킷으로 하지 않았는가?**

- It brings its own routing solution which might not be preferable for some users.
- It is first and foremost a framework that just happens to use Vite under the hood, not a Vite app.

This template contains as little as possible to get started with Vite + TypeScript + Svelte, while taking into account the developer experience with regards to HMR and intellisense. It demonstrates capabilities on par with the other `create-vite` templates and is a good starting point for beginners dipping their toes into a Vite + Svelte project.

Should you later need the extended capabilities and extensibility provided by SvelteKit, the template has been structured similarly to SvelteKit so that it is easy to migrate.

**Why `global.d.ts` instead of `compilerOptions.types` inside `jsconfig.json` or `tsconfig.json`?**

Setting `compilerOptions.types` shuts out all other types not explicitly listed in the configuration. Using triple-slash references keeps the default TypeScript setting of accepting type information from the entire workspace, while also adding `svelte` and `vite/client` type information.

**Why include `.vscode/extensions.json`?**

Other templates indirectly recommend extensions via the README, but this file allows VS Code to prompt the user to install the recommended extension upon opening the project.

**Why enable `allowJs` in the TS template?**

While `allowJs: false` would indeed prevent the use of `.js` files in the project, it does not prevent the use of JavaScript syntax in `.svelte` files. In addition, it would force `checkJs: false`, bringing the worst of both worlds: not being able to guarantee the entire codebase is TypeScript, and also having worse typechecking for the existing JavaScript. In addition, there are valid use cases in which a mixed codebase may be relevant.

**Why is HMR not preserving my local component state?**

HMR state preservation comes with a number of gotchas! It has been disabled by default in both `svelte-hmr` and `@sveltejs/vite-plugin-svelte` due to its often surprising behavior. You can read the details [here](https://github.com/rixo/svelte-hmr#svelte-hmr).

If you have state that's important to retain within a component, consider creating an external store which would not be replaced by HMR.

```ts
// store.ts
// An extremely simple external store
import { writable } from 'svelte/store'
export default writable(0)
```
