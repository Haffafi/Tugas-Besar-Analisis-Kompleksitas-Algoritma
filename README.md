#include <iostream>
#include <chrono>

using namespace std;

long long pangkatIterasi(int a, int b) {
    long long result = 1;
    for (int i = 1; i <= b; i++) {
        result = result * a;
    }
    return result;
}

long long pangkatRekursif(int a, int b) {
    if (b == 0) {
        return 1;
    }

    if (b % 2 == 0) {
        long long result = pangkatRekursif(a, b / 2);
        return result * result;
    }
    else {
        return a * pangkatRekursif(a, b - 1);
    }
}

int main() {
    int a = 2;
    int dataN[] = {10, 20, 30, 40, 50, 100, 1000};
    int jumlahData = 7;
    int ulang = 1000000;

    volatile long long dummy = 0;

    cout << "n,Iteratif_ns,Rekursif_ns\n";

    for (int i = 0; i < jumlahData; i++) {
        int n = dataN[i];

        auto start1 = chrono::high_resolution_clock::now();
        for (int k = 0; k < ulang; k++) {
            dummy += pangkatIterasi(a, n);
        }
        auto end1 = chrono::high_resolution_clock::now();

        auto start2 = chrono::high_resolution_clock::now();
        for (int k = 0; k < ulang; k++) {
            dummy += pangkatRekursif(a, n);
        }
        auto end2 = chrono::high_resolution_clock::now();

        long long tIter = chrono::duration_cast<chrono::nanoseconds>(end1 - start1).count();
        long long tRek  = chrono::duration_cast<chrono::nanoseconds>(end2 - start2).count();

        cout << n << "," << (tIter / ulang) << "," << (tRek / ulang) << "\n";
    }

    return 0;
}
