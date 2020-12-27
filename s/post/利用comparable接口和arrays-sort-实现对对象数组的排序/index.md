RT
<!--more-->
```java
class TV implements Comparable{

	int StartTime;
	int EndTime;
	
	public TV(int s,int e){
		this.StartTime = s;
		this.EndTime = e;
	}
 
	@Override
	public int compareTo(Object o) {
		// TODO Auto-generated method stub
		TV tv = (TV)o;
		return (EndTime > tv.EndTime)?1:-1;
	}
 
}
```
然后↓即可按照电视节目的结束时间对电视节目完成升序排序
```java
TV tvs[] = new TV[n];
Arrays.sort(tvs);
```
超方便！
不过直接写个冒泡排一下也不是不行哈哈哈
但是这个好玩_(:3」∠)_

#但是这个只可以按照一种方式排序噢 如果想要按照多种方式排序就要用Comparator啦