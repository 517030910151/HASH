# HASH
一个规模为100000 * 100000的稀疏矩阵，其中至多10000个位置被赋了值，其余位置上均为零。对矩阵进行以下三种操作：交换两行的值；交换两列的值；询问矩阵当前某个位置上的值
// 1053 Erge's memory
#include<iostream>
#include<stdio.h> 
const int HASH_MAX = 233333;
using namespace std;

struct coordinate {
	int x;
	int y;

	coordinate() {
		x = -1;
		y = -1;
	}
};

coordinate cohash[HASH_MAX];
int valhash[HASH_MAX] = { 0 };

int main() {
	ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
	int xx[100000], yy[100000], i, j, n, m;

	for (i = 0; i <= 99999; i++) xx[i] = yy[i] = i;

	cin >> n;
	//scanf("%d", &n);
	int z;
	unsigned int x, y;
	for (i = 1; i <= n; i++) {
		cin >> x >> y >> z;
		//scanf("%d%d%d", &x, &y, &z);
		int pos = x * y % HASH_MAX;
		while (cohash[pos].x != -1) pos = (pos + 1) % HASH_MAX;
		cohash[pos].x = x;
		cohash[pos].y = y;
		valhash[pos] = z;
	}

	cin >> m;
	for (i = 1; i <= m; i++) {
		cin >> j >> x >> y;
		//scanf("%d%d%d", &j, &x, &y);
		int tmp, pos;
		switch (j) {
		case 0:
			// Exchange Row x with Row y
			tmp = xx[x];
			xx[x] = xx[y];
			xx[y] = tmp;
			break;
		case 1:
			// Exchange Column x with Column y
			tmp = yy[x];
			yy[x] = yy[y];
			yy[y] = tmp;
			break;
		case 2:
			// Find value in position (x, y)
			x = xx[x];
			y = yy[y];
			pos = x * y % HASH_MAX;
			while (!(cohash[pos].x == x && cohash[pos].y == y) && cohash[pos].x != -1)
				pos = (pos + 1) % HASH_MAX;
			if (cohash[pos].x == -1) cout << 0 << '\n';
			//printf("0\n");
			else
				cout << valhash[pos] << '\n';
				//printf("%d\n", valhash[pos]);
			break;
		}
	}

	return 0;
}
