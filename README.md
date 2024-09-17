# 3122004581
核心算法
def calc_similarity(text1, text2):
    """
    计算余弦相似度
    :param text1: 文本1
    :param text2: 文本2
    :return: 相似度
    """
    texts = [text1, text2]
    # 建立词袋模型向量化文本123
    dictionary = gensim.corpora.Dictionary(texts)
    corpus = [dictionary.doc2bow(text) for text in texts]
    similarity = gensim.similarities.Similarity('-Similarity-index', corpus, num_features=len(dictionary))  # 计算余弦相似度
    test_corpus = dictionary.doc2bow(text1)     # 将文本转换为bow向量
    cosine_sim = similarity[test_corpus][1]    # 变量类型为<class 'numpy.float32'>
    result = round(cosine_sim.item(), 2)   # 转化为<class 'float'>，并取小数点后两位
    return result
单元测试
import unittest

class Test(unittest.TestCase):
    orig_path = "../data/test1/orig.txt"
    ans_path = "answer.txt"

    def test_dis15_2(self, orig_path=orig_path, ans_path=ans_path):
        test_path = "../data/test2/orig_0.8_dis_15.txt"
        text1 = main.filter_words(main.read_file(orig_path))
        text2 = main.filter_words(main.read_file(test_path))
        main.save_answer(ans_path, main.calc_similarity(text1, text2))
        main.get_answer(ans_path)
        //123

if __name__ == '__main__':
    unittest.main()
