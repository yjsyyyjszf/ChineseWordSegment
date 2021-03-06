ChineseWordSegment
==================


##中文分词程序说明
###Documents for ChineseWordSegment Program 

1. 系统功能

 本程序可以实现以下功能：选取字典载入，选择分词的方向，计算程序执行的时间, 语料库的选择来自于1998年人民日报的中文词以及最近的搜狗词库，两个词典可以随意选择，进行分词效果的对比。

2. 算法设计以及数据结构


  算法: 最大正向(逆向)匹配算法，即在词典中匹配到最大长度的词语，可以从正向和逆向两方面匹配，匹配的结果可能不相同
  数据结构：数据结构的选择主要体现在对于字典的单词的匹配上，查找的速度快慢直接影响的是程序的分词效率。因此有以下三种数据结构 可供选择：
  (1)线性表 + 二分查找 ：将词典中的词语存在一个线性表中（数组即可），经过去重和排序预处理之后，在程序执行中进行二分有序查找。
  (2)C++ 的hash_map : 对于查找哈希表是一种比较好的数据结构，避免了去重操作，效率比较高，C++ 中的hash_map对应着红黑二叉树。
  (3)Trie 树（字典树）： 字典树是一种对于存储无重复的字典序的字符串的优势很明显，插入简单，查询速度快。
（本程序在实现的过程中是使用的哈希表构建）


3. 程序执行框图

 初始化字典函数 CreatDic(): 实现从文件中逐行读入词语并且不断加入到哈希表完善词表的建立。正向逆向分隔函数Segment(string s1) & ReverseSegment(string s1): 分别从正向和逆向  对从输入文件读入的每行词语进行匹配，调用初始化字典中的函数Find( string s) 来确定最大的匹配长度。实现分隔函数SegmentSentence (string line, int type) : type ==1 是进行正向处理，type ==2 时进行逆向处理，函数中包括了对于非中文字符的特殊处理。 

4. 程序分词效果以及效率讨论

 (1)分词效率讨论：  
 正向和逆行程序在程序执行快慢上并没有太大的区别都是基于最大匹配的算法实现的，即对于最大分词长度MaxWordLength的都和词典进行匹配，那么时间复杂度就是O（n * m）。根据测试语料，程序跑出的时间为47.132s，那么对于千万级的语料的效果仍然不是很理想，可以在以后考虑基于统计语言模型的算法。

 (2)分词效果讨论：
  中文自动分词的效果很多时候是由分词的颗粒度决定的，不同人对于分词会有不同的理解，所以准确度的衡量可以是人工干预下的分词。在程序中使用了自动机，通过本程序的分词结果和标准答案进行对拍，经过大量的实验可以得出准确率维持在70% 到80% 附近。 考虑到语料库距离现在时间很长，并且测试预料中大量出现的人名比如“老瓦”大大影响了分词的效果，我把词语“老瓦”添加到词典dict.txt 中，再次计算程序分词的准确率。对于简单的基本的匹配的算法的效果很难得到保证，增加对于特定统计语言模型，不断进行学习提高准确率。

5. 程序完善的地方

 （1）进一步完善程序的鲁棒性，可以支持恶意输入，包括非中文字符等。
  (2)改善数据结构，优化算法执行效率，提供易于调用的接口，方便其他应用程序使用中文分词做预处理。
 







   
