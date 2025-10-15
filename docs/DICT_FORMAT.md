# 词库格式说明

本文档说明 keykey 词库的 JSON 格式规范，帮助用户创建自定义词库。

## 📋 基本格式

词库文件是一个 JSON 文件，包含元数据和单词列表：

```json
{
  "id": "词库唯一标识符",
  "name": "词库显示名称",
  "description": "词库描述",
  "category": "分类",
  "tags": ["标签1", "标签2"],
  "length": 100,
  "language": "语言代码",
  "languageCategory": "语言分类",
  "url": "/dicts/文件名.json",
  "words": [
    {
      "name": "单词",
      "trans": ["翻译1", "翻译2"],
      "usphone": "美式音标",
      "ukphone": "英式音标"
    }
  ]
}
```

## 🔑 字段说明

### 元数据字段

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| `id` | string | ✅ | 词库唯一标识符，建议使用小写字母和连字符 |
| `name` | string | ✅ | 词库显示名称，用户在界面上看到的名称 |
| `description` | string | ✅ | 词库描述，简要说明词库内容和用途 |
| `category` | string | ✅ | 分类，如 "基础"、"考试"、"专业" 等 |
| `tags` | string[] | ❌ | 标签数组，用于筛选和搜索 |
| `length` | number | ✅ | 单词总数 |
| `language` | string | ✅ | 语言代码，如 "en"（英语）、"ja"（日语） |
| `languageCategory` | string | ✅ | 语言分类，与 `language` 相同 |
| `url` | string | ✅ | 词库文件路径，相对于 `/dicts/` 目录 |

### 单词字段

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| `name` | string | ✅ | 单词本身 |
| `trans` | string[] | ✅ | 翻译数组，可包含多个翻译 |
| `usphone` | string | ❌ | 美式音标（IPA 格式） |
| `ukphone` | string | ❌ | 英式音标（IPA 格式） |

### 可选字段（扩展）

单词对象还可以包含以下可选字段：

| 字段 | 类型 | 说明 |
|------|------|------|
| `pos` | string | 词性，如 "n."、"v."、"adj." 等 |
| `sentence` | string | 例句 |
| `sentenceTrans` | string | 例句翻译 |

## 📝 完整示例

### 示例 1：基础英语词库

```json
{
  "id": "example-basic",
  "name": "示例词库 - 基础单词",
  "description": "包含100个最常用英语单词的示例词库",
  "category": "基础",
  "tags": ["示例", "基础", "常用"],
  "length": 5,
  "language": "en",
  "languageCategory": "en",
  "url": "/dicts/example-basic.json",
  "words": [
    {
      "name": "hello",
      "trans": ["你好", "哈喽"],
      "usphone": "həˈloʊ",
      "ukphone": "həˈləʊ"
    },
    {
      "name": "world",
      "trans": ["世界"],
      "usphone": "wɜrld",
      "ukphone": "wɜːld"
    },
    {
      "name": "love",
      "trans": ["爱", "喜欢"],
      "usphone": "lʌv",
      "ukphone": "lʌv"
    },
    {
      "name": "learn",
      "trans": ["学习", "学会"],
      "usphone": "lɜrn",
      "ukphone": "lɜːn"
    },
    {
      "name": "happy",
      "trans": ["快乐的", "幸福的"],
      "usphone": "ˈhæpi",
      "ukphone": "ˈhæpi"
    }
  ]
}
```

### 示例 2：带例句的词库

```json
{
  "id": "tech-terms",
  "name": "编程术语",
  "description": "常用编程和技术术语",
  "category": "专业",
  "tags": ["编程", "技术", "IT"],
  "length": 3,
  "language": "en",
  "languageCategory": "en",
  "url": "/dicts/tech-terms.json",
  "words": [
    {
      "name": "algorithm",
      "trans": ["算法"],
      "usphone": "ˈælɡərɪðəm",
      "ukphone": "ˈælɡərɪðəm",
      "pos": "n.",
      "sentence": "This sorting algorithm is very efficient.",
      "sentenceTrans": "这个排序算法非常高效。"
    },
    {
      "name": "variable",
      "trans": ["变量"],
      "usphone": "ˈveriəbl",
      "ukphone": "ˈveəriəbl",
      "pos": "n.",
      "sentence": "Declare a variable before using it.",
      "sentenceTrans": "使用变量前先声明它。"
    },
    {
      "name": "function",
      "trans": ["函数"],
      "usphone": "ˈfʌŋkʃn",
      "ukphone": "ˈfʌŋkʃn",
      "pos": "n.",
      "sentence": "Call the function to execute the code.",
      "sentenceTrans": "调用函数来执行代码。"
    }
  ]
}
```

### 示例 3：最小词库

最简单的词库只需要必需字段：

```json
{
  "id": "my-words",
  "name": "我的单词本",
  "description": "自定义单词列表",
  "category": "自定义",
  "length": 2,
  "language": "en",
  "languageCategory": "en",
  "url": "/dicts/my-words.json",
  "words": [
    {
      "name": "apple",
      "trans": ["苹果"]
    },
    {
      "name": "banana",
      "trans": ["香蕉"]
    }
  ]
}
```

## 🎨 语言分类

支持的语言代码：

| 语言 | 代码 | 示例词库 |
|------|------|----------|
| 英语 | `en` | CET4, CET6, TOEFL |
| 日语 | `ja` | N1, N2, N3 |
| 德语 | `de` | Goethe-Zertifikat |
| 法语 | `fr` | DELF, DALF |
| 西班牙语 | `es` | DELE |
| 韩语 | `ko` | TOPIK |
| 其他 | `code` | 自定义代码片段 |

## 📂 文件命名规范

建议的文件命名格式：

```
<类别>-<名称>-<级别>.json
```

**示例**：
- `cet4-core.json` - 四级核心词汇
- `toefl-reading.json` - 托福阅读词汇
- `programming-javascript.json` - JavaScript 编程术语
- `custom-mywords.json` - 自定义单词本

## 🚀 使用自定义词库

### 方法 1：放入项目目录

1. 创建符合格式的 JSON 文件
2. 将文件放入 `public/dicts/` 目录
3. 重启应用
4. 在词库列表中选择你的词库

### 方法 2：通过 API 加载

1. 将词库文件上传到你的服务器
2. 配置 API 地址：
   ```bash
   # .env.local
   VITE_API_BASE_URL=https://your-api.com
   ```
3. 确保词库可通过 `https://your-api.com/dicts/文件名.json` 访问

### 方法 3：动态导入（高级）

在应用中添加词库选择器，支持用户上传本地 JSON 文件。

## ✅ 验证工具

可以使用在线 JSON 验证工具检查格式：
- [JSONLint](https://jsonlint.com/)
- [JSON Formatter](https://jsonformatter.org/)

## 💡 最佳实践

### 1. 单词数量

- **小型词库**：50-200 个单词（适合专题学习）
- **中型词库**：200-1000 个单词（适合考试备考）
- **大型词库**：1000+ 个单词（适合系统学习）

### 2. 翻译质量

- 提供准确、常用的翻译
- 多个翻译按重要性排序
- 避免过于生僻的释义

### 3. 音标标注

- 使用国际音标（IPA）格式
- 美式和英式音标都提供更好
- 如果不确定，可以省略音标字段

### 4. 分类和标签

- **category**：大分类，如 "考试"、"专业"、"日常"
- **tags**：细分标签，用于筛选，如 ["四级", "核心", "高频"]

### 5. 文件大小

- 单个词库文件建议不超过 5MB
- 超大词库可以拆分成多个文件
- 考虑压缩 JSON（生产环境）

## 🔧 工具和资源

### 词库转换工具

如果你有其他格式的词库（如 TXT, CSV），可以使用工具转换：

```javascript
// 简单的 CSV 转 JSON 示例
const fs = require('fs');

function csvToDict(csvPath, outputPath) {
  const csv = fs.readFileSync(csvPath, 'utf-8');
  const lines = csv.split('\n');
  
  const words = lines.map(line => {
    const [word, translation] = line.split(',');
    return {
      name: word.trim(),
      trans: [translation.trim()]
    };
  });
  
  const dict = {
    id: "custom-dict",
    name: "自定义词库",
    description: "从 CSV 转换",
    category: "自定义",
    length: words.length,
    language: "en",
    languageCategory: "en",
    url: "/dicts/custom-dict.json",
    words: words
  };
  
  fs.writeFileSync(outputPath, JSON.stringify(dict, null, 2));
}
```

### 音标资源

- [IPA 音标对照表](https://www.internationalphoneticalphabet.org/)
- 可以从在线词典获取音标（如有道、牛津等）

## 📞 技术支持

如果在创建词库时遇到问题：

1. 检查 JSON 格式是否正确
2. 确保所有必需字段都已填写
3. 查看浏览器控制台的错误信息
4. 参考本项目的示例词库

## 🔗 相关文档

- [资源说明](./RESOURCES.md)
- [项目 README](../README.md)
- [原项目词库示例](https://github.com/Kaiyiwing/qwerty-learner/tree/master/public/dicts)

---

**最后更新**：2025-10-15

