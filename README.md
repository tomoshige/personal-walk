# 日本人向けカロリーモデルシミュレーター

このプロジェクトは、日本人の平均的な体格と生活習慣を考慮したカロリー消費と体重変化のシミュレーションモデルを提供します。基礎代謝量（BMR）、総消費エネルギー量（TDEE）、歩数、運動強度などを考慮し、より現実的なシミュレーションを可能にしています。


## 特徴

- 基礎代謝量の主な推定式として「国立健康・栄養研究所の式（Ganpule の式）」を用いて算出 (W:weight, H:height, A:age)。
- 男性：$$（0.0481×W＋0.0234×H－0.0138×A－0.4235）×1,000/4.186$$
- 女性:$$（0.0481×W＋0.0234×H－0.0138×A－0.9708）×1,000/4.186$$
- 歩数とスポーツ活動を考慮したTDEE計算
- 日々の摂取カロリーと活動量の変動を反映
- 長期的な体重変化のシミュレーション

## 必要条件

- Python 3.6以上

## 使用方法

1. `calorie_model.py`ファイルをインポートします。
2. `Person`クラスのインスタンスを作成し、シミュレーションを実行します。

例：

```python
from calorie_model import Person, run_simulation

# 40歳の日本人男性の例
person = Person(age=40, gender='male', weight=67, height=170, base_activity_level='lightly active')

# 30日間のシミュレーションを実行
results = run_simulation(
    person, 
    days=30, 
    avg_calorie_intake=2000,  # 平均摂取カロリー
    calorie_variance=150,
    avg_steps=7000,  # 平均歩数
    steps_variance=1500,
    avg_sports_duration=30,  # 運動時間（分）
    sports_duration_variance=10,
    sports_intensity='moderate'
)

# 結果の表示
for result in results:
    print(f"Day {result['day']}: Weight = {result['weight']:.2f} kg, "
          f"Calorie Intake = {result['calorie_intake']:.0f} kcal, "
          f"TDEE = {result['tdee']:.0f} kcal")
```

## カスタマイズ

モデルのパラメータは簡単にカスタマイズできます：

- `Person`クラスの初期化時に、年齢、性別、体重、身長、基本活動レベルを設定できます。
- `run_simulation`関数で、シミュレーション期間、平均摂取カロリー、平均歩数、運動時間と強度を設定できます。


## 注意事項

このモデルはデータ分析用のサンプルデータを生成するために作成したものです。あくまでも、一般的な傾向を示すためのものであり、個人の健康管理や医療目的での使用は想定していません。
具体的な健康アドバイスについては、必ず医療専門家に相談してください。
