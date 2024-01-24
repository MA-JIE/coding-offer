``` cpp
#include <iostream>

class Array {
private:
    int* data; // 指向动态分配的数组的指针
    int size; // 数组的大小

public:
    // 构造函数
    Array(int size) {
        this->size = size;
        data = new int[size];
    }

    // 拷贝构造函数
    Array(const Array& other) {
        size = other.size;
        data = new int[size];
        for (int i = 0; i < size; i++) {
            data[i] = other.data[i];
        }
    }

    // 深拷贝复制操作符
    Array& operator=(const Array& other) {
        if (this != &other) {
            delete[] data;
            size = other.size;
            data = new int[size];
            for (int i = 0; i < size; i++) {
                data[i] = other.data[i];
            }
        }
        return *this;
    }

    // 析构函数
    ~Array() {
        delete[] data;
    }

    // 获取数组大小
    int getSize() {
        return size;
    }

    // 获取指定位置的元素
    int get(int index) {
        if (index >= 0 && index < size) {
            return data[index];
        } else {
            std::cout << "Index out of range!" << std::endl;
            return -1;
        }
    }

    // 设置指定位置的元素
    void set(int index, int value) {
        if (index >= 0 && index < size) {
            data[index] = value;
        } else {
            std::cout << "Index out of range!" << std::endl;
        }
    }
};

int main() {
    Array arr1(5); // 创建一个大小为5的数组

    // 设置数组元素的值
    for (int i = 0; i < arr1.getSize(); i++) {
        arr1.set(i, i + 1);
    }

    // 使用拷贝构造函数创建一个新的数组
    Array arr2(arr1);

    // 使用深拷贝复制操作符将arr1的值复制给arr3
    Array arr3 = arr1;

    // 修改arr1的值
    arr1.set(0, 100);

    // 输出arr2和arr3的值
    std::cout << "arr2: ";
    for (int i = 0; i < arr2.getSize(); i++) {
        std::cout << arr2.get(i) << " ";
    }
    std::cout << std::endl;

    std::cout << "arr3: ";
    for (int i = 0; i < arr3.getSize(); i++) {
        std::cout << arr3.get(i) << " ";
    }
    std::cout << std::endl;

    return 0;
}

```
