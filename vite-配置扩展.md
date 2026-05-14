# Vite 配置扩展

OTD Core 提供了 `defineConfig` 函数，用于快速配置 Vite 项目，自动集成 Vue、组件自动导入、虚拟路由、微前端等常用插件和配置。

## 核心特性

- **一键配置**: 快速集成常用 Vite 插件和配置
- **组件自动导入**: 自动导入 X-UI 组件和 VXE Table 组件
- **虚拟路由**: 集成文件系统路由插件
- **微前端支持**: 集成 qiankun 微前端框架
- **应用名称管理**: 支持统一配置应用名称，自动注入到 HTML、全局常量和基础路径
- **灵活扩展**: 支持自定义插件和配置覆盖

## 快速开始

### 基础使用

```javascript
// vite.config.js
import { defineConfig } from '@x-ui/otd-core/vite-config';

export default defineConfig({
  // 您的自定义配置
  server: {
    port: 3000
  }
});
```

### 完整配置示例

```javascript
// vite.config.js
import { defineConfig } from '@x-ui/otd-core/vite-config';

export default defineConfig({
  // 应用名称配置
  appName: 'my-app',

  // 微前端配置
  qiankun: {
    name: 'my-micro-app',
    useDevMode: true
  },

  // 自定义组件解析器
  resolvers: [
    // 您的自定义解析器
  ],

  // 是否生成 TypeScript 类型文件
  dts: true,

  // 自定义插件
  plugins: [
    // 您的自定义插件
  ],

  // 其他 Vite 配置
  server: {
    port: 3000,
    proxy: {
      '/api': 'http://localhost:8080'
    }
  },
  build: {
    outDir: 'dist'
  }
});
```

## 配置选项

### appName

- **类型**: `string`
- **默认值**: `undefined`
- **说明**: 应用名称，配置后会自动启用以下功能：

#### 1. HTML 模板转换

自动替换 HTML 模板中的 `<%= name %>` 占位符：

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
  <head>
    <title><%= name %></title>
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
```

配置 `appName: 'my-app'` 后，会自动替换为：

```html
<title>my-app</title>
```

#### 2. 全局常量注入

自动注入 `__APP__NAME__` 全局常量，可在代码中直接使用：

```javascript
console.log(__APP__NAME__); // 'my-app'
```

#### 3. 基础路径配置

生产环境自动配置 base 路径：

```javascript
// 开发环境: base = '/'
// 生产环境: base = '/my-app/'
```

这对于部署到子路径非常有用。

### qiankun

- **类型**: `{ name: string; useDevMode?: boolean }`
- **默认值**: `undefined`
- **说明**: 微前端配置，用于集成 qiankun 框架

#### name

- **类型**: `string`
- **必填**: 是
- **说明**: 微应用名称，用于 qiankun 注册

#### useDevMode

- **类型**: `boolean`
- **默认值**: `true`
- **说明**: 是否启用开发模式

**示例**:

```javascript
export default defineConfig({
  qiankun: {
    name: 'my-micro-app',
    useDevMode: true
  }
});
```

### resolvers

- **类型**: `Array<ComponentResolver>`
- **默认值**: `[]`
- **说明**: 自定义组件解析器数组，用于扩展组件自动导入功能

**示例**:

```javascript
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers';

export default defineConfig({
  resolvers: [ElementPlusResolver()]
});
```

### dts

- **类型**: `boolean`
- **默认值**: `false`
- **说明**: 是否生成组件自动导入的 TypeScript 类型声明文件

**示例**:

```javascript
export default defineConfig({
  dts: true // 会生成 components.d.ts 文件
});
```

### plugins

- **类型**: `Array<Plugin>`
- **默认值**: `[]`
- **说明**: 自定义 Vite 插件数组，会在内置插件之后添加

**示例**:

```javascript
import vueJsx from '@vitejs/plugin-vue-jsx';

export default defineConfig({
  plugins: [vueJsx()]
});
```

### 其他配置

`defineConfig` 支持所有 Vite 原生配置选项，如 `server`、`build`、`resolve` 等。这些配置会与内置配置合并，用户配置优先级更高。

**示例**:

```javascript
export default defineConfig({
  server: {
    port: 3000,
    host: '0.0.0.0',
    proxy: {
      '/api': {
        target: 'http://localhost:8080',
        changeOrigin: true
      }
    }
  },
  build: {
    outDir: 'dist',
    sourcemap: true
  },
  resolve: {
    alias: {
      '@': '/src'
    }
  }
});
```

## 内置插件

`defineConfig` 默认集成了以下插件：

### 1. Vue 3 支持

```javascript
import vue from '@vitejs/plugin-vue';
```

提供 Vue 3 单文件组件支持。

### 2. VXE Table 按需导入

```javascript
import { lazyImport, VxeResolver } from 'vite-plugin-lazy-import';
```

自动按需导入 `vxe-table` 和 `vxe-pc-ui` 组件及样式。

### 3. 组件自动导入

```javascript
import Components from 'unplugin-vue-components/vite';
```

自动导入 X-UI 组件，无需手动 import。默认包含 `XUiResolver`。

### 4. 虚拟路由插件

```javascript
import { createVirtualRoutePlugin } from '@x-ui/otd-core';
```

基于文件系统自动生成路由配置。详见 [路由器 (Router)](./router.md)。

### 5. 微前端插件（可选）

```javascript
import { qiankun } from '@x-ui/otd-core';
```

当配置了 `qiankun.name` 时自动启用。

### 6. HTML 转换插件（可选）

当配置了 `appName` 时自动启用，用于替换 HTML 模板中的应用名称。

## 配置合并策略

`defineConfig` 采用深度合并策略：

1. **内置默认配置**: 基础配置和插件
2. **appName 配置**: 当提供 `appName` 时添加的配置
3. **用户自定义配置**: 通过参数传入的配置

用户配置优先级最高，可以覆盖内置配置。

**示例**:

```javascript
export default defineConfig({
  // 用户的 define 会与 appName 生成的 define 合并
  define: {
    __APP_VERSION__: JSON.stringify('1.0.0')
  },
  // 用户的 base 会覆盖 appName 生成的 base
  base: '/custom-path/'
});
```

## 使用场景

### 场景 1: 简单的 Vue 3 应用

```javascript
import { defineConfig } from '@x-ui/otd-core/vite-config';

export default defineConfig({
  appName: 'simple-app'
});
```

这将自动配置 Vue 3、组件自动导入、虚拟路由等。

### 场景 2: 微前端子应用

```javascript
import { defineConfig } from '@x-ui/otd-core/vite-config';

export default defineConfig({
  appName: 'user-center',
  qiankun: {
    name: 'user-center',
    useDevMode: true
  },
  server: {
    port: 8081
  }
});
```

### 场景 3: 需要自定义组件库

```javascript
import { defineConfig } from '@x-ui/otd-core/vite-config';
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers';

export default defineConfig({
  appName: 'admin-portal',
  resolvers: [ElementPlusResolver()],
  dts: true
});
```

### 场景 4: 复杂的生产配置

```javascript
import { defineConfig } from '@x-ui/otd-core/vite-config';
import vueJsx from '@vitejs/plugin-vue-jsx';
import { visualizer } from 'rollup-plugin-visualizer';

export default defineConfig({
  appName: 'enterprise-app',
  qiankun: {
    name: 'enterprise-app'
  },
  plugins: [vueJsx(), visualizer()],
  server: {
    port: 3000,
    proxy: {
      '/api': 'http://api.example.com'
    }
  },
  build: {
    outDir: 'dist',
    sourcemap: true,
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['vue', 'vue-router', 'pinia']
        }
      }
    }
  }
});
```

## TypeScript 支持

如果使用 TypeScript，可以获得完整的类型提示：

```typescript
// vite.config.ts
import { defineConfig } from '@x-ui/otd-core/vite-config';
import type { ViteConfigOptions } from '@x-ui/otd-core/vite-config/types';

export default defineConfig({
  appName: 'my-app',
  qiankun: {
    name: 'my-app',
    useDevMode: true
  }
} as ViteConfigOptions);
```

## 注意事项

1. **插件顺序**: 内置插件会先于用户插件执行
2. **配置覆盖**: 用户配置会覆盖内置配置，请注意避免意外覆盖
3. **appName 影响**: 配置 `appName` 会影响 HTML、全局常量和 base 路径，请确保这符合您的需求
4. **微前端模式**: 启用 `qiankun` 后会自动配置微前端相关插件，可能影响应用启动方式

## 最佳实践

1. **统一应用名称**: 使用 `appName` 统一管理应用名称，避免硬编码
2. **环境区分**: 使用环境变量配置不同环境的选项

```javascript
export default defineConfig({
  appName: process.env.VITE_APP_NAME,
  server: {
    port: Number(process.env.VITE_PORT) || 3000
  }
});
```

3. **按需配置**: 只配置需要的选项，利用默认值简化配置
4. **类型安全**: TypeScript 项目使用类型导入获得更好的开发体验

## 相关文档

- [路由器 (Router)](./router.md) - 虚拟路由插件详细说明
- [微前端 (Micro)](./micro.md) - 微前端集成指南
- [快速开始](./quickstart.md) - OTD Core 快速开始
