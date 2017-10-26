## ScrollView里嵌套RecyclerView时，在RecyclerView上滑动时出现卡顿（冲突）的现象

>一个界面有一个RecyclerView（GridView型的），外面套了一层ScrollView，通过ScrollView上下滚动，但是在滑动的时候如果是在RecyclerView的内容上滑动，这时会出现滑动卡顿，而如果是在其他内容上滑动时就可以很顺畅的滑下去。

这是RecyclerView和ScrollView的滑动事件冲突引起的，解决办法就是禁止RecyclerView的滑动事件.
```java
LinearLayoutManager linearLayoutManager = new LinearLayoutManager(getActivity(), LinearLayoutManager.VERTICAL, false) {  
        @Override  
        public boolean canScrollVertically() {  
            return false;  
        }  
    };  
recyclerview.setLayoutManager(linearLayoutManager);
recyclerview.setAdapter(tempCommonAdapter);  
```
