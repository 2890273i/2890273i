import hashlib


class Block:

    def __init__(self, timestamp, data, previous_hash=''):
        '''
        区块的初始化
        :param timestamp: 创建时的时间戳
        :param data: 区块数据
        :param previous_hash: 上一个区块的hash
       :param hash: 区块的hash
        '''
        self.previous_hash = previous_hash
        self.timestamp = timestamp
        self.data = data
        self.hash = self.calculate_hash()

    def calculate_hash(self):
        '''
        计算区块哈希值
        :return:
        '''
        # 将区块信息拼接然后生成sha256的hash值
        raw_str = self.previous_hash + str(self.timestamp) + json.dumps(self.data, ensure_ascii=False)
        sha256 = hashlib.sha256()
        sha256.update(raw_str.encode('utf-8'))
        hash = sha256.hexdigest()
        return hash


