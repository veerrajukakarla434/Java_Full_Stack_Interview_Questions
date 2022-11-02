## 2022 Coding Problems

#### 1) Java Code To Create Pyramid and Pattern

* Pattren 1

![image](https://user-images.githubusercontent.com/40323661/199374708-612f3d0c-2f4d-4e54-996d-72e466933f10.png)





#### 1) Java Program to Find Largest Prime Factor of an Integer
* Read more: https://javarevisited.blogspot.com/2015/03/how-to-find-largest-prime-factor-of.html#ixzz7iYOFyR7S

```Java
public class PrimeDivison {

	public static void main(String[] args) {
		System.out.printf("Largest prime factor of number '%d' is %d %n", 5, largestPrimeFactor(20));

	}
	

	/** * @return largest prime factor of a number */
	public static int largestPrimeFactor(long number) {
		int i;
		long copyOfInput = number;
		for (i = 2; i <= copyOfInput; i++) {
			if (copyOfInput % i == 0) {
				copyOfInput = copyOfInput/i;
				i--;
			}
		}
		return i;
	}

}
```
