#include <iostream>

using namespace std;

int pangkatIterasi(int a,int b){
    int result = 1;
    for(int i = 1; i <= b; i++){
        result = result * a;
    }
    return result;
}

int pangkatRekusif(int a,int b){
    if (b == 0){
        return 1;
    }
    if (b % 2 == 0){
        int result = pangkatRekusif(a, b / 2);
        return result * result;
    } else {
        return a * pangkatRekusif(a,b - 1);
    }
}

int main()
{
    int a, b;
    cin >> a;
    cin >> b;
    cout << pangkatIterasi(a,b) << endl;
    cout << pangkatRekusif(a,b) << endl;
}
