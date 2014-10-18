atomic
====
아토믹은 원자성이 보장되는 변수이다.<br>

__헤더__
```C++
#include <atomic>
```

아토믹 변수의 이용
----
```C++
std::atomic<int> n = 0;
std::atomic<char> c = 'a';
```
```C++
std::atomic<int> global = 0;

void func(){
  for(int i=0;i<1000;i++)
    global ++;
}

for(int i=0;i<4;i++)
  std::thread(func);
```

compare_and_exchange
----
값 비교 후 교환 연산을 수행한다.

```C++
std::atomic<int> n = 10;
int old_value = 5;
int new_value = 15;

/* n의 값이 old_value와 같다면 n의 값을 new_value로 치환한다. */
/* 치환했을 경우 true를 리턴한다. */
/* old_value와 다를 경우에는 바꾸지 않고 false를 리턴한다. */

/* n은 10인데 old_value는 5이기 때문에 교환은 일어나지 않고 false리턴 */
printf("%d\n",
  n.compare_and_exchange_weak(old_value, new_value));
  
/* 일치하기 때문에 n의 값을 new_value로 치환 */
old_value = 10;
printf("%d\n",
  n.compare_and_exchange_weak(old_value, new_value));
```
