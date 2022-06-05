# DECOMPOSITON

Türkçe'deki karşılığı ayrıştırma olan 'Decomposition' kavramı en basit ifade ile büyük bir problemi alt problemlere ayrıştırmak anlamına gelmektedir. Mantıken bakılacak olursa büyük bir problemi daha yönetilebilir alt problemlere bölmek daha motive edicidir. Çünkü büyük sorunlar, küçük sorunlara göre daha zor çözülebilmektedir.

C dilinde ayrıştırma birimi fonksiyonlar iken, C++ ve Java'da ayrıştırma birimi sınıflardır.Ayrıştırmanın tam anlamı ile uygulanabilmesi için alt problemlerin hepsinin mümkün olduğunca birbirinden bağımsız olması gerekmektedir.Burada denilmek istenen alt sınıfların olmayacağı değil, sadece gereksiz detaylar ile sınıflar birbirlerine bağlanmamalıdır.Bu yaklaşımın bir diğer avantajı ise uzayıp giden kod bloklarının önüne geçilmiş olmasıdır.

Bağımsızlığın bir diğer avantajı ise programcının programı yazarken programın geri kalanı hakkında endişelenmesini ortadan kaldırarak her soruna odaklanabilmesini sağlamaktır.

Decomposition kavramını uygularken karşımıza çıkan 'black box' kavramına değinmemiz gerekmektedir.

## Black Box

İyi ayrıştırılmış bir işlev ya da iyi tasarlanmış bir sınıf yazılımın kara kutusuna benzetilebilir.Bu kara kutunun içeriğinin belli olmamasına rağmen başardığı işle tanımlanır.Girdilerinin iyi tanımlanmış olması gerekmektedir.Kara kutuyu yaptğı işleme göre tanımlarız.

Ayrıştırmanın temel amacı, problemi bağımsız alt problemlere bölmektir.Kara kutular bu hedefin doğal uzantısıdır.Bağımsız yazılabilirler, gereksiz etkileşime girmezler.Kara kutular ve sınıflar düzenli bir soyutlamaya ve etkisiz bir yöntem paketine sahip nesneyi temsil eder.

Bir kara kutu oluşturulurken dikkat edilecek etmenler vardır.Bu etmenlere aşağıda kısaca değinelim.

* **_Abstraction(Soyutlama)_**

Ayrıştırma bir böl ve yönet stratejisidir.Alt bölümler birbirlerinden bağımsızdır.Dışarıdan bakıldığında, kara kutular mümkün olduğu kadar basittir, bu nedenle kolayca kullanılabilirler.Her bir kara kutu ayrı ayrı oluşturulur ve kullanım esnasında bir araya getirilir.Bu süreç yalnızca kara kutunun temelinde sunulan soyutlama çerçevesinde mantıklıdır.Girdi ve çıktılar arasında mantıklı bir ilişki olması zorunludur.Bu süreçteki asıl test şudur: Bu bileşenin neyi başardığını açıklamak kolay mı? Bir yöntem için işlemin alıcıya göre net bir tanımı olmalıdır.

* **_Uygulamada Fonksiyon Kuralları_**

Parametrelerin neler olacağı belirlenmiş olmalıdır.Alt fonksiyonlar yeterli derecede bağımsız ve karmaşıklığı en aza indirgenmiş olmalıdır.

* **_Tek Bir Probleme Odaklanmak_**

Bir fonksiyon tek bir sorunun çözümüne odaklanmış olmalıdır. Her fonksiyon daha sonrasında bir araya getirilerek büyük bir problemi çözecek basit fonksiyonlar olarak tanımlanmalıdır.

* **_Uzunluk_**
  
Uzunluk, analizin yerini almayan basit bir ölçüdür. Bir fonksiyon birden fazla sorunun çözümüne odaklanırsa dolaylı olarak çözüm için gerek süre uzayacaktır. Bu demek değildir ki her fonksiyonun uzunluğunu kısa tutmalıyız. Bazen sorunlar hiçbir alt parçanın olmadığı uzun bir alt parça dizisini gerektirebilir. Ancak yinede unutmamakta fayda var ki ideal bir fonksiyon ortalama 5-15 satır uzunluğunda olmalıdır.

* **_Kısa Rutinler_**

Kısa rutin dediğimiz kavram 1-2 satırlık kod parçasını ifade etmektedir. 1-2 satırda gerçekleştirilibilecek bir olay muhtemelen yeterince karmaşık değildir. Bu yüzden kendi rutininin olmasını haketmektedir. Kısa rutinler oluşturmak programın okunabilirliği içinde faydalıdır. Örneğin;

```
Sqrt((a.x - b.x)^2 + (a.y - b.y)^2) 
```

ifadesini

```
distance(a,b) 
```

ifadesi ile değiştirmek kodu çok daha okunabilir hale getirir.
Tek satırlık bu kodun çalışma zamanına etkisi hakkında endişelenmeye gerek yoktur. Çünkü derleyicinin uygun olduğunda kodu çağıracağını biliyoruz.
Java'da tek satırlı erişimler kullanmak iyidir. Çokça kullandığımız tek satırlık get ve set metodları buna örnektir.

* **_Parametreler_**

Bir metod problemi çözmek için mümkün olan en az sayıda değişkene sahip olmalıdır. Kullanıcı tarafından talep edilenden fazla kısıtlamalar eklenmemelidir. Bu durum metodun yeniden kullanımını kolaylaştırır.

* **_Karmaşıklık_**

Bir fonksiyondaki her satır bu fonksiyona ait algoritmanın adımlarını anlatmalıdır. Eğer programın karmaşıklığını arttıran ya da ayrıntıları fazlalaştıran bir durum söz konusu ise, dikkati dağıtmamak için fonksiyon ayrıştırılmalıdır. Her adımdaki işlevlerin tümü aynı ayrıntı düzeyinde çalışıyor olmalıdır.

* **_Tekrar_**

Yazılımın temel ilkelerinden birisi kendini tekrar eden kodlar yazmaktan kaçınmaktır. En basit örnek olarak; eğer 2 farklı ancak birbirine yakın problemi çözmek için "method overriding" ya da "method overloading" gibi yaklaşımları kullanabiliriz.Asla "ctrl+c" "ctrl+v" yazılımcısı olmamalıyız.

* **_Genelleme_**

Son derece bilinen veya yaygın olan bir problemin çözümünde alt problemlere ayrıştırılmamalıdır. Bunlara örnek olarak; arama ve sıralama problemleri verilebilir.Çünkü bu problemlerle daha önce defalarca karşılaşılmış olduğundan metodun işlevi kolayca çağrışım yapabilecektir. Diğer taraftan modern bir programlama dili bu gibi yaygın problemlerin çözümünde kullanılacak hazır çözümler içermektedir. Tek yapmak gereken ilgili kütüphaneyi çağırmak olacaktır. Bu nedenle bu gibi durumlarda decomposition işlemi yapmamıza gerek yoktur.

* **_Yerel Olmayan Erişim_**

Fonksiyon dışındaki bir değişkene erişim her zaman için parametreler aracılığı ile olmalıdır.Global tanımlanmış bir değişkene yerel olmayan erişim "black box" paradigmasını ihlal eder. Temel olarak bir kara kutunun programın diğer kısımları ile iletişime girerken karmaşıklığı ve soyutlamayaı basit tutmak için parametre mekanizmasını kullanmasını sağlamak gerekir. Yerel olmayan erişim, sabitler ve standart girdi-çıktı dosyaları için uygundur. 
