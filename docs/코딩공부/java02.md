```java
public class AverageCal {
	
	public static void main(String[] args) {
		AverageCal r = new AverageCal();

		int [] intArray = {1,2,3,4,5,6};
		double [] dbArray = {6.0, 4.4, 1.9, 2.9, 3.4, 3.5};
		
		System.out.println(average(intArray));
		System.out.println(r.average(dbArray));
		
	}
	
	public static int average(int [] array) {
		int i = 0;
		int avg = 0;

		for (i=0; i<array.length; i++) {
			avg += array[i];
		}
		return avg/array.length; #이렇게 하면 되지만
	}

	public double average(double [] array) {
		double avg = 0.0;
		int i = 0;
		for (i=0; i<array.length; i++) {
			avg += array[i];
			avg = avg/array.length; #이렇게 하면 return 이 되지 않는다..
		}
		return avg;
	}

	

}
```

왜그러는걸까..!
