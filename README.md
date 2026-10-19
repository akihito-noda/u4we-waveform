# U4We 受信波形ビューア

導電性テキスタイル上の UART 伝送方式 U4We（UART for Wearables）について，受信波形を実時間軸で確認するブラウザ用ツールです．
AC 等価回路（論文 Fig. 3）の素子値 L∥ [µH]，C_tex [nF]，R_D [Ω] を入力すると，論文の式 (1)(2) に基づく受信電圧 v_RX(t) を描画します．

## 使い方

`index.html` をブラウザで開きます（インストール不要）．GitHub Pages で公開した場合はそのURLを開きます．

- **ステップ応答**: 1 つのパルスエッジに対する応答を表示します．同じ L, C で ζ = 1 とした参照波形を破線で重ねます．
- **ビット列**: 入力したビット列（既定は 0x55 の UART フレーム）について，各エッジの応答を重ね合わせて表示します．
- 減衰比 ζ と，設計条件 ω₀T_S > 2π を満たすかどうかを表示します．
  - ζ < 1（振動的）: R_D を減らす
  - ζ > 1（過減衰）: R_D を増やす
  - パルス幅に対して応答が遅い: L∥ または C_tex を減らす
- 「R_D を臨界制動値に設定」ボタンで R_D = ½√(L∥/C_tex)（ζ = 1）を入力します．

## モデル

```
V_RX(s) = (2ζ/ω₀) · ω₀² / (s² + 2ζω₀s + ω₀²)      … (1)
ω₀ = 1/√(L∥ C_tex),  ζ = (1/2R_D) √(L∥/C_tex)      … (2)
```

入力 V₀ は 1 V の単位ステップとして正規化しています．

## 出典

A. Noda, "UART for Wearables (U4We): DC Power and Carrierless Signal Transfer Over Conductive Textiles,"
*IEEE Transactions on Circuits and Systems II: Express Briefs*, 2026. doi:[10.1109/TCSII.2026.3735640](https://doi.org/10.1109/TCSII.2026.3735640)

## ライセンス

[MIT License](LICENSE)
