```Java
public static List<Student> filterStudents(List<Student> students, StudentPredicate sp, StudentFunction sf, StudentConsumer sc) {
    List<Student> result = new ArrayList<>();
    for (Student s : students) {
        if (sp.test(s)) {
            String str = sf.apply(s);
            sc.accept(str);
            result.add(s);
        }
    }
    return result;
}

public static void main(String[] args) {
    List<Student> result = filterStudents(students,
            s -> s.getAverage() >= 26 && s.getAverage() <= 30,
            s -> String.format("%s_%s_%f", s.getLastname(), s.getName(), s.getAverage()),
            s -> System.out.println(s));
}

```
```Java
public static <T extends Measurable> double average(List<T> objects) {
    // ...
}
//oppure
public static double average(List<? extends Measurable> objects) {
    // ...
}
```
```Java
// singolo limite di tipo
<T extends A>
// limite di tipo multiplo
<T extends A & B & C & ...>
//! Il primo tipo vincolato ("A") può essere una classe o un'interfaccia.
//Il resto dei tipi vincolati (da "B" in poi) devono essere interfacce.
```
```Java
public class Pencil implements DrawingTool {
    @Override
    public String draw(Curve curve) {
        return "Pencil drawing a " + curve.draw();
    }
}
public class Brush implements DrawingTool {
    @Override
    public String draw(Curve curve) {
        return "Brush drawing a " + curve.draw();
    }
}
public class DrawingApp {
    public static void main(String[] args) {
        Curve curve = new Curve();
        DrawingTool[] drawingTools = new DrawingTool[]{new Pencil(), new Brush()};
        for (DrawingTool tool : drawingTools) {
            System.out.println(tool.draw(curve));
        }
    }
}
```
```Java
class A { }

interface B { }
interface C { }

class D extends A implements B, C { }
interface E extends B, C { }

```
```Java
public class Cat {

    private String name;

    public Cat(String name) {
        this.name = name;
    }

    public class Bow {  //inner class
        String color;

        public Bow(String color) {
            this.color = color;
        }

        public void printColor() {
            System.out.println("Cat " + Cat.this.name + " has a " + this.color + " bow.");
        }
    }
}

```
```Java
/*--> INZIALIZZAZIONE DI LIST INTERFACE*/
/* plain, simple, long */
List<Integer> l = new ArrayList<>();
l.add(14);
l.add(73);
l.add(18);

/* more compact version (mutable) */
List <Integer> l = new ArrayList<>(Arrays.asList(14, 73, 18));
List <Integer> l = new ArrayList<>(List.of(14, 73, 18));

List <Integer> l = new LinkedList<>(Arrays.asList(14, 73, 18));
List <Integer> l = new LinkedList<>(List.of(14, 73, 18));

/* more compact version (immutable) */
List <Integer > l = List.of(14, 73, 18);
```
```Java
/*--> INZIALIZZAZIONE DI SET INTERFACE*/
public static void main(String[] args) {
    List<String> l = List.of("Nicola", "Denise", "Agata", "Marzia", "Agata");

    Set<String> hs = new HashSet<>(l);
    System.out.println(hs);
    // [Denise, Marzia, Nicola, Agata]

    Set<String> lhs = new LinkedHashSet<>(l);
    System.out.println(lhs);
    // [Nicola, Denise, Agata, Marzia]

    Set<String> ts = new TreeSet<>(l);
    System.out.println(ts);
    // [Agata, Denise, Marzia, Nicola]
  
    /* more compact version (immutable) */
    Set<String> set = Set.of("Nicola", "Denise", "Agata", "Marzia", "Agata");
}
```
```Java
/*--> INZIALIZZAZIONE DI MAP INTERFACE*/
Map<Integer, String> src;
src = new HashMap<>();
src.put(77, "Nicola");
src.put(17, "Marzia");
src.put(22, "Agata");
System.out.println(src);
// {17=Marzia, 22=Agata, 77=Nicola}

src = new LinkedHashMap<>();
src.put(77, "Nicola");
src.put(17, "Marzia");
src.put(22, "Agata");
System.out.println(src);
// {77=Nicola, 17=Marzia, 22=Agata}

src = new TreeMap<>();
src.put(77, "Nicola");
src.put(17, "Marzia");
src.put(22, "Agata");
System.out.println(src);
// {17=Marzia, 22=Agata, 77=Nicola}

```
```Java
public interface Comparable<T> {
    int compareTo(T obj);
}
public interface Comparator<T> {  // raccolta di oggetti da confrontare
    int compare(T obj1, T obj2);
}
// esempio di comparable
public class Person implements Comparable<Person> {
  protected String name; 
  protected String lastname;
  protected int age;
   
  public int compareTo(Person p) {
	// order by surname
	return lastname.compareTo(p.lastname);
  }
}
// esempio di comparator - ordina un insieme di oggetti
public class SortByAge implements Comparator<Person> {
  @Override
  public int compare(Person o1, Person o2) {
    return o1.age - o2.age;
  }
}

```
```Java
public static <T> T doSomething(T t) {
    return t;
}
public static <E> int length(E[] array) {
    return array.length;
}

```
```Java
class SimpleClass {

    public <T> T getParameterizedObject(T t) {
        return t;
    }
}
/*Questa classe non fornisce un parametro di tipo, quindi dobbiamo specificare il parametro di tipo nella
*dichiarazione del metodo per rendere il metodo getParameterizedObject generico.
*!In questo esempio non possiamo usare T come tipo per un campo nella classe, perché appartiene al metodo
*piuttosto che alla classe stessa.
*/
```

