
1. Разбиваем задачу сортировки массива до **1 элемента**
2. Объединяем решения по парам: 2 элемента в двух элементные, 2 двухэлементные в 4х элементные и так далее
3. Четное разбиение не всегда может выйти - значит можем объединить 1 и 2 элементные, но также по парам.

![[Pasted image 20240921102652.png]]

Алгоритм для массива a \[left, right)
```
void merge(int* a, int l, int mid, int r) {
    int it1 = 0;
    int it2 = 0;

    int* res = new int[r - l];
    while (l + it1 < mid && mid + it2 < r) {
        if (a[l + it1] < a[mid + it2]) {
            res[it1 + it2] = a[l + it1];
            it1++;
        }
        else {
            res[it1 + it2] = a[mid + it2];
            it2++;
        }
    }

    while (l + it1 < mid) {
        res[it1 + it2] = a[l + it1];
        it1++;
    }

    while (mid + it2 < r) {
        res[it1 + it2] = a[mid + it2];
        it2++;
    }

    for (int i = 0; i < it1 + it2; i++) {
        a[l + i] = res[i];
    }

    delete[] res;
}

void mergeSort(int* a, int l, int r) {
    if (l >= r) return;

    int mid = (l + r) / 2;
    mergeSort(a, l, mid);
    mergeSort(a, mid + 1, r);

    merge(a, l, mid + 1, r);
}
```