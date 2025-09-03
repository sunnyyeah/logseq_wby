- 安装相关包
	- ```python
	  # 安装 transformer 模型
	  pip install transformers
	  
	  # 安装 pytorch，由于跑 transformer 模型需要使用深度学习框架，不知道能不能用 tensorflow
	  PyTorch
	  ```
-
- 运行
	- ```python
	  from transformers import GPT2LMHeadModel, GPT2Tokenizer
	  
	  def test_transformer():
	      # 初始化模型和 tokenizer
	      tokenizer = GPT2Tokenizer.from_pretrained("gpt2")
	      model = GPT2LMHeadModel.from_pretrained("gpt2")
	  
	      # 得到用户输入
	      user_input = input("Please enter your query: ")
	  
	      # 对输入进行 encode 并添加到输入语句列表
	      inputs = tokenizer.encode(user_input + tokenizer.eos_token, return_tensors='pt')
	  
	      # 得到模型输出
	      outputs = model.generate(inputs, max_length=500, num_return_sequences=5, no_repeat_ngram_size=2, temperature=0.7)
	  
	      # 对模型输出进行 decode
	      for i in range(5):
	          print(f"Generated response {i + 1}: {tokenizer.decode(outputs[:, inputs.shape[-1]:][i], skip_special_tokens=True)}\n")
	  
	  if __name__ == '__main__':
	      test_transformer()
	  ```
-
-