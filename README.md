# EpsiloN-Lang
数学記述言語（アイデア）  
公理系からなるCoreクレートと、基本の定理の集合のStdクレートが標準ライブラリとして提供される  
どちらとも独自のものに置き換えることができ、さまざまな論理体系の記述が可能  
公理系に矛盾がある場合、未定義動作となる  
組み込み機能はいくつかの集合実体と、それらの基本的な写像のみ  
静的に安全性を解析できるRustの影響を大きく受けている  
## 目指すもの
数学定理の体系化
## コード例
ε-N論法で数列`a_n = 1/n`が0に収束することの証明
```
//数列の極限を定義
theorem<T: fn(N) -> R> limit_numseq: T {
    let epsilon = all {x; 0<x & x: R};
    let exist n_0: N;
    let n = all {x; n_0<x};
    let alpha: R;

    prop epsilon_n(self) -> { abs(self(n) - alpha) < epsilon };

    fn lim_inf(self) -> R {
        alpha
    }
}

//数列a_nの定義
fn a(n: N) -> R {
    1/n
}

//定理証明
impl limit_numseq for a {
    let alpha = 0;
    prop epsilon_n(self) -> { abs(self(n) - alpha) < epsilon } {
        use Self::*;
        let a = core::archimedes::prop1::prop(n_0, epsilon, 1);
        let b = src a & src N < n { 1/n < 1/N } & src { self(n) = 1/n } {
            self(n) = 1/n < epsilon
        };
        src b & src n: N {0 < 1/n} {
            abs(self(n) - alpha) = self(n) < epsilon
        }
    }
}

```
## 名称
Epsilon-N論法から。
