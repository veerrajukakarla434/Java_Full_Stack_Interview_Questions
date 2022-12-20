## 2022 Coding Problems

#### 1) Java Code To Create Pyramid and Pattern

* Pattren 1

![image](https://user-images.githubusercontent.com/40323661/199374708-612f3d0c-2f4d-4e54-996d-72e466933f10.png)

```Java
public static void main(String[] args) {
		{
			int row = 5;
			for (int i = 1; i <=row; i++) {
				for (int k = row; k >=i; k--) {
					System.out.print(k);
				}
				System.out.println();
			}
		}
	}
	
O/P : 

54321
5432
543
54
5
	
```

* Pattern 2 -> Program to print **half pyramid** using start (*)
```Java
public static void main(String[] args) {
	    int rows = 5;

	    for (int i = 1; i <= rows; ++i) {
	      for (int j = 1; j <= i; ++j) {
	        System.out.print("* ");
	      }
	      System.out.println();
	    }
	  }
	}
	
O/P:

* 
* * 
* * * 
* * * * 
* * * * * 

* Pattern 3 -> Program to print **half pyramid** using numbers

	public static void main(String[] args) {
	    int rows = 5;

	    for (int i = 1; i <= rows; ++i) {
	      for (int j = 1; j <= i; ++j) {
	        System.out.print(j +" ");
	      }
	      System.out.println();
	    }
	  }
	}
	
O/P:

1 
1 2 
1 2 3 
1 2 3 4 
1 2 3 4 5 

* Pattern 4 -> Program to print half pyramid using alphabets



```



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
