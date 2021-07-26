# 直流モータドライバ基盤
## 仕様　<br>
to252のFETに対応している。用件によって必要となる定格のFETを使うこと
## 注意
FETを変えた場合ゲート入力抵抗、GS間容量(C_add)を適切な値に変更すること。目安は下記 <br>
<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{C_{dg}}{C_{gs}&plus;C_{add}}&space;=&space;0.5" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{C_{dg}}{C_{gs}&plus;C_{add}}&space;=&space;0.5" title="\frac{C_{dg}}{C_{gs}+C_{add}} = 0.5" /></a> <br>
上式で容量を決めたらオシロスコープでFETの立ち下がりを見てセルフターンオンしないゲート入力抵抗を入れる <br>
※セルフターンオンしているとDtimeでカバーできない上下アームオン状態が生まれ、短絡しFETの発熱およびドライバの短絡検知、電流制限に引っかかる。
