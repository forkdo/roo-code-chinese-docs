# Roo Code 中文文档

本文档使用 AI 翻译

## 项目流程

### 1. 拉取上游文档
1. 创建空分支
```bash
git switch --orphan docs
```

2. 创建 `README.md`
```bash
cat > README.md <<EOF
# 中文文档

本文档使用 AI 翻译
EOF
```

3. 首次提交
```bash
git add .
git commit -am init
git push origin docs
```

4. 设置上游仓库
```bash
# GitHub fork Codespaces 方式已自动设置
git remote add upstream https://github.com/RooCodeInc/Roo-Code-Docs.git
git fetch upstream main
git checkout upstream/main -- docs
```

5. 增量翻译
```bash
git diff docs/
```

6. 本地测试
```bash
git clone https://github.com/RooCodeInc/Roo-Code-Docs.git docsite
cp -r docs_zh/* ./docsite/docs/

cd docsite
npm install
npm start

# 构建
npm build
```

### 2. 安装 AI 助手
1. 安装 CLI 工具 （增量更新直接使用 AI CLI 工具直接对比）
```bash
# npm install -g npm
npm install -g @google/gemini-cli
npm install -g @qwen-code/qwen-code
```

2. 设置环境变量 `.env`
```bash
API_KEY=
MODEL=
API_URL=https://openrouter.ai/api/v1/chat/completions

ROOT_DIR=./docs
EXCLUDE_DIR=update-notes
OUTPUT_MODE=new_folder
```

3. AI 翻译

## 文档管理器
- [Docusaurus](https://docusaurus.io/zh-CN/) （已内置）
```bash
npm install
npm build
```
