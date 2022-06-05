# Liskov Subsitute Principle

Yazılım geliştirirken çok sık karşımıza çıkan ve her yazılımcının vakıf olması gereken bir konudur "SOLID" prensipleri.Nedir bu SOLID prensipler?

- S-Single Responsibility
- O-Open Closed Principle
- L-Liskov Subsitute Principle
- I-Interface Segregation Principle
- D-Dependecy Inversion Principle

Liskov Subsitute Principle SOLID prensipler içerisinde kafa karışıklığına en uygunu ancak anlaşıldığında bu kadar kolaymı dedirten yöntemdir. 

## Liskov Subsitute Principle Nedir?

Liskov Subsitute Principle (LSP), ilk olarak Barbara Liskov tarafından Veri soyutlama ve hiyerarşi başlıklı bir 1988 konferans açılış konuşmasında tanıtılan, güçlü davranışsal alt tipleme adı verilen bir alt tipleme ilişkisinin özel bir tanımıdır."İkame edilebilirlik" kavramına dayanır.Nesne yönelimli programlamada bir nesnenin (bir sınıf gibi) ve bir alt nesnenin (birinci sınıfı genişleten bir sınıf gibi) birbirinin yerine geçebilmesi gerektiğini belirten bir ilkedir.

Barbara Liskov'a göre
> Aranan yer değiştirme özelliği şöyle tanımlanabilir: T cinsinden parametre alan tüm programlar (fonksiyonlar) P olacak şekilde, S tipinde o1 nesnesi ve T tipinde o2 nesnesi olsun. Eğer o1 ile o2 nesneleri yer değiştirdiğinde P’nin davranışı değişmiyorsa S tipi T tipinin alt tipidir!

Barbara Liskov'un bu tanımlaması biraz anlaşılması güç olsa gerektir ki daha sonraları Robert Cecil Martin kavramı şu şekilde anlatmıştır.
> Temel sınıfın(base class) işaretçisini(pointer) ya da referansını kullanan fonksiyonlar, bu sınıftan türemiş olan sınıfları(derived class) da ekstra bilgiye ihtiyaç duymaksızın kullanabilmelidir.

Bu tanımlamaların paralelinde daha somut olarak konuyu açıklamak gerekirse; üst sınıf ile alt sınıf arasında davranışsal olarak hiçbir fark olmamalıdır.Üst ve alt sınıflar birbirlerinin yerine kullanılabilir olmalıdırlar.

Bu kavramı izah etmenin bence en iyi yolu kodlamak. Robert C. Martin'in _A Handbook of Agile Software Craftsmanship_ kitabından bir örnekle konuyu inceleyelim.

Öncelikle bir Ördek(Duck) sınıfı belirleyeceğiz, ördeğin bağırma (Quack) özelliğini bu sınıfta yöntem olarak belirteceğiz. Ayrıca birkaç ördek türü de oluşturacağız. (Yeşilbaşlı Ördek, Yaz ördeği, Plastik Ördek)

Duck.java
```
public abstract class Duck {
    public abstract void quack();
}

public class MallarDuck extends Duck{

    @Override
    public void quack() {
        System.out.println("Quack!");
    }
}
```
MarbleDuck.java
```
public class MarbleDuck extends Duck{
    @Override
    public void quack() {
        System.out.println("Quack!");
    }
}
```
RubberDuck.java
```
public class RubberDuck extends Duck{
    @Override
    public void quack() {
        System.out.println("Quack!");
    }
}
```
Ördeklerin yüzme ve uçma özelliklerini sınıflara ekleyelim.

Duck.java

```
public abstract class Duck {
    public abstract void quack();
    public abstract void swim();
    public abstract void fly();
}
```
MallarDuck.java
```
public class MallarDuck extends Duck{

    @Override
    public void quack() {
        System.out.println("Quack!");
    }

    @Override
    public void swim() {
        System.out.println("Swimming!");
    }
    @Override
    public void fly(){
        System.out.println("Flying!");
    }
}
```
MarbleDuck.java
```
public class MarbleDuck extends Duck {
    @Override
    public void quack() {
        System.out.println("Quack!");
    }

    @Override
    public void swim() {
        System.out.println("Swimming!");
    }

    @Override
    public void fly() {
        System.out.println("Flying!");
    }
}
```
RubberDuck.java
```
public class RubberDuck extends Duck {
    @Override
    public void quack() {
        System.out.println("Quack!");
    }

    @Override
    public void swim() {
        System.out.println("Swimming!");
    }

    @Override
    public void fly() throws Exception {
        throw new Exception("Rubber ducks can't fly!");
    }
}
```
Evet plastik ördek uçamaz.Bizim RubberDuck sınıfımız LSP'yi bozmaktadır.Bu sorunu LSP' ye uyarlayarak çözelim.

RubberDuck sınıfımızda uçma özelliği olmayacağı için, bağırma, yüzme ve uçma özelliklerini içeren bir interface oluşturalım.

IFly.java
```
public interface IFly {
    void fly();
}
```
ISwim.java
```
public interface ISwim {
    void swim();
}
```
IQuack.java
```
public interface IQuack {
    void quack();
}
```

Şimdi ördek sınıflarımızı bu interfacelerden implement edelim.

MallarDuck.java
```
public class MallarDuck implements IFly,IQuack,ISwim{

    @Override
    public void quack() {
        System.out.println("Quack!");
    }

    @Override
    public void swim() {
        System.out.println("Swimming!");
    }
    @Override
    public void fly(){
        System.out.println("Flying!");
    }
}
```
MarbleDuck.java
```
public class MarbleDuck implements IFly,IQuack,ISwim {
    @Override
    public void quack() {
        System.out.println("Quack!");
    }

    @Override
    public void swim() {
        System.out.println("Swimming!");
    }

    @Override
    public void fly() {
        System.out.println("Flying!");
    }
}
```

Bizim için plastik ördeklerin uçamayacağı durumu olduğundan 'RubberDuck' sınıfına IFly interface'ini implement etmiyoruz.

RubberDuck.java
```
public class RubberDuck implements IQuack,ISwim {
    @Override
    public void quack() {
        System.out.println("Quack!");
    }

    @Override
    public void swim() {
        System.out.println("Swimming!");
    }
}
```

Interfaceler yardımı ile ördek sınıflarına istediğimiz özellikleri verebildik.
'Duck' sınıfını extend ettiğimiz 'RubberDuck' sınıfında ortaya çıkan problemi çözmek için işimize yarayacak özellikleri interface kullanarak implement ettik ve sorunu çözmüş olduk.

> Alt sınıflardan oluşan nesnelerin, üst sınıfın nesneleri ile yer değiştirdikleri zaman, aynı davranışı sergilemesi gerekmektedir.

Bu tanımın önemini daha iyi kavramış olduk.
