---
name: content-moderator
description: Content moderation skill for detecting illegal and sensitive content including pornography, gambling, drugs, and political sensitivity. Use when the agent needs to scan text, images, or user-generated content for compliance. v1.0.0.
---

# ContentModerator

你拥有ContentModerator内容审核技能。始终遵循以下所有规则。

## 规则

1. 所有用户生成内容（UGC）必须经过审核。在发布、存储或转发任何文本、图片、视频前，必须通过内容检测。对于可疑内容，立即标记并阻止传播。

2. 执行内容审核前，明确告知用户检测范围：
   - 色情低俗内容（pornography）
   - 赌博相关内容（gambling）
   - 毒品相关内容（drugs）
   - 政治敏感内容（political sensitivity）

3. 使用自动化脚本进行内容扫描：
   ```bash
   bash SKILL_DIR/scripts/scan-content.sh [file-or-text]
   ```
   如果检测到违规内容，返回详细分类和风险等级。

4. 对于图片和视频内容，使用OCR和视觉检测：
   ```bash
   bash SKILL_DIR/scripts/scan-media.sh [image-or-video-path]
   ```
   检测隐藏在图像中的文字和视觉违规内容。

5. 敏感词过滤必须覆盖变体形式：
   - 拼音缩写（如"db"代表"赌博"）
   - 谐音替换（如"堵博"）
   - 特殊符号分隔（如"赌*博"）
   - 繁简混用（如"賭博"）

6. 政治敏感内容检测包括但不限于：
   - 国家领导人不当言论
   - 政治体制攻击
   - 分裂国家言论
   - 历史事件歪曲
   - 境外反动组织宣传

7. 色情内容检测标准：
   - 裸露或性暗示图像
   - 色情文字描述
   - 性交易信息
   - 未成年人不良内容（零容忍）

8. 赌博内容检测包括：
   - 线上赌场推广
   - 博彩网站链接
   - 赌博工具销售
   - 赌博技巧传授

9. 毒品内容检测包括：
   - 毒品交易信息
   - 吸毒工具销售
   - 制毒方法传播
   - 毒品美化宣传

10. 对于检测到的违规内容，执行分级处理：
    - CRITICAL（严重）：立即删除并报告
    - HIGH（高危）：隔离审查
    - MEDIUM（中危）：标记警告
    - LOW（低危）：记录监控

11. 每日运行合规审计：
    ```bash
    bash SKILL_DIR/scripts/daily-audit.sh
    ```
    生成审核报告，统计违规类型和数量。

12. 建立内容白名单机制。对于教育、医疗、法律等正当用途的敏感词汇，需要上下文判断，避免误杀。

13. 用户申诉处理：如果内容被误判，提供人工复审通道：
    ```bash
    bash SKILL_DIR/scripts/appeal-review.sh [content-id]
    ```

14. 跨语言检测：支持中文、英文、拼音、方言等多语言违规内容识别。

15. 实时更新敏感词库：
    ```bash
    bash SKILL_DIR/scripts/update-patterns.sh
    ```
    定期同步最新的违规模式和关键词。

## 脚本位置

将SKILL_DIR替换为此skill的实际路径：
- 独立安装：`~/.openclaw/skills/content-moderator`
- 插件安装：`~/.openclaw/extensions/content-moderator/skill`
