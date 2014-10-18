mutex
----

뮤텍스는 지정한 코드 범위에 동시에 하나의 스레드만 접근할 수 있도록 해준다.

__헤더__
```C++
#include <mutex>
```


뮤텍스의 이용
```C++
std::mutex m;

m.lock();
  // 이 영역에는 동시에 하나의 스레드만 접근이 가능.
m.unlock();
```
```C++
int global = 0;
std::mutex m;

void func(){
  for(int i=0;i<1000;i++){
    m.lock();
      global ++;
    m.unlock();
  }
}

for(int i=0;i<4;i++){
  std::thread(func);
}
```


락 가드의 이용
----
락 가드는 생성 시에 뮤텍스를 잠그고, 소멸 시에 뮤텍스를 잠금 해제한다.

```C++
int global = 0;
std::mutex m;

void func(){
  std::lock_gaurd<std::mutex> g(m);
  global ++;
} //스코프를 벗어난 g는 자동으로 락이 해제된다.
```