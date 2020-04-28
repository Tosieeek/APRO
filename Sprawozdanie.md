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
Wynik dla algorytmu w którym implementowałem `StringBuilder`:   
![zdjęcie zadania](WithStr.png)
  ### Instrukcje 1  
`aload_0` - pobiera referencję do obiektu ze zmiennej lokalnej i umieszcza ją na stosie.  
`invokespecial #1` - wywołuje instrukcję konstruktora.  
`return` - kończy instrukcję konstruktora i informmuje o zakńczeniu jego wykonywania.  
Później wykonywane są instrukcje zapisane w metodzie main:   
`new` - tworzy referencję do obiektu klasy StringBuilder.   
`dup` - duplikuje referencje powstałą w poprzednim kroku. Na stosie znajdują się teraz dwie identyczne referencje.   
`invokespecial #3` - wywołuje konstruktor z klasy StringBuilder i zdejmuje ze stosu jedną, zduplikowaną wcześniej referencję.  
`astore_1` - zdejmuje referencję ze stosu i przypisuje ją do zmiennej lokalnej word.    
`aload_1` - pobiera referencję ze zmiennej lokalnej word i wrzuca ją na czubek stosu.  
`ldc` - wrzuca na stos referencję do stringa word.  
`invokevirtual #5`  - wywołuje metodę append z klasy StringBuilder i wrzuca na górę stosu referencję do utworzonego obiektu.  
W tym momencie w pamięci znajdują się 2 referencje do tej samej komórki następuje operacja `pop`.
Ten sposób konkatynacji dokonuje zmian na referencji i nie tworzy nowej referencji w pamięci.(Nie musiała angażować większej ilości zasobów.)
Później następuje ponowne pobranie referencji ze zmiennej lokalnej na stos, umieszczenie na stosie stringa("def"), wykonanie metody append oraz usunięcie ze stosu referencji.  
`return` informuje o zakończeniu się tej metody  


Wynik dla algorytmyu, który konkatynował wartości z użyciem operatora `+=`:  

![zdjęcie zadania](WithoutStr.png)
  ### Instrukcje 2
`aload_0` - pobiera referencję do obiektu ze zmiennej lokalnej i umieszcza ją na stosie.  
`invokespecial #1` - wywołuje instrukcję konstruktora.  
`return` - kończy instrukcję konstruktora i informmuje o zakńczeniu jego wykonywania.  
Później wykonywane są instrukcje zapisane w metodzie main:   
`ldc` - wrzuca na stos referencję do stringa stb.  
`astore_1` - zdejmuje referencję ze stosu i przypisuje ją do zmiennej lokalnej stb. 
`aload_1` - pobiera referencję ze zmiennej lokalnej stb i wrzuca ją na czubek stosu.  
`invokedynamic #3,  0` - wywołanie metody knkatenacji łańcucha znaków- tworzy to nową referencję  
`astore_1` - zdejmuje referencję ze stosu i przypisuje ją do zmiennej lokalnej stb. 
`return` informuje o zakończeniu się tej metody  

### Wnioski 
Jeżeli zależy nam na jak najlepszej efektywności algorytmu powinniśmy wybrać metodę konkatynacji polegającą na utworzeniu obiektu klasy StringBuilder, zastosowanie tej metody pozwoli zaoszczędzić zasoby pamięci. Ta metoda nie towrzy nowej referencji, nowego obiektu. Wszystkie operacje są wykonywane na jednym obiekcie zapisanym tylko w jednym miejscu w pamięci. Kiedy chcemy użyć operatorów `+=` tworzona jest kolejna referencja do nowego obiektu, a co za tym idzie, przez pewien czas w naszej pamięci znajdują się dwie referencje. Nie jest to potrzebne, ponieważ później jedna zostanie nadpisana przez drugą.
