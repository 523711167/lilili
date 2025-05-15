# ES

### 组成部分

​	词项(term)：将文档通过分词器处理后得到的单词。

​	term dictionary：将文档集通过分词器处理的词项做排序得到term dictionary，可以通过二分法查询。

​	posting list：词项对应出现在文档(每份文档存在唯一主键ID)的对应关系。

​	倒排索引(inverted index)：term dictionary加posting list组成倒排索引。	

> [!CAUTION]
>
> 💡 倒排索引存放在磁盘，在磁盘检索数据比较低效，存放在内存中有更加高效的结构term index

​	term index：将形似的(比如：follow和forward)term，提取相同前缀部分作为上级节点，可以将term dictionary转换树结构，叶节点保存term的地址引用，将term index保存在内存中。

> [!CAUTION]
>
> 💡 通过term index可以定位对应**查找term**在term dictionary的大概位置，从term index定位的位置继续查找可以快速定位**查找term**精确位置。

​	stored fields：保存完整文档和文档ID对应关系的结构，通过倒排索引查找文档ID，再查找完整文档。

​	Doc values：将文档中的特定字段提取单独保存（同时保存文档ID），方便查找排序。

> [!CAUTION]
>
> 💡无Doc values下对**查找term**某字段(term对应文档内容的某个字段)进行排序，先通过倒排索引获取文档ID，再通过stored fields获取文档内容，在提取内部字段进行排序。

​	segment：由倒排索引、term index、stored fileds、Doc values组成，构成复合文件，具备完整搜索功能的最小单元。

> [!CAUTION]
>
> 同时对segment进行读写存在性能瓶颈，因此segment一旦写入完成后（可能还存在其他条件），再写入文档数据，会生成新的segment，保证性能。

​	segment Merging：存在过多的segment的时候（不知道具体的时机），会合并多个segment。

​	Lucene：以上所有结构和机制组成Lucene，Lucene采用并发读去多个segment检索数据，保证效率。