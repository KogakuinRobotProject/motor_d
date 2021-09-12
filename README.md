# 直流モータドライバ基盤
## 仕様　<br>
to252のFETに対応している。用件によって必要となる定格のFETを使うこと<br>
PWMfreqは20kHz～50kHz(100kHzとかでも動くだろうけど、スイッチング損失えぐい)<br>

|FaultFlag|LEDstate|
|---|---|
|FF1|Green|
|FF2|Red|

<br>

|FF1state|FF2state|MDstate|
|---|---|---|
|0|0|Normal Operation|
|1|0|Overtemperature|
|0|1|Short-to-ground,Short-to-supply,Shorted load|
|1|1|V5 undervoltage,VREG undervoltage,Bootstrap undervoltage|

## FET使用例（FETゲート回路周りの定数）

|MOSFETname|Gate Register|Gate to Source Capasita|
|----|----|----|
|IPD034N06N3G|10|220~1000pF|
|DMTH4005SK3Q|10|1000~2200pF|

## 注意
FETを変えた場合ゲート入力抵抗、GS間容量(C_add)を適切な値に変更すること。目安は下記 <br>
<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{C_{dg}}{C_{gs}&plus;C_{add}}&space;=&space;0.5" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{C_{dg}}{C_{gs}&plus;C_{add}}&space;=&space;0.5" title="\frac{C_{dg}}{C_{gs}+C_{add}} = 0.5" /></a> <br>
上式で容量を決めたらオシロスコープでFETの立ち下がりを見てセルフターンオンしないゲート入力抵抗を入れる <br>
基板上のC_5,C_6の値をFETの追加容量含んだトータルゲートチャージの10倍ほどのコンデンサに変更する<br>
※データシート上では容量ではなく、充電される電荷が記載されているため、電荷にV_gsを徐算すること<br>
※セルフターンオンしているとDtimeでカバーできない上下アームオン状態が生まれ、短絡しFETの発熱およびドライバの短絡検知、電流制限に引っかかる。<br>
※セルフターンオンであると思っていたものがそうでなかった。低負荷状態ではセルフターンオンの発生は確認できなかったが、高負荷時に発生する可能性があるため上記目安を参考に容量を追加すること。<br>
