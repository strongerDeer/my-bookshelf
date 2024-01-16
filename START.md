<!-- https://github.com/wikibook/react-deep-dive-example/tree/main/chapter9/zero-to-next/src -->

1. `npm init` -> 계속 엔터 -> package.json 생성
2. react/react-dom/next 설치

```bash
npm i react react-dom next
```

3. devDependencies 필요 패키지 설치

```bash
npm i -D @types/node @types/react @types/react-dom eslint eslint-config-next typescript
```

4. tsconfig.json 작성

```json
{
  "$scheme": "https://json.schemastore.org/tsconfig.json",
  "compilerOptions": {
    // 타입스크립트를 자바스크립트로 컴파일할 때 사용하는 옵선

    "target": "ES5",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true, // JS, TS 혼재 사용
    "skipLibCheck": true, // d.ts에 대한 검사여부 결정 d.ts(TS에서 제공하는 타입에 대한 정보를 담고 있는 파일)
    "strict": true, // 엄격모드 true 일 경우 "alwaysStrict", "strictNullChecks", "strictBindCallApply", "strictFunctionTypes" ...등도 자동으로 true
    "forceConsistentCasingInFileNames": true, // 파일 이름의 대소문자를 구분하도록 강제
    "noEmit": true, // 컴파일을 하지 않고 타입만 체크. Next.js는 swc가 타입스크립트 파일을 컴파일. 굳이 타입스크립트가 자바스크립트로 컴파일 할 필요 없음.
    "esModuleInterop": true, // CommonJS 방식으로 보낸 모듈을 ES 모듈 방식의 import로 가져올 수 있게 해준다.
    "module": "esnext", // 모듈 시스템 설정. 대표적으로 commonjs(required),esnext(import)가 있다
    "moduleResolution": "node", // 모듈을 해석하는 방식. node는 module이 CommonJS일 때만 사용 가능
    "resolveJsonModule": true, // JSON 파일을 import할 수 있게 해줌. 이옵션을 키면 "allowJs"도 자동으로 켜진다.
    "isolatedModules": true, // TS 컴파일러는 파일에 import나 export가 없다면 단순 스크립트 파일로 인식해 이러한 파일이 생성되지 않도록 막는다.  (모듈 시스템과 연계되지 않고 단독으로 있는 파일의 생성을 막음.)
    "jsx": "preserve", // swc가 JSX 또한 변환해 주기 때문!
    /* tsx 파일 내부에 있는 JSX를 어떻게 컴파일할지 설정. 
    react-jsx: 리액트17에 등장. import React from 'react' 필요 없음.(권장)
    react: 기본값. React.createElement로 변환
    react-jsx: 리액트17에 등장. import React from 'react' 필요 없음
    react-jsxdev: react-jsx + 디버깅 정보 추가
    preserve: 변환하지 않고 그대로 유지. 
    react-native: 리액트 네이티브에서 사용하는 방식. 마찬가지로 변환하지 않음.
    */
    "incremental": true, // TS 마지막 컴파일 정보를 .tsbuildinfo 파일 형태로 만들어 디스크에 저장. 별도 파일로 저장 시 이후에 다시 컴파일러가 호출됐을 때 해당 정보를 활용해 가장 비용이 적게 드는 방식ㅇ으로 컴파일을 수행해 컴파일이 더 빨라지는 효과를 누릴 수 있다.
    "baseUrl": "src", // 모듈을 찾을 때 기준이 되는 디렉터리 저장.
    "paths": {
      "#pages/*": ["pages/*"],
      "#hoosk/*": ["hoosk/*"],
      "#types/*": ["types/*"],
      "#component/*": ["component/*"],
      "#utils/*": ["utils/*"]
    }
  },
  "include": ["next-eng.d.ts", "**/*.ts", "**/*.tsx"], // 타입스크립트 컴파일 대상에서 포함시킬 파일 목록 의미.
  "exclude": ["node_modules"] // 타입스크립트 컴파일 대상에서 제외시킬 파일 목록을 의미.
}
```

5. next.config.js 작성

```js
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true, // 엄격모드 활성화
  poweredByHeader: false, // 보안 취약점으로 취급되는 X-Powered-By 헤더 제거
  eslint: {
    ignoreDuringBuilds: true, // 빌드 시에 ESLint 무시.
  },
}

module.exports = nextConfig
```

6. ESLint/Prettier 설정하기

- 코드 스타일링 등 eslint-config-next가 해주지 않는 일반적인 ESLint 작업을 수행하기 위해 가장 설치 설정이 쉬운 `@titicaca/eslint-config-triple` 설치

```bash
npm i -D @titicaca/eslint-config-triple @titicaca/prettier-config-triple prettier
```

```jsx
const path = require('path');
const createConfig = require('@titicaca/eslint-config-triple/create-config');
const { extents: extendConfigs, overrides } = createConfig({
  type: 'frontend',
  project: path.resolve(__dirname, './tsconfig.json'),
});

module.exports={
  extends:[...extendConfig, 'next/core-web-witals']m
  overrides
}
```

7. 스타일 설정하기

- `styled-components` 사용

```bash
npm i styled-components
npm i -D @types/styled-components
```

```js
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  poweredByHeader: false,
  eslint: {
    ignoreDuringBuilds: true,
  },
  styledComponents: true,
}

module.exports = nextConfig
```
