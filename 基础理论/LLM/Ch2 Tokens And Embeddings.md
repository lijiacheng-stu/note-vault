## 一、LLM Tokenization
1. There are three major factors that dictate how a tokenizer breaks down an input prompt.
	- tokenization method
		- method1: byte paire encoding, BPE, used by GPT
		- method2: Word Piece, used by BERT
		- aim：optimize an efficient set of tokens to represent a text dataset
	- make a number of tokenizer design choices
		- example1: vocabulary size
		- example2: what special tokens to use
	- tokenizer need to be trained on a specific datasets to establish the best vocabulary it can use to represent that dataset.
		- code dataset
		- multilingual text dataset
		- English text dataset
	- 