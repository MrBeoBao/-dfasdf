#include <iostream>
using namespace std;
#include <cmath>
#include<vector>
#include<algorithm>
void nhapDSDiem(int hang, int cot, int mang2D[50][50]) {
    for (int h = 0; h < hang; h++) {
    	cout<<"- Phan tu hang["<< h<< "]: ";
        for (int c = 0; c < cot; c++){
        	cin>> mang2D[h][c];
        }
    }
}
void hienThiMang(int hang, int cot, int mang2D[50][50]) {
        for(int i = 0; i < hang; i++) {
        for(int j = 0; j < cot; j++) {
            cout << mang2D[i][j];
            if(j < cot - 1) cout.width(5);
        }
        cout << endl;
    }
}
void sapXepMang(int hang, int cot, int mang2D[50][50]) {
    vector<int> vec;
    for (int i = 0; i < hang; i++) {
        for (int j = 0; j < cot; j++) {
            vec.push_back(mang2D[i][j]); // chuyen mang 2 chieu ve thanh vector 1 chieu
        }
    }
    sort(vec.begin(), vec.end(), less<int>()); // sap xep vector theo thu tu tang dan

    int top = 0; int bottom = hang - 1; int left = 0; int right = cot - 1;
    int index = 0;

    while (top <= bottom && left <= right)
    {
        //chay tu trai sang phai
        for (int i = left; i <= right; i++) {
            mang2D[top][i] = vec[index++];
        }
        top++;

        //chay tu tren xuong duoi
        for (int i = top; i <= bottom; i++) {
            mang2D[i][right] = vec[index++];
        }
        right--;

        //chay tu phai sang trai
        for (int i = right; i >= left; i--) {
            mang2D[bottom][i] = vec[index++];
        }
        bottom--;

        //chay tu duoi len tren
        for (int i = bottom; i >= top; i--) {
            mang2D[i][left] = vec[index++];
        }
        left++;
    }
}
int main() {
    int n;
    cout << "Nhap so phan tu cua hang va cot: ";
    cin >> n;
    const int hang = n, cot = n;
    int mang2D[50][50];
    nhapDSDiem(hang, cot, mang2D);
    cout <<"-> Mang "<<n<<"x"<<n<<" gom:"<<endl;
    hienThiMang(hang, cot, mang2D);
    sapXepMang(hang, cot, mang2D);
    cout<<"-> Mang sau khi sap xep gom:" <<endl;
    hienThiMang(hang, cot, mang2D);
    return 0;
}
 
