# Sprawozdanie APRO Laboratorium 5 
### Antoni Kwietniewski(303706)
## Zadanie 1
W celu wykonania zadania napisałem dwa programy konkatenujące łańcuchy znaków na różne sposoby.
Pierwszy z nich używa operatora `+=` .
```java 
public class WithoutStringBuilder {
    
    public static void main(String[] args) {
        
        String word = "abc";
        word+="def";
        
    }

}
```
Natomiast drugi z nich stosuje metodę konkatynowania poprzez użycie obiektu klasy `StringBuider`.
```java 
public class WithStringBuilder {

    public static void main(String[] args) {

        StringBuilder stb = new StringBuilder();
        stb.append("abc");
        stb.append("def");

    }
}
}
```
W celu przeanalizowania działania obu algorytmów posłużyłem się programem `javap`, który umożliwia deasemblację plików .class. 
Wynik dla algorytmu w którym implementowałem StringBuilder:   
