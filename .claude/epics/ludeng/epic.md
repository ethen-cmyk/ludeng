---
name: ludeng
status: backlog
created: 2025-09-15T10:09:18Z
progress: 0%
prd: .claude/prds/ludeng.md
github: [Will be updated when synced to GitHub]
---

# Epic: ludeng

## Overview

太阳能路灯AI批量场景图生成系统的技术实现，采用前后端分离架构，集成DeepSeek和nanobanana API。系统核心是差异化算法和元素池管理，通过Web界面提供智能/手动两种配置模式，实现批量生成高质量、差异化的产品营销素材图。

## Architecture Decisions

- **前后端分离**：React前端 + Node.js/Express后端，便于独立开发和部署
- **数据库选择**：PostgreSQL存储用户数据和历史记录，Redis缓存热点数据
- **文件存储**：本地文件系统存储图片，支持后续迁移到云存储
- **API集成**：HTTP客户端封装DeepSeek和nanobanana API调用
- **差异化算法**：基于组合键的哈希去重 + 欧几里得距离计算差异度
- **异步处理**：任务队列处理图片生成，WebSocket实时推送进度

## Technical Approach

### Frontend Components
- **上传组件**：支持拖拽上传，图片预览和校验
- **配置面板**：智能/手动模式切换，表单验证和级联选择
- **进度显示**：实时任务状态展示，WebSocket连接管理
- **结果预览**：按组展示图片，支持单张/批量下载
- **历史管理**：任务列表和组合查询界面

### Backend Services
- **文件上传服务**：文件校验、存储和元数据提取
- **元素池管理**：地域数据库CRUD，差异化算法核心逻辑
- **任务调度器**：异步任务队列，支持重试和失败恢复
- **API网关层**：统一外部API调用，错误处理和限流
- **结果管理**：图片生成结果存储、下载和打包服务

### Infrastructure
- **开发环境**：Docker Compose本地开发栈
- **生产部署**：云服务器部署，Nginx反向代理
- **监控观测**：基础的API调用监控和错误日志
- **数据备份**：定期数据库备份和文件系统快照

## Implementation Strategy

### 开发阶段
1. **核心服务开发**（3周）：元素池管理、差异化算法、API集成
2. **前端界面开发**（2周）：用户交互界面和状态管理
3. **集成测试**（1周）：端到端功能测试和性能优化

### 风险缓解
- **API依赖**：实现模拟服务用于开发测试，准备备选API方案
- **性能问题**：设置合理的并发限制，实现请求排队机制
- **成本控制**：API调用监控和预算预警机制

### 测试策略
- **单元测试**：核心算法和业务逻辑覆盖率>80%
- **集成测试**：API集成和数据流验证
- **端到端测试**：关键用户流程自动化测试

## Task Breakdown Preview

高层级任务类别（限制在10个以内）：
- [ ] **数据层设计**：数据库设计、元素池数据准备和导入
- [ ] **差异化算法实现**：组合生成、去重逻辑和相似度计算
- [ ] **外部API集成**：DeepSeek和nanobanana客户端封装
- [ ] **后端核心服务**：文件处理、任务调度和结果管理API
- [ ] **前端界面开发**：上传配置界面和结果展示组件
- [ ] **任务队列系统**：异步处理和进度通知机制
- [ ] **文件存储管理**：图片存储、下载和打包功能
- [ ] **用户历史管理**：历史记录存储和查询接口
- [ ] **系统集成测试**：端到端功能验证和性能测试
- [ ] **部署和监控**：生产环境配置和基础监控设置

## Dependencies

### 外部服务依赖
- **DeepSeek API**：提示词增强服务，需要API密钥和配额
- **nanobanana API**：图片生成服务，核心依赖需要备选方案
- **地域数据源**：需要收集和整理≥100个县级地域特征数据

### 内部团队依赖
- **产品团队**：元素池数据整理和用户验收测试
- **运营团队**：地域数据验证和使用反馈
- **基础设施**：服务器资源和部署环境准备

### 技术前置条件
- 确定云服务商和服务器配置
- 获取外部API的测试和生产环境密钥
- 准备开发环境和CI/CD流程

## Success Criteria (Technical)

### 性能基准
- 单组图片生成时间<3分钟
- 系统支持≤5个并发用户任务
- 文件上传响应时间<30秒
- 差异化算法计算时间<1秒

### 质量门槛
- 核心算法单元测试覆盖率>80%
- 外部API集成成功率>95%
- 系统可用性>99%（非生成期间）
- 代码review通过率100%

### 验收标准
- 智能配置生成8组差异化图片
- 手动配置精确反映指定参数
- 历史去重准确率>99%
- zip打包下载功能正常

## Estimated Effort

### 整体时间线
- **总开发时间**：6周（1.5人月）
- **关键路径**：外部API集成和差异化算法实现
- **并行开发**：前端界面可与后端服务并行开发

### 资源需求
- **后端开发**：1人 × 4周（核心逻辑和API集成）
- **前端开发**：1人 × 2周（用户界面和交互）
- **集成测试**：0.5人 × 1周（测试和优化）
- **数据准备**：产品/运营支持（地域数据整理）

### 关键里程碑
- Week 2: 差异化算法和API集成完成
- Week 4: 后端核心服务和前端界面完成
- Week 5: 端到端集成测试通过
- Week 6: 生产部署和验收测试完成

## Tasks Created
- [ ] 001.md - Project Setup and Environment Configuration (parallel: true)
- [ ] 002.md - Database Design and Schema Implementation (parallel: false)
- [ ] 003.md - Element Pool Data Preparation and Import (parallel: false)
- [ ] 004.md - Differentiation Algorithm Implementation (parallel: false)
- [ ] 005.md - External API Integration Layer (parallel: true)
- [ ] 006.md - File Upload and Management Service (parallel: true)
- [ ] 007.md - Task Queue and Job Processing System (parallel: false)
- [ ] 008.md - Frontend Interface Development (parallel: true)
- [ ] 009.md - System Integration and End-to-End Testing (parallel: false)
- [ ] 010.md - Production Deployment and Monitoring Setup (parallel: false)

Total tasks: 10
Parallel tasks: 4 (001, 005, 006, 008)
Sequential tasks: 6 (002, 003, 004, 007, 009, 010)
Estimated total effort: 236 hours (5.9 weeks)