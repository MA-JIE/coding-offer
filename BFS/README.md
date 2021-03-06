# STL: queue
front()：返回 queue 中第一个元素的引用。如果 queue 是常量，就返回一个常引用；如果 queue 为空，返回值是未定义的。<br>
back()：返回 queue 中最后一个元素的引用。如果 queue 是常量，就返回一个常引用；如果 queue 为空，返回值是未定义的。<br>
push(const T& obj)：在 queue 的尾部添加一个元素的副本。这是通过调用底层容器的成员函数 push_back() 来完成的。<br>
push(T&& obj)：以移动的方式在 queue 的尾部添加元素。这是通过调用底层容器的具有右值引用参数的成员函数 push_back() 来完成的。<br>
pop()：删除 queue 中的第一个元素。<br>
size()：返回 queue 中元素的个数。<br>
empty()：如果 queue 中没有元素的话，返回 true。<br>
emplace()：用传给 emplace() 的参数调用 T 的构造函数，在 queue 的尾部生成对象。<br>
swap(queue<T> &other_q)：将当前 queue 中的元素和参数 queue 中的元素交换。它们需要包含相同类型的元素。也可以调用全局函数模板 swap() 来完成同样的操作。<br>
![queue](https://github.com/MA-JIE/coding-offer/blob/master/BFS/img/queue.png)

# STL: deque
void push_front(const T& x):双端队列头部增加一个元素X <br>
void push_back(const T& x):双端队列尾部增加一个元素x  <br>
void pop_front():删除双端队列中最前一个元素 <br>
void pop_back():删除双端队列中最后一个元素 <br>
