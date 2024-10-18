
#include <iostream>
using namespace std;

//1.Dept 클래스의 모든 멤버 함수를 구현하여 프로그램을 완성

class Dept {
    int size;        // scores 배열의 크기
    int* scores;     // 동적 할당 받을 정수 배열의 주소
public:
    Dept(int size) {  // 생성자
        this->size = size;
        scores = new int[size];
    }

    // 복사 생성자 구현
    Dept(const Dept& dept) {
        size = dept.size;
        scores = new int[size];
        for (int i = 0; i < size; i++) {
            scores[i] = dept.scores[i];
        }
    }

    ~Dept() {  // 소멸자
        delete[] scores;
    }

    int getSize() { return size; }

    void read() {  // size 만큼 키보드에서 정수를 읽어 scores 배열에 저장
        cout << size << "개 점수 입력>> ";
        for (int i = 0; i < size; i++) {
            cin >> scores[i];
        }
    }

    bool isOver60(int index) {  // index의 학생 성적이 60 이상인지 확인
        return scores[index] > 60;
    }
};

// 60점 이상으로 통과하는 학생 수를 리턴하는 함수
int countPass(Dept dept) {
    int count = 0;
    for (int i = 0; i < dept.getSize(); i++) {
        if (dept.isOver60(i)) count++;
    }
    return count;
}

int main() {
    Dept com(10); // 총 10명이 있는 학과 com
    com.read();   // 총 10명의 학생들의 성적을 키보드로부터 읽어 scores 배열에 저장
    int n = countPass(com); // 60점 이상으로 통과한 학생 수를 계산
    cout << "60점 이상은 " << n << "명" << endl;
    return 0;
}

/*
//2. 복사 생성자 제거 및 코드 수정
#include <iostream>
using namespace std;

class Dept {
    int size;        // scores 배열의 크기
    int* scores;     // 동적 할당 받을 정수 배열의 주소
public:
    Dept(int size) {  // 생성자
        this->size = size;
        scores = new int[size];
    }

    ~Dept() {  // 소멸자
        delete[] scores;
    }

    int getSize() const {  // const 함수로 수정
        return size;
    }

    void read() {  // size 만큼 키보드에서 정수를 읽어 scores 배열에 저장
        cout << size << "개 점수 입력>> ";
        for (int i = 0; i < size; i++) {
            cin >> scores[i];
        }
    }

    bool isOver60(int index) const {  // const 함수로 수정
        return scores[index] > 60;
    }
};

// countPass 함수의 매개변수를 참조로 전달하고, const로 수정
int countPass(const Dept& dept) {
    int count = 0;
    for (int i = 0; i < dept.getSize(); i++) {
        if (dept.isOver60(i)) count++;
    }
    return count;
}

int main() {
    Dept com(10); // 총 10명이 있는 학과 com
    com.read();   // 총 10명의 학생들의 성적을 키보드로부터 읽어 scores 배열에 저장
    int n = countPass(com); // 60점 이상으로 통과한 학생 수를 계산
    cout << "60점 이상은 " << n << "명" << endl;
    return 0;
}
*/
