# My_kaggle_Tips

## 前後の値で欠損値置換
pandas で、列Aの欠損値を埋める際に、列Bグループ化した中での1つ前の列Aの値を使って埋めることはffill()でできるが、1つ前の値が存在しない場合に、1つ後の値を使って補完 (bfill()) したい場合はどうしたら良いか。その方法を示す。<br>
horses.loc[:, 'horse_weight'] = horses.groupby('horse_id')['horse_weight'].ffill()
とすることで、horse_weight の中で欠損した値を、horse_id でグループ化した中での1つ前の値を使って埋めることができるが、1つ前の値が存在しない場合に、1つ後の値を使って補完 (bfill()) したい場合はどうしたら良いか。
```
horses.loc[:, 'horse_weight'] = horses.groupby('horse_id')['horse_weight'].ffill()
horses.loc[:, 'horse_weight'] = horses.groupby('horse_id')['horse_weight'].bfill()
```
[pandas で グループごとに ffill() と bfill() を両方適用したい](https://blog.misosi.ru/2020/10/18/pandas-how-to-apply-ffill-and-bfill-for-each-group/)

```
train_df = train_df.sort_values(by=['loc_group', 'startdate']).ffill()
```
[WiDS Datathon 2023: Forecasting with LGBM](https://www.kaggle.com/code/iamleonie/wids-datathon-2023-forecasting-with-lgbm)

## [【pandas】csvの日付をDataFrameに読み込む方法（フォーマット・datetime・parse_dates）](https://www.self-study-blog.com/dokugaku/python-pandas-csv-datetime-parse/)
* parser_dates=True：indexが日付ならdatetimeに変換
* parser_dates=['列名','列名']：指定した列をdatetimeに変換
* parser_dates=[['列名','列名']]：指定した列を結合してdatetimeに変換
    * 結合したい列をリストに入れる。
    * 結合した元の列は削除される。
    * keep_ate_col=Trueでもとの列は削除されない。
* parser_dates={'新列名': ['列名','列名']}：結合した列名を新列名に変更

## 相関係数の見せ方
### numpy.tril()を利用する

```
plt.figure(figsize=(18, 8))
mask = np.triu(np.ones_like(df_train.corr()))
sns.heatmap(df_train.corr(),cmap='YlOrRd',annot=True,mask=mask)
```
![](https://user-images.githubusercontent.com/107327935/223187920-9a918b36-7c7b-4913-8f63-d7e7d015e3ba.png)

```
trigger:
  branches:
    include:
      - main  # ビルドをトリガーするブランチを指定

pool:
  vmImage: 'ubuntu-latest'  # 使用するビルドエージェントイメージを指定

steps:
- script: |
    # CUDA Toolkitのインストール
    wget https://developer.download.nvidia.com/compute/cuda/11.5.0/local_installers/cuda_11.5.0_495.29.05_linux.run
    sudo sh cuda_11.5.0_495.29.05_linux.run --silent --toolkit --override

    # CUDA環境の設定
    export PATH=/usr/local/cuda-11.5/bin${PATH:+:${PATH}}
    export LD_LIBRARY_PATH=/usr/local/cuda-11.5/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}

    # nvccのバージョン確認
    nvcc --version

    # プロジェクトのビルド
    cd your_project_directory  # プロジェクトのディレクトリに移動
    mkdir build
    cd build
    cmake ..
    make

  displayName: 'Build with CUDA'

```

