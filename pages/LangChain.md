- > LangChain 是一个开源的Python库，为开发人员提供了构建由大型语言模型 (LLM) 驱动的应用程序的工具。更具体地说，LangChain是一个提示编排工具，可以让开发者更轻松地以交互方式链接不同的提示。
-
- #+BEGIN_NOTE
  LangChain 是一个用于开发由语言模型驱动的应用程序的框架。他主要拥有 2 个能力：
  1. 可以将 LLM 模型与外部数据源进行连接
  2. 允许与 LLM 模型进行交互
  #+END_NOTE
-
-
- LangChain 中主要支持的组件如下所述：
	- Models：各种类型的模型和模型集成，比如OpenAI 的 ChatGPT。
	- Prompts：提示管理、提示优化和提示序列化，通过提示微调模型的语义理解。
	- Memory：用来保存和模型交互时的上下文状态。
	- Indexes：用来结构化文档，以便和模型交互。
	- Chains：一系列对各种组件的调用。
	- Agents：决定模型采取哪些行动，执行并且观察流程，直到完成为止。
-
-
-
- Reference
	- [LangChain 与 LangSmith：构建与微调支持LLM的智能应用双重攻略](https://blog.csdn.net/FrenzyTechAI/article/details/132695264)
	- [LangChain 中文入门教程](https://liaokong.gitbook.io/llm-kai-fa-jiao-cheng/)
	-