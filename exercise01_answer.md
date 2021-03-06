## Q1

以下のように表示するプログラムを作成せよ

```sh
  100   101   102   103   104   105   106   107   108   109 
  110   111   112   113   114   115   116   117   118   119 
  120   121   122   123   124   125   126   127   128   129 
  130   131   132   133   134   135   136   137   138   139 
  140   141   142   143   144   145   146   147   148   149
```

### 模範解答
```c
#include <stdio.h>

int main() {
    int i, j;
    int x = 100;
    for (i=0; i<5; i++) {
        for (j=0; j<10; j++) {
            printf("  %3d ", x);
            x++;
        }
        printf("\n");
    }
}
```

### 解説

- 作成と表示が一致しているのでそのままできる．
- 2重ループにしなくても 10 個表示したら改行するようにしても良い．
- printf("5%d", x) としても見た目は一緒だが，x が３桁以内とわかっている（仕様で決まっている）なら printf("  %3d", x) の方が明示的で良い

## Q2

以下のように表示するプログラムを作成せよ

```sh
  100   105   110   115   120   125   130   135   140   145 
  101   106   111   116   121   126   131   136   141   146 
  102   107   112   117   122   127   132   137   142   147 
  103   108   113   118   123   128   133   138   143   148 
  104   109   114   119   124   129   134   139   144   149
```

### 模範解答
```c
#include <stdio.h>

int main() {
    int i, j;
    int x = 100;
    int data[5][10];
    for (j=0; j<10; j++) {
        for (i=0; i<5; i++) {
            data[i][j] = x;
            x++;
        }
    }

    for (i=0; i<5; i++) {
        for (j=0; j<10; j++) {
            printf("  %3d ", data[i][j]);
        }
        printf("\n");
    }
}
```

### 解説

- 作成順と表示順が一致してないのでちょっと考える問題
- 数列に強い？人は次のようにするかもしれない
```c
for (i=0; i<5; i++) {
    for (j=0; j<10; j++) {
        printf("  %3d", x);
        x += 5;
    }
    x -= 44;
}
```
が，間違えやすいのと，変更がしにくい（保守性が悪い）のでおすすめできない．

## Q3

次のデータに対する処理を作成せよ

|名前|国語|算数|理科|社会|体育|
|:-:|:-:|:-:|:-:|:-:|:-:|
|A|54|52|24|13|15|
|B|91|19|96|96|91|
|C|19|69|91|96|19|
|D|88|19|55|39|100|
|E|19|42|43|68|19|

```c
#include <stdio.h>

int main() {

    int i,j; // for のインデックス用
    int tmp; // 一時的に利用する
    char name[] = {'A', 'B', 'C', 'D', 'E'};
    int score[5][5] = {
        /*A*/ {54, 52, 24, 13, 15},
        /*B*/ {91, 19, 96, 96, 91},
        /*C*/ {19, 69, 91, 96, 19},
        /*D*/ {88, 19, 55, 39, 100},
        /*E*/ {19, 42, 43, 68, 19}
    };

    /**
     * A から E の５科目の合計を計算せよ
     */
    int total_score[] = {0, 0, 0, 0, 0};
    //
    // この部分を作成
    //

    /**
     * A から E の５科目の平均点を計算せよ
     */
    float person_average[] = {0, 0, 0, 0, 0};
    //
    // この部分を作成
    //

    /**
     * 国語から体育それぞれの平均点を計算せよ
     */
    float kamoku_average[] = {0, 0, 0, 0, 0};
    //
    // この部分を作成
    //

    /**
     * 国語から体育それぞれの最高点を記録せよ
     */
    int max[] = {0, 0, 0, 0, 0};
    //
    // この部分を作成
    //


    /**
     *  国語から体育それぞれの最低点を記録せよ
     */
    int min[] = {100, 100, 100, 100, 100};
    //
    // この部分を作成
    //

    /**
     * AからEが最も得意とする科目（最も得点が高い科目）を見つけて
     * その科目番号（0 から 4）を記録せよ．ただし，同点の場合は
     * どれを選んでも良い
     */
    int favorite[] = {0, 0, 0, 0, 0};
    //
    // この部分を作成
    //

    /**
     * これまでの情報を全部表示するようなきれいな表示を考えよう
     */

    //
    // この部分を作成
    //

    /**
     * 発展：
     * AからEが最も得意とする科目（最も得点が高い科目）を見つけて
     * その科目番号（0 から 4）を記録せよ．ただし，同点の場合は
     * その全部を選択する
     */

    //
    // この部分を作成
    //
    //
    // 表示も再考
    //
}
```

### 模範解答
```c
#include <stdio.h>

int main() {

    int i,j; // for のインデックス用
    int tmp; // 一時的に利用する
    char name[] = {'A', 'B', 'C', 'D', 'E'};
    int score[5][5] = {
        /*A*/ {54, 52, 24, 13, 15},
        /*B*/ {91, 19, 96, 96, 91},
        /*C*/ {19, 69, 91, 96, 19},
        /*D*/ {88, 19, 55, 39, 100},
        /*E*/ {19, 42, 43, 68, 19}
    };

    /**
     * A から E の５科目の合計を計算せよ
     */
    int total_score[] = {0, 0, 0, 0, 0};
    for (i=0; i<5; i++) {
        for (j=0; j<5; j++) {
            total_score[i] += score[i][j];
        }
    }

    /**
     * A から E の５科目の平均点を計算せよ
     */
    float person_average[] = {0, 0, 0, 0, 0};
    for (i=0; i<5; i++) {
        person_average[i] = total_score[i] / 5.0;
    }


    /**
     * 国語から体育それぞれの平均点を計算せよ
     */
    float kamoku_average[] = {0, 0, 0, 0, 0};
    for (j=0; j<5; j++) {
        tmp = 0;
        for (i=0; i<5; i++) {
            tmp += score[i][j];
        }
        kamoku_average[j] = tmp / 5.0;
    }

    /**
     * 国語から体育それぞれの最高点を記録せよ
     */
    int max[] = {0, 0, 0, 0, 0};
    for (j=0; j<5; j++) {
        for (i=0; i<5; i++) {
            if (max[j] < score[i][j]) {
                max[j] = score[i][j];
            }
        }
    }


    /**
     *  国語から体育それぞれの最低点を記録せよ
     */
    int min[] = {100, 100, 100, 100, 100};
    for (j=0; j<5; j++) {
        for (i=0; i<5; i++) {
            if (min[j] > score[i][j]) {
                min[j] = score[i][j];
            }
        }
    }

    /**
     * AからEが最も得意とする科目（最も得点が高い科目）を見つけて
     * その科目番号（0 から 4）を記録せよ．ただし，同点の場合は
     * どれを選んでも良い
     */
    int favorite[] = {0, 0, 0, 0, 0};
    for (i=0; i<5; i++) {
        tmp = 0;
        for (j=0; j<5; j++) {
            if (tmp < score[i][j]) {
                favorite[i] = j;
                tmp = score[i][j];
            }
        }
    }

    /**
     * これまでの情報を全部表示するようなきれいな表示を考えよう
     */
    printf("---------------------------------------------------------\n");
    printf("| 名前 | 国語 | 算数 | 理科 | 社会 | 体育 | 合計 | 平均 |\n");
    printf("---------------------------------------------------------\n");
    for (i=0; i<5; i++) {
        printf("|    %c |", name[i]);
        for (j=0; j<5; j++) {
            if (favorite[i] == j) {
                printf(" *%3d |", score[i][j]);
            } else {
                printf("  %3d |", score[i][j]);
            }
        }
        printf("  %3d |", total_score[i]);
        printf(" %3.1f |", person_average[i]);
        printf("\n");
    }
    printf("---------------------------------------------------------\n");
    printf("| 平均 |");
    for (j=0; j<5; j++) {
        printf(" %3.1f |", kamoku_average[j]);
    }
    printf("             |\n");
    printf("| 最低 |");
    for (j=0; j<5; j++) {
        printf("  %3d |", min[j]);
    }
    printf("             |\n");
    printf("| 最大 |");
    for (j=0; j<5; j++) {
        printf("  %3d |", max[j]);
    }
    printf("             |\n");
    printf("---------------------------------------------------------\n");

    /**
     * 発展：
     * AからEが最も得意とする科目（最も得点が高い科目）を見つけて
     * その科目番号（0 から 4）を記録せよ．ただし，同点の場合は
     * その全部を選択する
     */
    int favorite2[5][5];
    for (i=0; i<5; i++) {
        tmp = 0;
        for (j=0; j<5; j++) {
            if (tmp < score[i][j]) {
                tmp = score[i][j];
            }
        }
        for (j=0; j<5; j++) {
            if (tmp == score[i][j]) {
                favorite2[i][j] = 1;
            } else {
                favorite2[i][j] = 0;
            }
        }
    }

    /* 表示 */
    printf("---------------------------------------------------------\n");
    printf("| 名前 | 国語 | 算数 | 理科 | 社会 | 体育 | 合計 | 平均 |\n");
    printf("---------------------------------------------------------\n");
    for (i=0; i<5; i++) {
        printf("|    %c |", name[i]);
        for (j=0; j<5; j++) {
            if (favorite2[i][j] == 1) {
                printf(" *%3d |", score[i][j]);
            } else {
                printf("  %3d |", score[i][j]);
            }
        }
        printf("  %3d |", total_score[i]);
        printf(" %3.1f |", person_average[i]);
        printf("\n");
    }
    printf("---------------------------------------------------------\n");
    printf("| 平均 |");
    for (j=0; j<5; j++) {
        printf(" %3.1f |", kamoku_average[j]);
    }
    printf("             |\n");
    printf("| 最低 |");
    for (j=0; j<5; j++) {
        printf("  %3d |", min[j]);
    }
    printf("             |\n");
    printf("| 最大 |");
    for (j=0; j<5; j++) {
        printf("  %3d |", max[j]);
    }
    printf("             |\n");
    printf("---------------------------------------------------------\n");
}
```
## 解説

- データ分析の基本（表計算）を C でやってみるもの
- 表示するためのデータと表示に分けている（処理が独立するのでこの方が良い）
- i, j が何を表すか全体的に統一している（i は人，jは科目）
- int と float の型変換に注意
- 合計があれば平均の計算は簡単
- 科目平均は合計を tmp で一時的に記録
- max/min 処理はこれまでの max/min を tmp に入れて，それと比較してより大きい／小さい場合に tmp を更新（典型的な処理）
- 最初に与える最大値／最小値は 0 や 100 のように決まっていると簡単．決まっていない場合は最初のデータで代用することがある（以下参照）
```c
    int max[] = {0, 0, 0, 0, 0};
    for (j=0; j<5; j++) {
        max[j] = score[i][0];
        for (i=0; i<5; i++) {
            if (max[j] <= score[i][j]) {
                max[j] = score[i][j];
            }
        }
    }
```
- 最大得点がどの科目かは max 値を求めながら max 値が更新されたら，そのインデックスを記録する典型的な処理パターン．
- 表示は視覚的にデータと捉えるために重要．ある意味でのデータビジュアライゼーションなので，どういった表示がわかりやすいか，見やすいかを考えることが大事．模範解答の表示は以下の感じ．ここでは得意科目に * をつけたが他の表示候補もあり得る
```sh
---------------------------------------------------------
| 名前 | 国語 | 算数 | 理科 | 社会 | 体育 | 合計 | 平均 |
---------------------------------------------------------
|    A | * 54 |   52 |   24 |   13 |   15 |  158 | 31.6 |
|    B |   91 |   19 | * 96 |   96 |   91 |  393 | 78.6 |
|    C |   19 |   69 |   91 | * 96 |   19 |  294 | 58.8 |
|    D |   88 |   19 |   55 |   39 | *100 |  301 | 60.2 |
|    E |   19 |   42 |   43 | * 68 |   19 |  191 | 38.2 |
---------------------------------------------------------
| 平均 | 54.2 | 40.2 | 61.8 | 62.4 | 48.8 |             |
| 最低 |   19 |   19 |   24 |   13 |   15 |             |
| 最大 |   91 |   69 |   96 |   96 |  100 |             |
---------------------------------------------------------
---------------------------------------------------------
| 名前 | 国語 | 算数 | 理科 | 社会 | 体育 | 合計 | 平均 |
---------------------------------------------------------
|    A | * 54 |   52 |   24 |   13 |   15 |  158 | 31.6 |
|    B |   91 |   19 | * 96 | * 96 |   91 |  393 | 78.6 |
|    C |   19 |   69 |   91 | * 96 |   19 |  294 | 58.8 |
|    D |   88 |   19 |   55 |   39 | *100 |  301 | 60.2 |
|    E |   19 |   42 |   43 | * 68 |   19 |  191 | 38.2 |
---------------------------------------------------------
| 平均 | 54.2 | 40.2 | 61.8 | 62.4 | 48.8 |             |
| 最低 |   19 |   19 |   24 |   13 |   15 |             |
| 最大 |   91 |   69 |   96 |   96 |  100 |             |
---------------------------------------------------------
```
- 発展は最大値が複数ある場合の処理．１ループで考えると面倒なので２ループ考える方が楽．１ループ目は最大値の算出，２ループ目は最大値と同じ点数のピックアップ．2 pass のアルゴリズムの簡単なやつ（１ループ目でデータ全体を眺めて，２ループ目で全体を最適にするような詳細な処理をする）．
