# python
python文本相似度
from gensim import corpora,models,similarities
import jieba
from collections import defaultdict
doc1="F:\\alex python\\wenbenwajue\\dic1.txt"
doc2="F:\\alex python\\wenbenwajue\\dic2.txt"
d1=open(doc1).read()
d2=open(doc2).read()
data1=jieba.cut(d1)
data2=jieba.cut(d2)
#for item in data2:
    #print(item)
#整理成指定的格式
data11=""
for item in data1:
    data11+=item+" "
data21=""
for item in data2:
    data21+=item+" "
#print(data11)
documents=[data11,data21]
texts=[[word for word in document.split()]
       for document in documents] #弄成列表的形式
#print(texts)
frequency=defaultdict(int)
for text in texts:
    for token in text:
        frequency[token]+=1
        '''
texts=[[word for word in text if frequency[toekn]>3]
       for text in texts]
'''
dictionary=corpora.Dictionary(texts)
dictionary.save("F:\\alex python\\wenbenwajue\\.gao.txt")
doc3="F:\\alex python\\wenbenwajue\\dic3.txt"
print(dictionary)
d3=open(doc3).read()
data3=jieba.cut(d3)
data31=""
for item in data3:
    data31+=item+" "
new_doc=data31
new_vec=dictionary.doc2bow(new_doc.split())
corpus=[dictionary.doc2bow(text) for text in texts]
tfidf=models.TfidfModel(corpus)
featureNum=len(dictionary.token2id.keys())
index=similarities.SparseMatrixSimilarity(tfidf[corpus],num_features=featureNum)
sim=index[tfidf[new_vec]]
