# 前缀和

## 一维前缀和

```cpp
// 前缀和数组
s[i] = a[0] + a[1] + a[2] + ... + a[i];

// 初始化前缀和数组
s[0] = 0;
for (int i = 0; i < n; i++) s[i + 1] = s[i] + a[i];

// 区间求和 [l...r]
s[l...r] = s[r] - s[l - 1];
```

## 二维前缀和

```cpp
// 二维数组 a[1...n][1...m]
// s[i, j] = 第i行j列格子左上部分所有元素的和
for (int i = 1; i <= n; i++)
  for (int j = 1; j <= m; j++)
    s[i][j] = s[i - 1][j] + s[i][j - 1] - s[i - 1][j - 1] + a[i][j];

// 以(x1, y1)为左上角，(x2, y2)为右下角的子矩阵的和为：
s[x2][y2] - s[x2][y1 - 1] - s[x1 - 1][y2] + s[x1 - 1][y1 - 1];
```