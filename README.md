# 概要
マイクから音声を取得して、あらかじめmasterに登録しておいた楽曲との判定を行う。  
判定できた場合は、slackに通知する。  

# 準備
1. `scripts/record_wav.py` によって録音する。  
    録音時間と保存先を設定
2. `scripts/add_master.py` によってmasterにfingerprintを登録する。  
    wavファイルを指定する

# 実行
`python3 main.py`で実行可能
以下のファイルの設定を確認しておく
- `env/local.py`
- `detect_parameter.py`

## 判定アルゴリズム
- `detect.py`
- `fingerprint.py`

### アルゴリズム概要
1. 対数スペクトログラムを計算
2. ローカルピークを求める
3. あるローカルピークとその周辺のローカルピーク、時間差を使いハッシュを計算
4. あらかじめ登録しておいたハッシュ同士のマッチングを取る
5. マッチングした2つのハッシュが得られた音声開始からの経過時刻の差のヒストグラムを作成
6. 大きい順に結果の候補となる

## その他
- サンプリング周波数は頑健性のため小さい値にしている
- 現状、masterは1楽曲でも問題ない
