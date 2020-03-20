## Action1：使用libfm工具对movielens进行评分预测，采用SGD优化算法

### 分割数据集

    import pandas as pd
    from sklearn.model_selection import train_test_split
    data = pd.read_csv('ratings.csv')
    train, test = train_test_split(data, test_size=0.2)    
    test['rating'] = 1
    train.to_csv('train.csv', header = None)
    test.to_csv('test.csv', header = None)

### libFM命令

    perl triple_format_to_libfm.pl -in train.csv -target 3 -delete_column 0 -separator ","
    perl triple_format_to_libfm.pl -in test.csv -target 3 -delete_column 0 -separator ","
    libFM -task r -train train.csv.libfm -test test.csv.libfm -dim '1,1,8' -iter 1000 -method sgd -learn_rate 0.01 -regular '0,0,0.01' -init_stdev 0.1 -out movielens_sgd_out.txt