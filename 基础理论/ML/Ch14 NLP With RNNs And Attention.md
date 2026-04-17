训练一个分词器都需要什么讯息：


images are typically complex and contain a wide variety of objects, making it difficult to encode specific retrieval criteria in an image alone
specify complex visual information in text alone, as describing details of color patterns and the shapes of interest objects is often difficult and imprecise with text

两只并排站立在枝条上的鹦鹉。

Incorporating open-ended text as an additional search criterion allows the inclusion of diverse natural language concepts, modifiers, and search specifications with images to produce a flexible retrieval formulation.


怎样构建这样的包？
了解层级结构会让我们更容易记忆。

from tokenizers.trainers import WordPieceTrainer
trainer = WordPieceTrainer(vocab_size=30522, special_tokens=["[UNK]", "[CLS]", "[SEP]", "[PAD]", "[MASK]"])
files = [f"data/wikitext-103-raw/wiki.{split}.raw" for split in ["test", "train", "valid"]]
bert_tokenizer.train(files, trainer)
bert_tokenizer.save("data/bert-wiki.json")


from tokenizers import Tokenizer
from tokenizers.models import WordPiece
bert_tokenizer = Tokenizer(WordPiece(unk_token="[UNK]"))


tokenizier:
- normalizer
- pre_tokenizer
- model
- post_processor



指的是什么？
BPE algorithm：分词和映射？还是生成vocab的？
train the tokenizer