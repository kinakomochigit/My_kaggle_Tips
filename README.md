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
