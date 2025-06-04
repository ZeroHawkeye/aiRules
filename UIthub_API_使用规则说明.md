# UIthub API 使用全局规则

## 核心使用格式

### 基础访问
```
https://uithub.com/[用户名]/[仓库名]
```

### 关键参数组合
```
?maxTokens=[值]&ext=[扩展名]&maxFileSize=[字节数]
```

## 必备参数说明

| 参数 | 用途 | 推荐值 | 示例 |
|------|------|--------|------|
| `maxTokens` | 控制响应大小 | 5000-15000 | `?maxTokens=10000` |
| `ext` | 文件类型筛选 | 按需选择 | `?ext=ts,tsx,js` |
| `maxFileSize` | 排除大文件 | 5000-20000 | `?maxFileSize=15000` |
| `accept` | 响应格式 | application/json | `?accept=application/json` |

## 最佳实践模板

### 1. 代码分析（推荐配置）
```
https://uithub.com/[repo]?ext=ts,tsx,js,py,go&maxFileSize=20000&maxTokens=12000
```

### 2. 文档获取（轻量配置）
```
https://uithub.com/[repo]?ext=md,txt&maxTokens=8000
```

### 3. 配置文件分析
```
https://uithub.com/[repo]?ext=json,yml,toml&maxTokens=5000
```

### 4. 特定目录分析
```
https://uithub.com/[repo]/tree/main/[路径]?ext=[类型]&maxTokens=10000
```

## 上下文优化策略

### 分阶段分析法
1. **项目概览**：`?ext=md&maxTokens=5000`
2. **核心代码**：`?ext=主要语言&maxTokens=15000`
3. **配置文件**：`?ext=json,yml&maxTokens=3000`

### 语言特定配置
- **前端项目**：`?ext=ts,tsx,js,jsx&maxFileSize=15000&maxTokens=12000`
- **后端Go项目**：`?ext=go,mod&maxFileSize=25000&maxTokens=15000`
- **Python项目**：`?ext=py,yml&maxFileSize=20000&maxTokens=12000`
- **文档项目**：`?ext=md,rst&maxTokens=8000`

## 快速模板

### API安全分析专用
```bash
# OWASP项目分析
https://uithub.com/OWASP/API-Security?ext=md,yml,json&maxTokens=15000

# 主流框架源码
https://uithub.com/[framework]?ext=主要语言&maxFileSize=25000&maxTokens=18000

# 安全工具分析
https://uithub.com/[security-tool]?ext=py,go,js&maxFileSize=20000&maxTokens=12000
```

## 注意事项

- ⚠️ **令牌控制**：始终设置maxTokens避免超时
- ⚠️ **文件筛选**：使用ext参数精确控制文件类型
- ⚠️ **分批处理**：大型项目分目录或分文件类型分析
- ⚠️ **公开仓库**：仅支持公开访问的仓库

## Cursor使用建议

1. **设为全局规则**：复制核心参数模板到全局规则
2. **上下文管理**：优先使用较小的maxTokens值（5000-10000）
3. **分阶段查询**：先概览后深入，避免一次性加载过多内容
4. **语言适配**：根据项目技术栈选择合适的ext参数 