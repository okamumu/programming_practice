## Example 1

文字列のASCIIコードを表示するプログラム

### プログラム
```c
#include <stdio.h>

int main() {
    int i;
    char s[] = "Hello";

    printf("文字列 %s のASCIIコード\n", s);
    i = 0;
    while (s[i] != '\0') {
        printf("%d ", s[i]);
        i++;
    }
    printf("\n");
}
```

### 実行結果

```sh
文字列 Hello のASCIIコード
 72 101 108 108 111 
```

### 解説

- %s による表示
- char 型が数値であることの理解
- %c, %d の違いを理解
- ヌル文字が終端に入っていることを理解
- ヌル文字までのwhileループ（基本書式）

## Example 2

配列 s1 に格納されている文字列を配列 s2 にコピーするプログラム（最大10文字）

### プログラム
```c
#include <stdio.h>

int main() {
    int i;
    char s1[] = "Hello1234567890";
    char s2[11];

    i = 0;
    while (s1[i] != '\0' && i <= 9) { // i <= 9 の条件は配列の添え字を超えないようにするため
        s2[i] = s1[i];
        i++;
    }
    s2[i] = '\0';

    printf("コピー元 %s\n", s1);
    printf("コピー先 %s\n", s2);
}
```

### 実行結果

```sh
コピー元 Hello1234567890
コピー先 Hello1234
```

### 解説

- ヌル文字が終端に入っていることを理解
- ヌル文字までのwhileループ（基本書式）
- 二つの配列を操作
- 大きさの違う配列を扱う際の考慮

## Example 3

配列 s1 に格納されている文字列と配列 s2 に格納されている文字列が同じかどうかを判定するプログラム

### プログラム
```c
#include <stdio.h>

int main() {
    int i, flag; // flag は判定用の変数, TRUEだったら1，FALSEだったら0
    char s1[] = "Hello1234567890";
    char s2[] = "Hello";

    i = 0;
    flag = 1; // 予めTRUEを入れておき，１文字でも違ったら0にする
    do { // どちらかの文字列が終端でも比較するので do-while を使う
        if (s1[i] != s2[i]) {
            flag = 0;
            break;
        }
        i++;
    } while (s1[i] != '\0' || s2[i] != '\0');

    if (flag == 1) {
        printf("二つの文字 %s %s は同じです．", s1, s2);
    } else {
        printf("二つの文字 %s %s は違います．", s1, s2);
    }
}
```

### 解説

- ヌル文字が終端に入っていることを理解
- ヌル文字までのwhileループ（基本書式）
- 二つの配列を操作
- 長さの違う文字列を判定するときどうするか？:arrow_right:いろいろな考え方ができる


## Example 4

文字列の配列の作成および表示をするプログラム

### プログラム
```c
#include <stdio.h>

int main() {
    int i;
    char s[6][21] = { // 最大20文字の文字列を6個格納する
        "We",
        "are",
        "students",
        "of",
        "Hiroshima",
        "university"
    };

    for (i=0; i<6; i++) {
        printf("%s ", s[i]); // 呼び出しは1次元配列の形式
    }
    printf("\n");
}
```

### 解説

- 文字列が配列なので二次元配列になる．
- ヌル文字分の大きさを確保
- 文字列特有の初期化形式
- 1次元形式にすることで「配列」を指定

## Exercise 1

Example 4 の文字列の配列で最大の文字数の文字列とその長さを表示するプログラムを作成せよ．

### 実行結果

```sh
最大の文字列は university でその長さは 10 です
```

### 解答例
```c
int main() {
    int i, j;
    int max_len, max_i, len;
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
        len = 0;
        j = 0;
        while (s[i][j] != '\0') {
            len++;
            j++;
        }
        if (len > max_len) {
            max_len = len;
            max_i = i;
        }
    }

    printf("最大の文字列は %s でその長さは %d です\n", s[max_i], max_len);
}
```

### 解説
- 次の段階を追って作る．
    - 各文字列の文字数を数える
    - 最大値をみつける
    - 最大値をとる文字列をみつける


#### 文字数を数える
```c
#include <stdio.h>

int main() {
    int i, k;
    int len[6]; // 文字列の長さを格納する配列
    char s[6][21] = { // 最大20文字の文字列を6個格納する
        "We",
        "are",
        "students",
        "of",
        "Hiroshima",
        "university"
    };

    for (i=0; i<6; i++) {
        // 以下で長さを変数kでカウント
        k = 0;
        while (s[i][k] != '\0') {
            k++;
        }
        len[i] = k; // 配列 len[i] に長さを格納
    }
}
```

#### 最大文字列数をみつける
```c
#include <stdio.h>

int main() {
    int i, k;
    int len[6]; // 文字列の長さを格納する配列
    int maxlen; // 最大の文字列数を格納する配列
    char s[6][21] = { // 最大20文字の文字列を6個格納する
        "We",
        "are",
        "students",
        "of",
        "Hiroshima",
        "university"
    };

    maxlen = 0; // 暫定的に最大値0としておく
    for (i=0; i<6; i++) {
        k = 0;
        while (s[i][k] != '\0') {
            k++;
        }
        len[i] = k;
        // 最大値の更新
        if (len[i] > maxlen) {
            maxlen = len[i];
        }
    }
}
```

#### 最大文字列数になる文字列（何番目の文字列か）をみつける
```c
#include <stdio.h>

int main() {
    int i, k;
    int len[6]; // 文字列の長さを格納する配列
    int maxlen; // 最大の文字列数を格納する配列
    int maxi; // 最大の文字列数となった文字列の番号を格納する配列
    char s[6][21] = { // 最大20文字の文字列を6個格納する
        "We",
        "are",
        "students",
        "of",
        "Hiroshima",
        "university"
    };

    maxlen = 0; // 暫定的に最大値0としておく
    maxi = 0; // 暫定的に0番（一番最初の文字としておく）
    for (i=0; i<6; i++) {
        k = 0;
        while (s[i][k] != '\0') {
            k++;
        }
        len[i] = k;
        // 最大値の更新
        if (len[i] > maxlen) {
            maxi = i;
            maxlen = len[i];
        }
    }
}
```

#### 不要な変数の削除と最後の表示を加える
```c
#include <stdio.h>

int main() {
    int i, k;
    int maxlen; // 最大の文字列数を格納する配列
    int maxi; // 最大の文字列数となった文字列の番号を格納する配列
    char s[6][21] = { // 最大20文字の文字列を6個格納する
        "We",
        "are",
        "students",
        "of",
        "Hiroshima",
        "university"
    };

    maxlen = 0; // 暫定的に最大値0としておく
    maxi = 0; // 暫定的に0番（一番最初の文字としておく）
    for (i=0; i<6; i++) {
        k = 0;
        while (s[i][k] != '\0') {
            k++;
        }
        if (k > maxlen) {
            maxi = i;
            maxlen = k;
        }
    }

    // 表示．．．
}
```