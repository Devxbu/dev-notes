[Abdul Bari's Solution][https://www.youtube.com/watch?v=sSno9rV8Rhg]

In this question we are given two strings, needle, the shorter one, and haystack, the longer one, in which we search for letters, but what we need to look for when doing this search is that the letters will be in the same order as in needle (there may be characters between them). For example

haystack: a - b - c - d - e - f - g - g - h - i - j
needle: c - d - g - i  

The sequel could be c d g i because in the haystack these letters are given in the same order as the needle, but things will change when we add the letter e to the beginning of the needle.

haystack: a - b - c - d - e - f - g - h - h - i - j
needle: e - c - d - g - i

This time, since the letters c and d come after the letter e in the haystack, we cannot add them, so the sequel will be e g i

## Solution With Recursion

```c
char needle[2] = {'b', 'd'};
char haystack[4] = {'a', 'b', 'c', 'd'};

int lcs(i, j){
	if (needle[i] == '/0' || haystack[j] == '/0') {
		return 0;
	} else if (needle[i] == haystack[j]){
		return 1 + lcs(i + 1, j + 1);
	} else {
		return max(lcs(i + 1, j), lcs(i, j + 1));
	}
}
```

The steps of the code will be as follows

	  a[0] b[0] -> b, a = 2
		a[1] b[0] -> d, a = 1
			a[1] b[1] -> d, b = 0
				a[1] b[2] -> d, c = 0
					a[1] b[3] -> d, d  = 1
						a[2] b[4] -> \0, \0 = 0
					a[2] b[2] - > \0, c = 0
				a[2] b[1] -> \0, b = 0
			a[2] b[0] -> \0, a = 0
		a[0] b[1] -> b, b = 1 + 1
			a[1] b[2] -> d, c = 0
				a[2] b[2] -> \0, c = 0
			a[1] b[3] -> d, d = 1
				a[2]  b[4] -> \0, \0 

This kind of progress will cost us 2 ^ n time complexity. If we store the traveled elements somewhere, we reduce this time complexity to n * m (n = needle, m = haystack). As can be seen in the example, both cocci started to do similar things at some point

## Solution With DP

The weak point of a recursive solution is that it solves the same subproblems over and over again. But in DP, we write these subproblems in a table and have them ready if we need them again later.

```c
#include <stdio.h>
#include <string.h>

// İki sayıdan büyük olanı döndüren fonksiyon
int max(int a, int b) {
    return (a > b) ? a : b;
}

// LCS (Longest Common Subsequence) hesaplayan fonksiyon
int lcs(char* needle, char* haystack) {
    int n = strlen(needle);    // needle uzunluğu
    int m = strlen(haystack); // haystack uzunluğu

    int dp[n + 1][m + 1]; // DP tablosu tanımlanıyor: dp[i][j] -> needle[i:] & haystack[j:] karşılaştırması

    // Başta tüm tabloyu sıfıra eşitle (alt problemler için başlangıç değeri)
    for (int i = 0; i <= n; i++) {
        for (int j = 0; j <= m; j++) {
            dp[i][j] = 0;
        }
    }

    // Tabloyu tersten (bottom-up) dolduruyoruz
    for (int i = n - 1; i >= 0; i--) {
        for (int j = m - 1; j >= 0; j--) {
            if (needle[i] == haystack[j]) {
                // Eğer harfler eşleşiyorsa, bu harfi eşleştir ve sonraki ikiliye geç
                dp[i][j] = 1 + dp[i + 1][j + 1];
            } else {
                // Eşleşmiyorsa, haystack'teki karakteri atla (i sabit, j ileri)
                dp[i][j] = dp[i][j + 1];
            }
        }
    }

    // En baştan başlayarak, needle'ın haystack içinde kaç karakterle sırayla eşleştiğini döndür
    return dp[0][0];
}

```

What We Did Step by Step:

We created the dp[i][j] table, which shows how many letters can match the subarrays needle[i:] and haystack[j:].
If needle[i] == haystack[j], then we matched that letter and moved to the next character in both arrays.
If there was no match, we skipped the character in haystack but kept looking for a match with the same character in needle.
We did this for all characters and got the result as dp[0][0].