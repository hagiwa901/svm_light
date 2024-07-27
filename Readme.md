# 概要
SVMLightの開発環境  
## 公式ページ
https://www.cs.cornell.edu/people/tj/svm_light/

# 環境
- Docker: 27.0.3
- docker-compose: 2.28.1

# 実行方法
## データセットのダウンロード
下記のURLよりデータをダウンロードして解凍    
https://osmot.cs.cornell.edu/svm_light/examples/example1.tar.gz

ダウンロードした後は下記のようなフォルダ構成にする
```
.
├── Readme.md
├── compose.yml
├── example1
│   ├── predictions
│   ├── test.dat
│   ├── train.dat
│   └── words
└── svm_light
    └── Dockerfile
```

## モデルの学習
### 1.モデルを学習する仮想環境を立てる
```
docker-compose build svm_learn 
```
### 2.仮想環境内でモデルを学習させる
```
docker-compose run svm_learn 
```
下記のように表示されて、`example1/`にモデルファイル`model`が作成されていることを確認する  
```
......
untime for XiAlpha-estimates in cpu-seconds: 0.00
XiAlpha-estimate of the error: error<=5.85% (rho=1.00,depth=0)
XiAlpha-estimate of the recall: recall=>95.40% (rho=1.00,depth=0)
XiAlpha-estimate of the precision: precision=>93.07% (rho=1.00,depth=0)
Number of kernel evaluations: 45954
Writing model file...done
```
## モデルの予測
### 1.学習したモデルで予測する仮想環境を立てる
```
docker-compose build svm_classify
```
### 2.学習したモデルで予測をする
```
docker-compose run svm_classify
```
下記のように表示されること
```
......
Reading model...OK. (878 support vectors read)
Classifying test examples..100..200..300..400..500..600..done
Runtime (without IO) in cpu-seconds: 0.00
Accuracy on test set: 97.67% (586 correct, 14 incorrect, 600 total)
Precision/recall on test set: 96.43%/99.00%
```
## データセットを変更する場合
`.env`ファイルの中身を下記のように修正する。
```
TRAIN_DATASET=学習させたいデータセットのファイルパス
```
