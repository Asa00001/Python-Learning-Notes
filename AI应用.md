# AI应用 - 提示词工程

提示词（prompt）：是引导大模型（LLM）进行内容生成的命令。

提示词工程（promot engineering）：通过有技巧地编写提示词，使大模型生成尽可能符合预期的内容，这一持续性的过程就称为提示词工程。

**编写提示词的几个可参考要点：**
![[Pasted image 20260713143617.png]]


# AI应用-实战

Streamlit：一个开源的Python库，专门为数据工程师及机器学习工程师设计，用来快速基于Python代码构建交互式的web网站。
## 界面消息展示
```
#初始化聊天信息

if "messages" not in st.session_state:
	st.session_state.messages = []
```

```
#保存用户输入的消息到会话状态(在获取到用户的prompt后)

st.session_state.messages.append({"role": "user", "content": prompt})
```

```
#保存AI的回复到会话状态(在获取到AI的回复后)

st.session_state.messages.append({"role": "assistant", "content": response})
```

```
#显示聊天记录(将聊天记录放在初始化聊天信息后、开始调用AI大模型前)

for message in st.session_state.messages:
	st.chat_message(message["role"]).write(message["content"])
```

## 会话记忆-处理方案（会话历史滚雪球）

将此前全部对话信息打包，一起发送给AI
```
messages=[
	{"role": "system", "content": system_prompt},
	#增加记忆功能（之前储存的消息结构为：{"role": "user", "content": prompt}，刚好对应）
	*st.session_state.messages
],
```

## 流式输出

### 1. 把stream的参数改成true
```
#流式输出

stream=True
```

