---
title: "13：记录一次autodl的codex配置"
date: "2026-04-30T15:29:30+08:00"
slug: "5：记录一次autodl的codex配置"
tags: ["学习记录"]
aliases: ["/2026/04/30/5：记录一次autodl的codex配置/"]
---

# 记录一次配置

首先安装node.js
```bash
apt update 
apt install -y curl curl -fsSL https://deb.nodesource.com/setup_lts.x | bash -
apt-get install -y nodejs
```
验证是否安装成功
```bash
node -v 
npm -v
```
安装codex
```bash
npm i -g @openai/codex --registry=https://registry.npmmirror.com
codex --version
```
创建配置
```bash
mkdir -p ~/.codex
apt update && apt install -y nano
nano ~/.codex/config.toml
```
写以下的配置文件
```toml
model_provider = "OpenAI" 
model = "gpt-5.4" 
model_reasoning_effort = "xhigh" 
disable_response_storage = true 
approval_policy = "never" 
sandbox_mode = "workspace-write" 
personality = "pragmatic" 
web_search = "live" 
suppress_unstable_features_warning = true 
[
features
] 
plan_tool = true 
apply_patch_freeform = true 
view_image_tool = true 
unified_exec = false 
streamable_shell = false 
rmcp_client = true 
[
model_providers.OpenAI
] 
name = "OpenAI" 
base_url = "https://api.hanbbq.top/v1" 
wire_api = "responses" 
requires_openai_auth = true 
[
sandbox_workspace_write
] 
network_access = true
```

创建api的key文件
`nano ~/.codex/auth.json`
```json
{ 
	"OPENAI_API_KEY": "your-api-key-here" 
}
```
`codex chat`验证是否成功
