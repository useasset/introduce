# useAsset
![Logo](logo.jpg)

## 简介
useAsset 是一个轻量、高效的前端资源管理钩子，旨在简化 React 应用中静态资源的加载、缓存和使用。它设计用于处理各种资源类型，包括图片、字体、音频、视频等，提供统一的资源管理接口。

## 功能特性

- **统一资源管理**：提供一致的 API 接口处理不同类型的资源
- **智能缓存**：自动缓存已加载的资源，提高性能和用户体验
- **懒加载支持**：支持资源懒加载，减少初始加载时间
- **错误处理**：内置资源加载错误处理机制
- **类型安全**：提供完整的 TypeScript 类型定义
- **响应式设计**：与 React 组件生命周期无缝集成
- **资源预加载**：支持资源预加载功能，提升用户体验

## 安装指南

### 前提条件

- React 16.8+ (支持 Hooks)
- Node.js 12.0+

### 安装步骤

```bash
# 使用 npm 安装
npm install useasset

# 使用 yarn 安装
yarn add useasset

# 使用 pnpm 安装
pnpm add useasset
```

## 快速开始

### 基本用法

```javascript
// 导入 useAsset 钩子
import { useAsset } from 'useasset';

function ImageComponent() {
  // 加载图片资源
  const { asset, loading, error } = useAsset('/path/to/image.jpg');

  if (loading) {
    return <div>加载中...</div>;
  }

  if (error) {
    return <div>加载失败</div>;
  }

  return <img src={asset} alt="示例图片" />;
}
```

```javascript
// 加载字体资源
import { useAsset } from 'useasset';

function FontComponent() {
  const { asset, loading, error } = useAsset('/path/to/font.woff2', {
    type: 'font',
    preload: true
  });

  // 字体加载后应用
  if (asset) {
    // 应用字体逻辑
  }

  return <div>字体示例</div>;
}
```

## 配置选项

| 选项 | 类型 | 描述 | 默认值 |
|------|------|------|--------|
| `type` | string | 资源类型 ('image', 'font', 'audio', 'video', 'other') | 'other' |
| `preload` | boolean | 是否预加载资源 | false |
| `cache` | boolean | 是否缓存资源 | true |
| `crossOrigin` | string | 跨域设置 | undefined |
| `onLoad` | function | 资源加载完成回调 | undefined |
| `onError` | function | 资源加载错误回调 | undefined |

## 高级用法

### 批量资源加载

```javascript
import { useAssets } from 'useasset';

function GalleryComponent() {
  // 批量加载图片资源
  const { assets, loading, errors } = useAssets([
    '/path/to/image1.jpg',
    '/path/to/image2.jpg',
    '/path/to/image3.jpg'
  ], {
    type: 'image',
    preload: true
  });

  if (loading) {
    return <div>加载中...</div>;
  }

  if (errors.length > 0) {
    return <div>部分资源加载失败</div>;
  }

  return (
    <div className="gallery">
      {assets.map((asset, index) => (
        <img key={index} src={asset} alt={`图片 ${index + 1}`} />
      ))}
    </div>
  );
}
```

### 资源预加载

```javascript
import { preloadAsset } from 'useasset';

// 在应用启动时预加载关键资源
function App() {
  useEffect(() => {
    // 预加载关键图片
    preloadAsset('/path/to/critical-image.jpg', { type: 'image' });
    // 预加载字体
    preloadAsset('/path/to/font.woff2', { type: 'font' });
  }, []);

  return <div>应用内容</div>;
}
```

## API 文档

### `useAsset(url, options)`

加载单个资源。

- **参数**：
  - `url` (string): 资源 URL
  - `options` (object): 配置选项
- **返回值**：
  - `asset` (string | undefined): 加载完成的资源 URL
  - `loading` (boolean): 是否正在加载
  - `error` (Error | null): 加载错误信息

### `useAssets(urls, options)`

批量加载多个资源。

- **参数**：
  - `urls` (string[]): 资源 URL 数组
  - `options` (object): 配置选项
- **返回值**：
  - `assets` (string[]): 加载完成的资源 URL 数组
  - `loading` (boolean): 是否正在加载
  - `errors` (Error[]): 加载错误信息数组

### `preloadAsset(url, options)`

预加载单个资源。

- **参数**：
  - `url` (string): 资源 URL
  - `options` (object): 配置选项
- **返回值**：
  - `Promise<string>`: 资源加载完成的 Promise

### `preloadAssets(urls, options)`

批量预加载多个资源。

- **参数**：
  - `urls` (string[]): 资源 URL 数组
  - `options` (object): 配置选项
- **返回值**：
  - `Promise<string[]>`: 所有资源加载完成的 Promise

## 贡献指南

我们欢迎社区贡献！如果您想参与 useAsset 的开发，请按照以下步骤操作：

1. Fork 仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 打开 Pull Request

## 问题反馈

如果您在使用过程中遇到问题，请在 GitHub 仓库的 [Issues](https://github.com/yourusername/useasset/issues) 页面提交问题描述。

## 许可证

useAsset 采用 [MIT 许可证](LICENSE)。详情请参阅 LICENSE 文件。

## 联系方式

- 项目维护者：[Your Name](https://github.com/yourusername)
- 电子邮件：your.email@example.com
- 项目链接：[https://github.com/yourusername/useasset](https://github.com/yourusername/useasset)

---

**享受资源管理的便捷！** 🚀