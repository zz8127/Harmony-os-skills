# 打包与上架

> **适用版本**：HarmonyOS 5.0.2+（API 14）及以上，HarmonyOS 6.1 = API 23 稳定，6.0 = API 22 稳定。

## 上架流程概览

```
开发完成 → AGC创建应用 → 配置签名 → 编译打包 → 上架审核 → 上线
```

---

## 前提条件

- 开发者账号已实名认证
- 已在受邀名单中（HarmonyOS 6生态）
- 应用具有软著（部分类目需要）

---

## AGC创建应用

1. 登录 AGC：https://developer.huawei.com/consumer/cn/service/josp/agc/
2. 我的应用 → 创建应用
3. 选择平台：APP(HarmonyOS)
4. 填写应用信息：
   - **应用包名**：必须与 `module.json5` 的 `bundleName` 完全一致
   - **是否元服务**：应用选"否"，元服务选"是"

---

## 签名配置

### 步骤一：生成密钥和CSR

1. DevEco Studio → Build → Generate Key and CSR
2. **Key Store File**：设置.p12文件存储路径
3. **Password**：密钥库密码
4. **Alias**：密钥别名

### 步骤二：申请发布证书

1. AGC → 用户与访问 → 证书管理 → 申请证书
2. 上传.csr文件
3. 下载.cer证书文件

### 步骤三：申请Profile

1. AGC → 用户与访问 → 证书管理 → 申请Profile
2. 选择应用（bundleName必须匹配）
3. 选择发布证书
4. 下载.p7b Profile文件

### 步骤四：配置签名信息

1. DevEco Studio → File → Project Structure → Signing Configs
2. 配置密钥库、证书、Profile文件

---

## 编译打包

### Debug版本

DevEco Studio → Build → Build Hap(s)
- 产物：`build/outputs/hap/debug/entry-debug.hap`

### Release版本（发布）

DevEco Studio → Build → Build App Pack(s)
- 产物：`build/outputs/app-pack/entry-app.app`

**上架必须使用App Pack格式。**

### 构建工具

- DevEco Studio **6.1.0**（支持 API 22/23 稳定版）
- hvigor 构建系统

---

## 应用上架

### 填写应用信息

1. AGC → 我的应用 → 选择应用 → 版本信息
2. 填写：应用名称、图标、描述、截图、隐私声明URL、用户协议URL等

### 审核标准

| 类别 | 审核要点 |
|------|---------|
| 功能完整性 | 核心功能正常运行，无崩溃 |
| 兼容性 | 在主流设备上运行正常 |
| 性能 | 启动时间、内存占用符合标准 |
| 安全 | 无恶意代码、安全漏洞 |
| 合规 | 无违法、违规、侵权内容 |
| 隐私 | 隐私声明真实有效，权限申请合理 |

---

## 常见问题

**Q: bundleName可以修改吗？**
A: 不可以。一旦创建，不可修改，只能重建应用。

**Q: 签名证书过期怎么办？**
A: 重新申请证书，下载新.cer文件，重新签名并上架新版本。

**Q: 可以同时上架手机和平板版本吗？**
A: 可以。在同一个应用下，通过配置deviceTypes支持多设备。
