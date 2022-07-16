# 자바 함수

## 메서드와 람다 동적파라미터화

### 메서드 참조

<aside>
💡 람다 표현식이 단 하나의 메소드만을 호출하는 경우에 해당 람다 표현식에서 불필요한 매개변수를 제거하고 사용할 수 있도록 해준다.

</aside>

- ::로 메소드를 참조할 수 있다.

```java
File[] hiddenFiles = new File(".").listFiles(new Filefilter(){
	public boolean accept(File file){
		return file.isHidden();
	}
});
```

```java
File[] hiddenFiles = new File(".").listFiles(File::isHidden);
```

### 메서드 전달

```java
public static List<Apple> filterGreenApplis(List<Apple> inventory(){
	List<Apple> result - new ArrayList<>();
	
	for (Apple apple : inventory) {
		if(GREEN.equals(apple.getColor())) {
			result.add(apple);
		}
	}
	return result;
}
```

```java
public static List<Apple> filterHeavyApple(List<Apple> inventory(){
	List<Apple> result - new ArrayList<>();
	
	for (Apple apple : inventory) {
		if(apple.getWeight() > 150) {
			result.add(apple);
		}
	}
	return result;
}
```

**Java 8 이전에는 다음과 같이 비슷한 코드여도 여러개의 함수를 만들어 일부만 변경해서 사용해야 했지만 Java 8 이후로는 메서드를 인수를 넘겨줄 수 있으므로 중복구현할 필요가 없다.**

```java
public static boolean isGreenApple(Apple apple){
	return GREEN.equals(apple.getColor);
}

public static boolean isHeavyApple(Apple apple){
	return apple.getWeight() > 150;
}

public interface Predicate<T>{
	boolean test(T t);
}

static List<Apple> filterApples(List<Apple> inventory, Predicate<Apple> p){
	List<Apple> result = new ArrayList<>();
	for (Apple apple : inventory) {
		if(p.test(apple)){
			result.add(apple);
		}
	}
	return result;
}

public static void main(){
	filterApples(inventory, Apple::isGreenApple);
	filterApples(inventory, Apple::isHeavyApple); 
}
```

### 람다 전달

```java
filterApples(inventory, (Apple a) -> GREEN.equals(a.getColor());
```
