# 関数（function）

- C言語で一連の手続きをまとめたもの
- 何回も使うものをまとめる
- 普通は入力と出力がある
- 入力・出力がないものは「手続き」（procedure）とも呼ばれる

## 用語

- 呼び出し：関数を利用すること
- （実）引数：関数を呼び出す際に入力として関数に渡す変数
- 仮引数：関数内の処理で外部から渡される変数
- 戻り値：関数が返す値
- 引数の型：実・仮引数の型（int, float, etc.）
- 戻り値の型：戻り値の型（int, float, etc.）
- 関数名：関数定義・呼び出しの際に使う名前

## 書式

```c

// 関数定義：使う前に定義しておく
int f(int x) {
    int y; 
    // 関数の内部処理
    return y;
}


int main() {
    int z;
    z = f(9); // 関数の呼び出し
}
```

- 定義の時の基本的な書式
```c
戻り値の型 関数名(引数の型 仮引数, 引数の型 仮引数) {
    // 関数の内部処理（関数本体）
    return 戻り値;
}
```

## Example 1（関数定義と呼び出し）

変数 x, y, z の2乗を計算するプログラム
```c
#include <stdio.h>

int main() {
    int x = 5;
    int y = 10;
    int z = 12;

    printf("x^2=%d\n", x*x);
    printf("y^2=%d\n", y*y);
    printf("z^2=%d\n", z*z);
}
```

関数を使う
```c
#include <stdio.h>

// 与えられた数値 x の2乗を計算してその値を返す関数
int pow2(int x) {
    return x*x;
}

int main() {
    int x = 5;
    int y = 10;
    int z = 12;

    printf("x^2=%d\n", pow2(x));
    printf("y^2=%d\n", pow2(y));
    printf("z^2=%d\n", pow2(z));
}
```

### 実行結果
```sh
x^2=25
y^2=100
z^2=144
```

### 解説

- 関数の定義の仕方
- 関数の呼び出し方
- 関数がいつ実行されるか
- 引数の型・戻り値の型
- 仮引数の仕組み：どんな変数が与えられても渡された値は関数内で変数xとして扱える
- return の書き方

## Example 2（複数引数）

5^5, 10^3, 12^4 を計算せよ．

#### 関数を使わないバージョン
```c
#include <stdio.h>

int main() {
    double x = 5.0;
    double y = 10.0;
    double z = 12.0;
    double tmp;
    int i;

    // x を 5 回かける
    tmp = 1.0;
    for (i=0; i<5; i++) {
        tmp *= x;
    }
    printf("x^5=%f\n", tmp);

    // y を 3 回かける
    tmp = 1.0;
    for (i=0; i<3; i++) {
        tmp *= y;
    }
    printf("y^3=%f\n", tmp);

    // z を 4 回かける
    tmp = 1.0;
    for (i=0; i<4; i++) {
        tmp *= z;
    }
    printf("z^4=%f\n", tmp);
}
```

### $x$ の $n$ 乗を計算する関数を作成
```c
#include <stdio.h>

double pown(double x, int n) {
    int i;
    double tmp = 1.0;
    for (i=0; i<n; i++) {
        tmp *= x;
    }
    return tmp;
}

int main() {
    double x = 5.0;
    double y = 10.0;
    double z = 12.0;

    printf("x^5=%f\n", pown(x, 5));
    printf("y^3=%f\n", pown(y, 3));
    printf("z^4=%f\n", pown(z, 4));
}
```

### 実行結果
```sh
x^5=3125.000000
y^3=1000.000000
z^4=20736.000000
```

### 解説

- 複数の引数はカンマで区切ってならべる
- 引数の型を変えてもOK
- 複数戻り値は不可能

## Example 3（値を返さない関数・引数を取らない関数）

- 値を取らない関数：括弧だけで定義
- void: 値を返さない場合に利用

配列を表示する関数を定義
```c
#include <stdio.h>

void print_message() {
    printf("いまから配列を表示します：");
    return;
}

void print_array(int n, int a[]) {
    int i;
    print_message();
    for (i=0; i<n; i++) {
        printf("%d ", a[i]);
    }
    printf("\n");
    return;
}

int main() {
    int x[] = {10, 3, 5, 6, 1, 4};
    int y[] = {61, 1, 11, 59, 1, 60, 19, 19};
    print_array(6, x);
    print_array(8, y);
}
```

### 実行結果

```sh
いまから配列を表示します：10 3 5 6 1 4 
いまから配列を表示します：61 1 11 59 1 60 19 19 
```

## Example 4（変数の有効範囲（スコープ））

- 次回以降．．

## Exercise 1

- 文字列を表示する関数 print_string を作成せよ．ただし printf の書式として %c のみを使うようにせよ．

```c
#include <stdio.h>

void print_string(char s[]) {
    // ここにプログラムを実装
}

int main() {
    int i;
    char s[6][21] = {
        "We",
        "are",
        "students",
        "of",
        "Hiroshima",
        "university"
    };

    for (i=0; i<6; i++) {
        print_string(s[i]);
        printf(" ");
    }
    printf("\n");
}
```

<!--
### 解答例
```c
#include <stdio.h>

void print_string(char s[]) {
    int i = 0;
    while (s[i] != '\0') {
        printf("%c", s[i]);
        i++;
    }
}

int main() {
    int i;
    char s[6][21] = {
        "We",
        "are",
        "students",
        "of",
        "Hiroshima",
        "university"
    };

    for (i=0; i<6; i++) {
        print_string(s[i]);
        printf(" ");
    }
    printf("\n");
}
```
-->

## Exercise 2

- 文字列の数を数える関数 length を作成せよ．

```c
#include <stdio.h>

void print_string(char s[]) {
    // ここにプログラムを実装
}

int length(char s[]) {
    // ここにプログラムを実装
}

int main() {
    int i;
    char s[6][21] = {
        "We",
        "are",
        "students",
        "of",
        "Hiroshima",
        "university"
    };

    for (i=0; i<6; i++) {
        print_string(s[i]);
        printf("の長さは%dです", length(s[i]));
    }
    printf("\n");
}
```

<!--
### 解答例
```c
#include <stdio.h>

void print_string(char s[]) {
    int i = 0;
    while (s[i] != '\0') {
        printf("%c", s[i]);
        i++;
    }
}

int length(char s[]) {
    int i = 0;
    while (s[i] != '\0') {
        i++;
    }
    return i;
}

int main() {
    int i;
    char s[6][21] = {
        "We",
        "are",
        "students",
        "of",
        "Hiroshima",
        "university"
    };

    for (i=0; i<6; i++) {
        print_string(s[i]);
        printf("の長さは%dです\n", length(s[i]));
    }
    printf("\n");
}
```
-->

## Exercise 3

- lesson02 の Exercise 1 を Exercise 2 で作った関数 length を用いて書き換えよ．

<!--
### 解答例
```c
#include <stdio.h>

int length(char s[]) {
    int i = 0;
    while (s[i] != '\0') {
        i++;
    }
    return i;
}

int main() {
    int i;
    int max_len, max_i;
    char s[6][21] = { // 最大20文字の文字列を6個格納する
        "We",
        "are",
        "students",
        "of",
        "Hiroshima",
        "university"
    };

    max_len = 0;
    max_i = 0;
    for (i=0; i<6; i++) {
        if (length(s[i]) > max_len) {
            max_len = length(s[i]);
            max_i = i;
        }
    }
    printf("最大の文字列は %s でその長さは %d です\n", s[max_i], max_len);
}
```
-->
