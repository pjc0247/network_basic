thread
====

__헤더__
```C++
#include <thread>
```

스레드 생성
----
```C++
void func(){
  printf("hello i am thread\n");
}

std::thread(func);
```
```C++
std::thread(
  [](){
    printf("using lambda\n");
  });
  
```

대기
----
join함수를 이용하면 스레드가 완전히 종료될때까지 대기한다.<br>
```C++
int global = 1;
void func(){
  sleep(1000);
  global += 5;
}

std::thread(func).join();
printf("v : %d\n", global);
```


joinable 메소드를 사용하면 현재 스레드가 join가능한 상태인지 검사할 수 있다.
```C++
std::thread t(func);
if(t.joinable())
  t.join();
```

스레드의 아이디
----
get_id 메소드를 이용해 스레드의 아이디를 가져올 수 있다.<br>
아이디는 서로 다른 스레드를 구분하는데 이용할 수 있다.
```C++
std::thread t(func);
printf("id : %d\n", t.get_id());
```


std::this_thread를 이용하면 현재 스레드에 접근할 수 있다.
```C++
printf("current thread's id is %d\n",
  std::this_thread::get_id());
```

현재 시스템의 코어 수 가져오기
----
std::thread::hardware_concurrency 메소드를 이용하여 현재 시스템에서 동시에 몇개의 스레가 작동할 수 있는 지 알아올 수 있다.

```C++
printf("%d\n",
  std::thread::hardware_concurrency());
```
