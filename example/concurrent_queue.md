concurrent_queue
====
concurrent_queue는 몇몇 메소드에 대해서 원자성이 보장된 큐이다.<br>
* windows 환경에서만 이용 가능

__헤더__
```C++
#include <concurrent_queue.h>
```

기본적인 이용
----
```C++
using namespace concurrency;

concurrent_queue<int> q;

q.push(1);
q.push(2);
q.push(3);

while(!q.empty()){
  int n;
  if(q.try_pop(n))
    printf("%d\n", n);
}
```

원자성이 보장된 메소드
----
- push
- try_pop
- empty

원자성이 보장되지 않은 메소드
----
- unsafe_begin
- unsafe_end
- clear
