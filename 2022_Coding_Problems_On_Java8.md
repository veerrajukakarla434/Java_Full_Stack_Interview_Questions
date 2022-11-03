# Java8 Coding Problems Using Java8 features

* Employee Object and EmployeeDemo classess  with All Problems

```Java
public class Employee {

	    private int id;
	    private String name;
	    private int age;
	    private String city;
	    private String gender;
	    private String department;
	    private int yearOfJoining;
	    private double salary;
	    
		public Employee(int id, String name, int age, String city, String gender, String department, int yearOfJoining,
				double salary) {
			super();
			this.id = id;
			this.name = name;
			this.age = age;
			this.city = city;
			this.gender = gender;
			this.department = department;
			this.yearOfJoining = yearOfJoining;
			this.salary = salary;
		}
    
    ------ setters and getters
    }

   public static void main(String[] args) {
		
		List<Employee> el = new ArrayList<Employee>();
        
		el.add(new Employee(11, "Veerraju", 36, "HYD", "Male", "IT-Dev", 2011, 100000.0));
		el.add(new Employee(12, "Paul", 25, "HYD", "Male", "Sales And Marketing", 2015, 13500.0));
		el.add(new Employee(133, "Suresh", 29, "HYD", "Male", "Infrastructure", 2012, 18000.0));
		el.add(new Employee(144, "Murali ", 28, "Bangalore", "Male", "Product Development", 2014, 32500.0));
		el.add(new Employee(155, "Nima", 27, "Bangalore", "Female", "HR", 2013, 22700.0));
		el.add(new Employee(166, "Iqbal", 43, "Bangalore", "Male", "Security And Transport", 2016, 10500.0));
		el.add(new Employee(177, "Manu", 35, "Bangalore", "Male", "Account And Finance", 2010, 27000.0));
		el.add(new Employee(188, "Rabin ", 31, "Bangalore", "Male", "Product Development", 2015, 34500.0));
		el.add(new Employee(199, "Radha", 24, "Bangalore", "Female", "Sales And Marketing", 2016, 11500.0));
		el.add(new Employee(200, "Praveen", 38, "Bangalore", "Male", "Security And Transport", 2015, 11000.5));
		el.add(new Employee(211, "Lakshmi", 27, "HYD", "Female", "Infrastructure", 2014, 15700.0));
		el.add(new Employee(222, "Nitin ", 25, "Bangalore", "Male", "Product Development", 2016, 28200.0));
		el.add(new Employee(233, "Jyothi ", 27, "HYD", "Female", "Account And Finance", 2013, 21300.0));
		el.add(new Employee(244, "Nicolus", 24, "Bangalore", "Male", "Sales And Marketing", 2017, 10700.5));
		el.add(new Employee(255, "Ali", 23, "HYD", "Male", "Infrastructure", 2018, 12700.0));
		el.add(new Employee(266, "Sanvi ", 26, "Bangalore", "Female", "Product Development", 2015, 28900.0));
		el.add(new Employee(277, "Anji", 31, "Bangalore", "Male", "Product Development", 2012, 35700.0));

    // 1) getting employee names whose age is >25  using streams with for each
		el.stream().filter(e->e.getAge()>35).map(Employee::getName).forEach(System.out::println);

    // out put:
    
      Veerraju
      Iqbal
      Praveen
     
    // 2) getting in list<String>  ->  getting names whose age is >25  using streams and collecting /returning list
		
		List<String> elist = el.stream().filter(e->e.getAge()>35).map(Employee::getName).collect(Collectors.toList());
		System.out.println(elist);

     // out put:
     [Veerraju, Iqbal, Praveen]
     
     // 2) Increase salary whose salary <25000 or age is >35  increment by 3%  here will print only salary
		
		List<Double> elist2 = el.stream().filter(i -> i.getAge() >35).map(i -> i.getSalary() + i.getSalary() *3 / 100).collect(Collectors.toList());
		System.out.println(elist2);
    
    // out put:
    [103000.0, 10815.0, 11330.515]



```
