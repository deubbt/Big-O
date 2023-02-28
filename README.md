# Big-O
> [Cracking-the-Coding-Interview-6th-Edition-189-Programming-Questions-and-Solutions](https://www.amazon.com/Cracking-Coding-Interview-Programming-Questions/dp/0984782850) Kitabının Big O bölümünün çevirisidir. Big O'yu tam anlamıyla öğrenebileceğiniz tek Türkçe kaynak.


<center><b>Big O</b></center>



<ol id="icerik">
<h1 id="i̇çi̇ndeki̇ler"><center>İÇİNDEKİLER</center></h1>
  <li class="parent"><a href="#1">Bir Benzetme / Kıyas</a></li>
  <li class="parent"><a href="#2">Zaman Karmaşıklığı</a>
    <ol>
      <li class="child"><a href="#3">Big O, Big Theta, and Big Omega</a></li>
      <li class="child"><a href="#4">Best Case, Worst Case ve Expected Case</a></li>
    </ol>
  </li>
  <li class="parent"><a href="#5">Bellek Karmaşıklığı</a>
    <ol>
      <li class="child"><a href="#6">Sabitleri Düşürmek</a></li>
      <li class="child"><a href="#7">Non-Dominant Terimleri Çıkartmak</a></li>
    </ol>
  </li>
  <li class="parent"><a href="#8">Çoklu Parçalı Algoritmalar: Toplama mı Çarpma mı?</a></li>
  <li class="parent"><a href="#9">Amortize olmuş zaman</a></li>
  <li class="parent"><a href="#10">Log N Çalışma Zamanı</a></li>
  <li class="parent"><a href="#11">Özyinelemeli Çalışma Süreleri</a></li>
  <li class="parent"><a href="#12">Örnekler ve Alıştırmalar</a></li>
  <li class="parent"><a href="#13">Ek Problemler</a></li>
</ol>


Bu konu o kadar önemli ki, bunu anlamak için tam bir bölüm ayırdık. Big O zamanı, algoritmaların verimliliğini tanımlamak için kullanılan bir dil ve ölçüttür. Bu kavramı tam olarak anlamamak, bir algoritma geliştirirken gerçekten zararlı olabilir. Sadece Big O'yu gerçekten anlamadığınız için başkaları tarafından sert bir şekilde eleştirilebilirsiniz ve ayrıca algoritmanızın ne kadar hızlı veya yavaş çalıştığını değerlendirmekte zorluk çekebilirsiniz. Bu nedenle, bu kavramı kesinlikle öğrenmenizi öneriyorum.

<h3 id="1">• Bir Benzetme / Kıyas</h3>
Şöyle bir senaryo düşünün: Sabit diskte bir dosyanız var ve bunu ülkenin diğer ucunda yaşayan arkadaşınıza mümkün olan en kısa sürede ulaştırmak istiyorsunuz. Dosyayı nasıl göndermelisiniz? 

Çoğu insanın ilk düşüncesi e-posta, FTP veya başka bir elektronik transfer yöntemi olacaktır. Bu düşünce mantıklı, ancak yarısı doğru.

Küçük bir dosya için, elbette haklısınız, havaalanına gitmek, uçağa binmek ve arkadaşınıza teslim etmek 5-10 saat alacaktır.
Ancak dosya gerçekten, gerçekten büyükse ne olacak? Fiziksel olarak uçağı kullanarak teslim etmek daha hızlı olabilir mi? 

Evet, aslında öyle. Bir terabayt (1 TB) boyutunda bir dosya elektronik olarak aktarılırsa bir günden fazla sürebilir. Ülkenin diğer ucuna uçarak teslim etmek çok daha hızlı olacaktır. Eğer dosyanız acilse (ve maliyet bir sorun değilse) bunu yapmayı tercih edebilirsiniz.

Ya uçuş yoksa ve ülkeyi arabayla geçmeniz gerekiyorsa? O zaman bile gerçekten büyük bir dosya için arabayla gitmek daha hızlı olacaktır.

<h3 id="2">• Zaman Karmaşıklığı</h3>
Bu, asimptotik çalışma zamanı veya büyük O zamanı kavramının ne anlama geldiğini açıklar. Veri transferi "algoritması" çalışma zamanını şöyle tanımlayabiliriz:

• Elektronik Transfer: O(s), burada s dosyanın boyutunu ifade eder. Bu, dosyanın boyutuyla lineer olarak artan bir şekilde aktarım süresinin artacağı anlamına gelir. (Evet, bu biraz basitleştirilmiş bir açıklama ancak bu amaçlar için yeterli.)

• Uçak Transferi: Dosya boyutuna göre O(1). Dosya boyutu arttıkça dosyayı arkadaşınıza ulaştırmak daha uzun sürmeyecektir. Süre sabittir.
~~~c
+
|                               XXX
|                            XXX
|     O(1)                 XXX
+-----------------------XXX---------+
|                     XXX
|                   XXX
|                 XXX
|              XXXX
|            XXX    O(S)
|          XXX
|       XXX
|    XXXX
|XXXXX
XX
+-----------------------------------+
~~~
Sabit olan sürenin ne kadar büyük olduğu veya lineer artışın ne kadar yavaş olduğu fark etmeksizin, lineer süre sabit süreyi bir noktada geçecektir.{O(1)}

Bunun yanı sıra birçok farklı çalışma zamanı vardır. En yaygın olanları O(log N), O(N log N),<br>
O(N), O(N²) ve O(2<sup>N</sup>)'dir ancak mümkün olan çalışma zamanları için sabit bir liste yoktur.

Ayrıca çalışma zamanında birden çok değişken de kullanabilirsiniz. Örneğin, w metre genişliğinde ve h metre yüksekliğinde bir çiti boyama süresi, O(wh) olarak tanımlanabilir. Eğer p kat boya gerekiyorsa, sürenin O(whp) olduğunu söyleyebilirsiniz.

<h5 id="3">Big O, Big Theta, and Big Omega</h5>
Eğer daha önce akademik bir ortamda büyük O notasyonunu işlemediyseniz, bu bölümü atlayabilirsiniz. Kafanızı daha çok karıştırabilir. Aşağıdaki bilgilendirme, öğrencilerin büyük O notasyonunu öğrenirken yaşadıkları kafa karışıklığını gidermek için hazırlanmıştır.

Akademisyenler, çalışma zamanlarını tanımlamak için büyük O, büyük Θ (theta) ve büyük Ω (omega) terimlerini kullanır.

- **• O (Big O):** Big O gösterimi, bir algoritmanın en kötü durumda ne kadar hızlı çalışabileceğini tanımlar. Örneğin, bir dizi içindeki tüm öğeleri yazdırmak için bir algoritma düşünelim. Bu algoritmanın çalışma süresi, dizinin boyutuna bağlı olacaktır. Eğer dizinin boyutu n eleman ise, algoritmanın çalışma süresi O(n) olarak tanımlanabilir. Bu, algoritmanın en kötü durumda n elemanlı bir dizide tüm elemanları yazdırmak için en fazla n adım gerektirdiği anlamına gelir.<br><br>
Ancak, algoritmanın çalışma süresi O(N²) veya O(2^<sup>n</sup>) gibi daha yavaş bir oranda da tanımlanabilir. Bu durumda, algoritmanın en kötü durumda n elemanlı bir dizide çalışması N² veya 2^<sup>n</sup> adım kadar zaman alacaktır. Burada önemli olan, bu gösterimlerin yalnızca bir üst sınır olduğudur. Algoritmanın gerçek çalışma süresi, bu gösterimlerin altında da olabilir.<br><br>
Benzer şekilde, Bob'un yaşını 130'den küçük olarak belirleyebiliriz (X ≤ 130), ancak bu, yaşının gerçek değeri olması anlamına gelmez. Bu sadece bir üst sınır olduğu için, Bob'un yaşının 100 veya 50 olabileceği gibi, 25 de olabilir.

- **• Ω (Big omega):** Akademide, Ω, alt sınır için aynı kavramı ifade eder.Big Ω, O'nun tam tersi olarak alt sınırları ifade eder. Bir dizideki değerleri yazdırmak için kullanılan algoritma, Ω(N) olduğu gibi Ω(log N) ve Ω(1) olarak da tanımlanabilir. Yani en az bu sürelerde çalışacaktır.

- **• Θ (Big theta):** Akademide, Θ, O ve Ω için kullanılır.
Big Θ, O ve Ω'nun karşılığıdır. Yani bir algoritma, O(N) ve Ω(N) ise Θ(N) olarak tanımlanır. Θ, çalışma zamanının sıkı bir üst sınırını verir.

Endüstride (ve dolayısıyla mülakatlarda), insanlar Θ ve O terimlerini birleştirmiş gibi görünüyorlar.
Endüstrinin büyük O'nun anlamı, akademisyenlerin Θ olarak anladığına daha yakındır, çünkü bir dizi yazdırmayı O(N²) olarak tanımlamak yanlış olarak görülür. Endüstri sadece bunu O(N) olarak tanımlar.

<h5 id="4">Best Case, Worst Case ve Expected Case</h5>
Bir algoritmanın zaman karmaşıklığını aslında üç farklı şekilde tanımlayabiliriz.

Bu durumu [Quick Sort](../Sorting-Algorithms/Quicksort/) algoritması açısından ele alalım. Quick sort, "pivot" olarak adlandırılan bir rastgele eleman seçer ve ardından dizideki değerleri pivot'tan küçük olanlar pivot'tan büyük olan değerlerden önce gelmek üzere yer değiştirir. Bu işlem, bir "kısmi sıralama ([partial sorting](https://en.wikipedia.org/wiki/Partial_sorting))" sağlar. Daha sonra, benzer bir işlem kullanarak sol ve sağ tarafları rekürsif olarak sıralar.

- **• Best Case:** Eğer tüm elemanlar eşitse, quick sort, ortalama olarak sadece bir kez dizi üzerinde gezinir. Bu O(N)'dir (Eleman sayısı kadar). (Aslında bu, quick sort'ın uygulamasına biraz bağlıdır. Ancak, sıralanmış bir dizide çok hızlı çalışacak uygulamalar vardır.)

- **• Worst Case:** Eğer çok şanssız olursak ve pivot tekrar tekrar dizinin en büyük elemanı olursa ne olur? (Aslında bu kolayca olabilir. Pivot, alt dizideki ilk eleman olarak seçildiğinde ve dizi ters sırada sıralanmışsa, bu durum oluşacaktır.) Bu durumda, özyinelemeli işlem diziyi yarıya bölemez ve her yarıda özyinelemeli işlem yapamaz. Bu durumda, O(N²) çalışma süresi oluşur.

- **Expected Case:** Genellikle, bu harika veya korkunç durumlar oluşmaz. Tabii, bazen pivot çok düşük veya çok yüksek olacak, ancak bu durumlar tekrar tekrar oluşmaz. Bu durumda O(N log N) bir çalışma süresi bekleyebiliriz.

En iyi durum zaman karmaşıklığını nadiren tartışırız, çünkü çok kullanışlı bir kavram değildir. Sonuçta, hemen hemen herhangi bir algoritmayı, bazı özel durumları ele alıp, en iyi durumda O(1) zaman karmaşıklığına sahip olabiliriz.

Çoğu algoritmanın -belki de çoğunluğunun- en kötü durum ve beklenen durum zaman karmaşıklığı aynıdır. Ancak bazen farklı olabilirler ve her iki çalışma süresini de tanımlamamız gerekebilir.

*Best/worst/expected case ve big O/theta/omega arasındaki ilişki nedir?*

En iyi, en kötü ve beklenen durumlar, belirli girdiler veya senaryolar için Big O (veya Big Theta) zamanını açıklar.

Big O, Big Omega ve Big Theta, çalışma zamanı için üst, alt ve sıkı sınırları tanımlar. Bu kavramlar arasında özel bir ilişki yoktur.

Öğrenciler genellikle bu kavramları karıştırır çünkü her ikisi de "daha yüksek", "daha düşük" ve "tam olarak doğru" gibi kavramlar içerir, ancak yine de bu kavramlar farklıdır.

<h3 id="5"> Bellek Karmaşıklığı</h3>

Zaman, bir algoritmanın önemli tek özelliği değildir. Algoritmanın gerektirdiği bellek veya alan miktarı da önemli olabilir.

Bellek karmaşıklığı, zaman karmaşıklığına paralel bir kavramdır. Örneğin, n boyutunda bir dizi oluşturmamız gerekiyorsa, bu O(n) bellek gerektirir. NxN boyutunda iki boyutlu bir dizi gerekiyorsa, bu O(n²) bellek gerektirir.

Ayrıca, özyinelemeli çağrılardaki yığın alanı da hesaba katılır. Örneğin, şu şekildeki kod, O(n) zaman ve O(n) bellek gerektirir:
```c
1 int sum(int n) {
2    if (n <= 0) {
3        return 0;
4    }
5    return n + sum(n-1);
6 }
```
Her çağrı yığında bir seviye ekler.
```
1 sum(4)
2    -> sum(3)
3      -> sum(2)
4        -> sum(1)
5            -> sum(0)
```
Bu çağrıların her biri, çağrı yığınına eklenir ve gerçek bellek kullanır.

Ancak, toplamda n çağrıya sahip olmanız, bu işlemin O(n) bellek kullanacağı anlamına gelmez. Aşağıdaki fonksiyonu düşünün, bu fonksiyon 0 ile n arasındaki bitişik elemanları toplar:
```c
1 int pairSumSequence(int n) {
2    int sum = 0;
3    for (int i = 0; i < n; i++) {
4        sum += pairSum(i, i + 1);
5    }
6    return sum;
7 }
8
9 int pairSum(int a, int b) {
10    return a + b;
11 }
```
pairSum'a yaklaşık olarak O(n) kez çağrı olacak. Ancak, bu çağrılar çağrı yığınında eş zamanlı olarak mevcut değil, bu nedenle sadece O(1) bellek kullanımına ihtiyacınız var.

<h5 id="6">Sabitleri Düşürmek</h5>
O(N) kodun belirli girdiler için O(1) koddan daha hızlı çalışması oldukça mümkündür. Big O, sadece artış hızını açıklar.

Bu nedenle, çalışma zamanındaki sabitleri düşürürüz. O(2N) olarak tanımlanabilecek bir algoritma aslında O(N) dir.

Birçok insan buna direnir. İki (iç içe olmayan) for döngüsü olan bir kod görürler ve bu O(2N) olarak devam ederler. Daha "kesin" olduklarını düşünürler: Ama değiller.

Aşağıdaki kodu düşünün:
```c
// MinandMax1
1 int min = INT_MAX;
2 int max = INT_MIN;
3 for (int i = 0; i < sizeof(array) / sizeof(int); i++) {
4    if (array[i] < min) {
5        min = array[i];
6    }
7    if (array[i] > max) {
8        max = array[i];
9    }
10 }
```
```c
// MinandMax2
1 int min = INT_MAX;
2 int max = INT_MIN;
3 for (int i = 0; i < sizeof(array) / sizeof(int); i++) {
4    if (array[i] < min) {
5        min = array[i];
6    }
7 }
8 for (int i = 0; i < sizeof(array) / sizeof(int); i++) {
9    if (array[i] > max) {
10        max = array[i];
11    }
12 }
```

Hangisi daha hızlıdır? İlki bir for döngüsü yapar ve diğeri iki for döngüsü yapar. Ancak, ilk çözüm her for döngüsü için bir satır kod içerirken diğeri sadece bir satır kod içerir.

Eğer adım sayısını sayacaksanız, o zaman derinlemesine gidip çarpmanın toplamadan daha fazla talimat gerektirdiği, derleyicinin bir şeyi nasıl optimize edeceği ve tüm diğer ayrıntıları dikkate almanız gerekir.

Bu korkunç derecede karmaşık olacaktır, bu yüzden bu yoldan hiç başlamayın. Big O, çalışma zamanının nasıl ölçeklendiğini ifade etmemizi sağlar. Sadece O(N) her zaman O(N²)'den daha iyi olduğu anlamına gelmediğini kabul etmemiz gerekiyor.

<h5 id="7">Non-Dominant Terimleri Çıkartmak</h5>
O(N² + N) gibi bir ifade için ne yapmalısınız? İkinci N tam olarak bir sabit değil. Ancak özellikle önemli değil.

Zaten sabitleri düşürdüğümüzü söyledik. Bu nedenle, O(N² + N²), O(N²) olurdu. Eğer o son N² terimiyle ilgilenmiyorsak, neden N ile ilgilensek ki? İlgilenmiyoruz.

Non-dominant terimleri çıkarmalısınız.
- • O(N² + N), O(N²) haline gelir.
- • O(N + log N), O(N) haline gelir.
- • O(5*2ᴺ + 1000N¹⁰⁰), O(2ᴺ) haline gelir.

Hala çalışma zamanında bir toplama olabilir. Örneğin, O(B² + A) ifadesi (A ve B hakkında bazı özel bilgiler olmadan) azaltılamaz.

Aşağıdaki grafik, bazı ortak büyük O zamanlarının artış oranını göstermektedir.

![](./asset2.jpeg)

Gördüğünüz gibi, O(x²) O(x)'den çok daha kötüdür, ancak O(2ˣ) veya O(x!) kadar kötü değildir. O(x!) gibi daha kötü birçok zamanlama vardır, örneğin O(xˣ) veya O(2ˣ * x!).

<h4 id="8">Çoklu Parçalı Algoritmalar: Toplama mı Çarpma mı?</h4>
Çok parçalı bir algoritmanız olduğunu ve iki adımdan oluştuğunu varsayalım. Bu durumda, işlem zamanlarını çarpacak mısınız, yoksa toplayacak mısınız?

Bu, öğrenciler için yaygın bir kafa karışıklığı kaynağıdır.
```c
// Çalışma zamanlarını toplayın: O(A + B)
1 void addRuntimes(int* arrA, int* arrB, int lenA, int lenB) {
2    for (int i = 0; i < lenA; i++) {
3        printf("%d ", arrA[i]);
4    }
5    for (int i = 0; i < lenB; i++) {
6        printf("%d ", arrB[i]);
7    }
8 }
```
```c
// Çalışma zamanlarını çarpın: O(A * B)
1 void multiplyRuntimes(int* arrA, int* arrB, int lenA, int lenB) {
2    for (int i = 0; i < lenA; i++) {
3        for (int j = 0; j < lenB; j++) {
4            printf("%d,%d ", arrA[i], arrB[j]);
5        }
6    }
7 }
```
İlk örnekte, önce A adet iş yaparız, ardından B adet iş yaparız. Bu nedenle, toplam iş <br>miktarı O(A + B) dir.

İkinci örnekte, A'daki her öğe için B adet iş yaparız. Bu nedenle, toplam iş miktarı O(A * B)'dir.

Diğer bir deyişle:

- • Algoritmanız "bunu yap, sonra bittiğinde onu yap" şeklindeyse, çalışma zamanlarını eklersiniz.
- • Algoritmanız "bunu yaparken her seferinde bunu yap" şeklindeyse, çalışma zamanlarını çarparsınız.

Mülakatta bunu karıştırmak çok kolay olduğundan, dikkatli olun.

<h4 id ="9">Amortize olmuş zaman</h4>
Bir ArrayList, veya dinamik boyutlu bir dizi, boyutunda esneklik sağlayarak bir dizinin avantajlarından yararlanmanızı sağlar. ArrayList'te alan tükenmeyecek, çünkü kapasitesi öğeleri ekledikçe büyüyecektir.

ArrayList bir dizi ile gerçekleştirilir. Dizi kapasitesine ulaştığında, ArrayList sınıfı kapasitesi iki katına çıkarılmış yeni bir dizi oluşturur ve tüm öğeleri yeni diziye kopyalar.

Ekleme işleminin çalışma süresini nasıl tanımlarsınız? Bu zor bir soru.

Dizi dolu olabilir. Dizi N öğesi içeriyorsa, yeni bir öğe eklemek O(N) zaman alacaktır. Kapasitesi 2N olan yeni bir dizi oluşturmanız gerekecektir ve N öğesi kopyalanacaktır. Bu ekleme O(N) zaman alır.

Ancak, bunun çok nadiren olduğunu da biliyoruz. Çoğu zaman ekleme işlemi O(1) zamanında gerçekleşir.

Her ikisini de hesaba katan bir kavrama ihtiyacımız var. İşte amortize zamanı bunu yapar. Evet, en kötü durum zaman zaman gerçekleşir. Ancak gerçekleştiğinde, bir daha uzun bir süre gerçekleşmeyecek kadar maliyet "amortize" edilir.

Bu durumda, amortize süresi nedir?

Öğeleri eklerken, dizi boyutu 2'nin bir kuvveti olduğunda kapasiteyi iki katına çıkarıyoruz. Bu nedenle, X öğelerinden sonra kapasiteyi 1, 2, 4, 8, 16, ..., X boyutlarında iki katına çıkarıyoruz. Bu iki katına çıkarma sırasıyla 1, 2, 4, 8, 16, 32, 64, ..., X kopyalama işlemi alır.

1 + 2 + 4 + 8 + 16 + ... + X toplamı nedir? Bu toplam, soldan sağa okursanız 1'den başlar ve X'e kadar iki katına çıkar. Sağdan sola okursanız X'ten başlar ve yarımşar bir şekilde 1'e kadar devam eder.

Öyleyse, X + X/2 + X/4 + X/8 + ... + 1 toplamı nedir? Bu yaklaşık olarak 2X'dir.

Bu nedenle, X eklemesi O(2X) zaman alır. Her eklem için amortize süresi O(1)'dir.

<h4 id ="10">Log N Çalışma Zamanı</h4>
Genellikle zaman karmaşıklıklarında O(log N) ifadesini sıkça görürüz. Bu nereden geliyor?

Bunun için bir örnek olarak ikili aramaya bakalım. İkili arama algoritmasında, N elemanlı sıralanmış bir dizide x öğesini arıyoruz. Öncelikle x değerini dizi ortasındaki elemanla karşılaştırıyoruz. Eğer x == ortanca eleman ise, arama işlemini bitirip ortanca elemanı döndürüyoruz. Eğer x ortanca elemandan küçükse, sol tarafı aramaya devam ediyoruz. Eğer x ortanca elemandan büyükse, sağ tarafı aramaya devam ediyoruz.
```
search 9 within {1,  5,  8,  9,  11,  13,  15,  19,  21}
    compare 9 to  11 -> smaller.
    search  9 within {1,  5,  8,  9,  11}
        compare 9 to  8  -> bigger
        search  9 within {9,  11}
            compare 9 to  9 return
```
N elemanlı bir dizide arama yapmaya başlıyoruz. Ardından bir adım sonra, N/2 elemana düşüyoruz. Bir adım daha atarak, N/4 elemana düşüyoruz. Değeri bulana veya yalnızca bir elemana düşene kadar bu işlemi gerçekleştiriyoruz.

Toplam çalışma zamanı, (N'yi her seferinde 2'ye bölerek) kaç adım atabileceğimize bağlı olarak belirlenir ve N, 1'e düşene kadar devam eder.
```
N = 16
N = 8    // divide   by  2
N = 4    // divide   by  2
N = 2    // divide   by  2
N = 1    // divide   by  2
```
Bunun tersine de bakabiliriz (16'dan 1'e gitmek yerine 1'den 16'ya gitmek). N'yi elde etmek için 1'i kaç kez 2 ile çarpabiliriz?
```
N = 1 
N = 2    // multiply   by  2
N = 4    // multiply   by  2
N = 8    // multiply   by  2
N = 16   // multiply   by  2
```
2ᵏ = N ifadesinde k nedir? Bu tam olarak logaritmanın ifade ettiği şeydir.
```
2⁴     =   16 ->  log₂l6  =  4 
log₂N  =   k  ->  2ᵏ      =  N
```
Bu, sizin için iyi bir sonuçtur. Sorun alanındaki öğe sayısı her seferinde yarıya indirildiğinde, muhtemelen O(log N) çalışma zamanı olacaktır.

Bu, dengeli bir ikili arama ağacında bir öğeyi bulmanın neden O(log N) olduğu aynı sebepten kaynaklanmaktadır. Her karşılaştırmada, ya sola ya da sağa gideriz. Her iki tarafın da yarısı düğümleri olduğundan, problem alanını her seferinde yarıya indiririz.

>[Logaritmanın tabanı nedir? Bu mükemmel bir soru! Kısaca, büyük O amaçları için önemli değildir.](https://stackoverflow.com/questions/6701809/base-of-logarithms-in-time-complexity-algorithms#:~:text=In)

<h4 id="11">Özyinelemeli Çalışma Süreleri</h4>

İşte zorlu bir soru. Bu kodun çalışma zamanı nedir?
```c
1   int f(int n)  {
2       if (n <= 1)  {
3           return  1;
4       }
5       return f(n - 1) + f(n - 1);
6   }
```
Birçok insan, bazı nedenlerden, f fonksiyonuna yapılan iki çağrıyı görüp O(N²)'ye atlayacaklar. Bu tamamen yanlıştır.

Varsayımlar yapmak yerine, kodu yürüterek çalışma zamanını türetelim. f(4) çağırdığımızı varsayalım. Bu, f(3)'ü iki kez çağırır. Bu f(3) çağrılarından her biri f(2) çağrısı yapar, f(1)'e ulaşıncaya kadar bu işlem devam eder.
```
                   f(4)
               /          \
             /              \
        f(3)                  f(3)        
       /    \                /    \       
    f(2)    f(2)          f(2)    f(2)    
    /  \    /  \          /  \    /  \    
f(1)    f(1)    f(1)  f(1)    f(1)    f(1)
```
Bu ağaçta kaç çağrı var? (Saymayın!)

Ağacın derinliği N olacaktır. Her düğüm (yani, fonksiyon çağrısı) iki çocuğa sahiptir. Bu nedenle, her seviyenin üstündekinin iki katı çağrısı olacaktır. Her seviyedeki düğüm sayısı şöyledir:

| LEVEL | # NODES | Also expressed as...             | Or... |
| --    | --      | --                               | --    |
| 0     | 1       |                                  | 2⁰    |
| 1     | 2       | 2 * previous level = 2           | 2¹    |
| 2     | 4       | 2 * previous level = 2 * 2¹ = 2² | 2²    |
| 3     | 8       | 2 * previous level = 2 * 2² = 2³ | 2³    |
| 4     | 16      | 2 * previous level = 2 * 2³ = 2⁴ | 2⁴    |

Bu nedenle, 2° + 2¹ + 2² + 2³ + 2⁴ +. • . + 2ᴺ (2⁽ᴺ⁺¹⁾ - 1) düğüm olacaktır. 

Bu kalıbı hatırlamaya çalışın. Birden çok çağrı yapan özyinelemeli bir fonksiyonunuz olduğunda, çalışma süresi genellikle (ancak her zaman değil) O(dallarᵈᵉᵖᵗʰ) şeklinde görünecektir, burada dallar her özyinelemeli çağrının dallanma sayısıdır. Bu durumda, bize O(2ᴺ) verir.

> Hatırlayabileceğiniz gibi, Big O için logların tabanı önemli değildir, çünkü farklı tabanların logları sadece sabit bir faktörle farklıdır. Ancak, bu üst kısımlara uygulanmaz. Bir tabanın üstü önemlidir. 2ⁿ ve 8ⁿ'i karşılaştırın. 8ⁿ'i genişletirseniz, (2³)ⁿ elde edersiniz, bu 2³ⁿ'ye eşittir, bu da 2²ⁿ * 2ⁿ'ye eşittir. Gördüğünüz gibi, 8ⁿ ve 2ⁿ, 2²ⁿ faktörüyle farklıdır. Bu kesinlikle sabit bir faktör değildir!

Bu algoritmanın bellek(uzay) karmaşıklığı O(N) olacaktır. Ağaçta toplamda O(2ᴺ) düğüm olsa da, yalnızca herhangi bir anda O(N) mevcuttur. Bu nedenle, yalnızca O(N) belleğe ihtiyacımız olacaktır.

<h4 id ="12">Örnekler ve Alıştırmalar</h4>
Big O zamanı başlangıçta zor bir kavramdır. Ancak, bir kez kafaya "tak" ettiğinde, oldukça kolay hale gelir. Aynı kalıplar tekrar tekrar ortaya çıkar ve gerisini türetebilirsiniz.

Basit bir şekilde başlayacağız ve giderek zorlaşacağız.

<h5>Örnek 1</h5>

Aşağıdaki kodun çalışma zamanı nedir?
```c
1 void foo(int array[], int size) {
2    int sum = 0;
3    int product = 1;
4    for(int i = 0; i < size; i++) {
5        sum += array[i];
6    }
7    for(int i = 0; i < size; i++) {
8        product *= array[i];
9    }
10    printf("%d, %d\n", sum, product);
11 }
```
Cevap:

<span class="spoiler">
Bu kodun çalışma zamanı O(N) olacaktır. Diziyi iki kez geçmemiz önemli değildir. O(n + n) = O(n)
</span>

<h5>Örnek 2</h5>

Aşağıdaki kodun çalışma zamanı nedir?
```c
1 void printPairs(int array[], int length) {
2    for (int i = 0; i < length; i++) {
3        for (int j = 0; j < length; j++) {
4            printf("%d,%d\n", array[i], array[j]);
5        }
6    }
7 }
```
Cevap:

<span class="spoiler">
İçteki for döngüsü N kez çağrıldığından ve N kez O(N) kez çalıştığından, çalışma zamanı O(N²)'dir.<br>
Bunun başka bir yolu, kodun "anlamını" inceleyerek görebileceğimizdir. Kod, tüm çiftleri (iki elemanlı dizileri) yazdırmaktadır. O(N²) çift vardır; dolayısıyla çalışma zamanı O(N²)'dir.<br> O (n * n) = O(N²)
</span>

<h5>Örnek 3</h5>
Bu, yukarıdaki örnekle çok benzer bir kod ancak içteki for döngüsü bu sefer i + 1'den başlıyor.

```c
void printUnorderedPairs(int* array, int length) {
    for(int i = 0; i < length; i++) {
        for(int j = i + 1; j < length; j++) {
            printf("%d,%d\n", array[i], array[j]);
        }
    }
}
```

Cevap:

Zaman karmaşıklığını birden fazla şekilde elde edebiliriz.

> Bu for döngüsü kalıbı çok yaygındır. Zaman karmaşıklığını bilmek ve derinlemesine anlamak önemlidir. Yaygın zaman karmaşıklıklarını ezberlemek yeterli değildir. Derin kavrayış önemlidir.

<h5>Döngü Yinelemelerini Sayma</h5>
İlk döngüde j, N-1 adımı için çalışır. İkinci kez döngüye girildiğinde, j N-2 adımı çalışır. Daha sonra, N-3 adımı çalışır ve bu böyle devam eder. Dolayısıyla, toplam adım sayısı şöyledir:
```
(N-1) +  (N-2) +  (N-3) +  ... + 2  + 1
    = 1 + 2 + 3 +  ... + N-1
    = sum of 1 through N-1
```
1'den N-1'e kadar olan sayıların toplamı, (N(N-1))/2'dir. Bu nedenle çalışma zamanı O(N²) olacaktır.
<h5>Bu ne anlama geliyor</h5>
Alternatif olarak, kodun çalışma süresini düşünerek ne anlama geldiğini anlayarak bulabiliriz. Kod, i < j olan j ve i değerlerinin her çifti için döngü oluşturur.

Toplamda N² adet çift bulunur. Bunların yaklaşık yarısı i < j'ye sahip olacak ve geri kalan yarısı<br> i > j'ye sahip olacaktır. Bu kod yaklaşık olarak N²/2 çift üzerinden işlem yapar, bu yüzden O(N²) iş yapar.

<h5>Ne Yaptığının Görselleştirilmesi</h5>
N = 8 olduğunda, kod aşağıdaki (i, j) çiftlerini tekrarlar:
```
(0, 1)  (0, 2)  (0, 3)  (0, 4)  (0, 5)  (0, 6)  (0, 7)
        (1, 2)  (1, 3)  (1, 4)  (1, 5)  (1, 6)  (1, 7)
                (2, 3)  (2, 4)  (2, 5)  (2, 6)  (2, 7)
                        (3, 4)  (3, 5)  (3, 6)  (3, 7)
                                (4, 5)  (4, 6)  (4, 7)
                                        (5, 6)  (5, 7)
                                                (6, 7)
```
Bu, yaklaşık olarak N²/2 boyutunda bir NxN matrisinin yarısı gibi görünüyor. Bu nedenle, işlem yapmak için O(N²) zaman alır.
<h5>Ortalama İş</h5>
Dış döngünün N kez çalıştığını biliyoruz. Peki iç döngü ne kadar iş yapar? İterasyonlara göre değişse de, ortalama iterasyon hakkında düşünebiliriz.

1, 2, 3, 4, 5, 6, 7, 8, 9, 10'un ortalaması nedir? Ortalama değer ortada olacaktır, bu yüzden yaklaşık olarak 5 olacaktır. (Tabii ki daha kesin bir cevap verebiliriz, ancak Big O için gerekli değil.)

Peki ya 1, 2, 3, ..., N için? Bu dizideki ortalama değer N/2'dir.

Bu nedenle, iç döngü ortalama olarak N/2 iş yapar ve N kez çalıştırılır, toplam işlem N²/2'dir ve O(N²) olarak ifade edilir. O(N * N/2) = O(N²)

<h5>Örnek 4</h5>
Bu yukarıdaki örnekle benzerdir, ancak şimdi iki farklı diziye(array) sahibiz.

```c
1 void printUnorderedPairs(int *arrayA, int lengthA, int *arrayB, int lengthB) {
2    for (int i = 0; i < lengthA; i++) {
3        for (int j = 0; j < lengthB; j++) {
4            if (arrayA[i] < arrayB[j]) {
5                printf("%d,%d\n", arrayA[i], arrayB[j]);
6            }
7        }
8    }
9 }
```
Bu analizi parçalara ayırabiliriz. j'nin for döngüsü içindeki if-ifadesi, yalnızca sabit zamanlı ifadeler dizisinden oluştuğu için O(1) zamanındadır.

Şimdi şuna sahibiz:

```c
1 void printUnorderedPairs(int *arrayA, int lengthA, int *arrayB, int lengthB) {
2    for (int i = 0; i < lengthA; i++) {
3        for (int j = 0; j < lengthB; j++) {
4            /* O(1) work */
5        }
6    }
7 }
```
Cevap:
<span class="spoiler">
arrayA'nın her bir öğesi için, içteki for döngüsü b = arrayB.length iterasyonuna gider. Eğer a = arrayA.length ise, çalışma süresi O(ab) olacaktır.<br>
Eğer O(N²) dediyseniz, o zaman daha önceki hatanızı hatırlayın. İki farklı girdi olduğu için bu O(N²) değildir. Her ikisi de önemlidir. Bu oldukça yaygın bir hatadır.
</span>

<h5>Örnek 5</h5>
Bu tuhaf kod parçası hakkında ne düşünüyorsunuz?

```c
1 void printUnorderedPairs(int* arrayA, int* arrayB, int lengthA, int lengthB) {
2    for (int i = 0; i < lengthA; i++) {
3        for (int j = 0; j < lengthB; j++) {
4            for (int k = 0; k < 100000; k++) {
5                printf("%d,%d\n", arrayA[i], arrayB[j]);
6            }
7        }
8    }
9 }
```
Cevap:
<span class="spoiler">
Burada gerçekten bir şey değişmedi. 100.000 birimlik iş hala sabit O(1) olduğundan, çalışma süresi hala O(ab) 'dir.
</span>

<h5>Örnek 6</h5>
Aşağıdaki kod bir diziyi tersine çevirir. Zaman karmaşıklığı nedir?

```c
1 void reverse(int array[], int length) {
2    for (int i = 0; i < length / 2; i++) {
3        int other = length - i - 1;
4        int temp = array[i];
5        array[i] = array[other];
6        array[other] = temp;
7    }
8 }
```
Cevap:
<span class="spoiler">
Bu algoritma, O(N) zamanda çalışır. Yalnızca dizinin yarısından geçtiği gerçeği (iterasyonlar açısından) Big O zamanını etkilemez.
</span>

<h5>Örnek 7</h5>
Aşağıdakilerden hangisi O(N) ile eşdeğerdir? Nedenleriyle birlikte açıklayabilir misiniz?

- • O(N  +  P), where P  < N/2
- • O(2N)
- • O(N  +  log N)
- • O(N  +  M)

Bunların üzerinden geçelim.
Cevap:
<span class="spoiler">
• Eğer P < N/2 ise, N'nin baskın terim olduğunu biliyoruz, bu nedenle O(P) terimini atlayabiliriz. (O(P) teriminin O(N) terimine oranla ihmal edilebilir düzeyde olması sebebiyle.)<br>
• O(2N) sabitleri atladığımızda O(N) ile aynıdır.<br>
• O(N), O(log N)'yi baskın kıldığından, O(log N) terimini atlayabiliriz.<br>
• N ve M arasında belirlenmiş bir ilişki olmadığından, her şey sonuncusu hariç O(N) ile eşdeğerdir.
</span>

<h5>Örnek 8</h5>
Elimizde, her bir stringi sıralayan ve ardından tüm diziyi sıralayan bir algoritma olsaydı, çalışma zamanı ne olurdu?

Birçok aday şöyle bir yaklaşım sergiler: Her bir stringi sıralamak O(N log N) işlemidir ve bunu her string için yapmamız gerektiği için bu O(N*N log N) eder. Ayrıca diziyi de sıralamamız gerektiği için ekstra O(N log N) işlem yaparız. Dolayısıyla, toplam çalışma zamanı O(N² log N + N log N) eder, yani sadece O(N² log N).

Ancak bu tamamen yanlıştır. Hata nedeni, N değişkenini iki farklı şekilde kullandığımızdandır. Bir durumda, N stringin uzunluğudur (hangi string?). Diğer durumda ise, N dizinin uzunluğudur.

Mülakatlarda, bu hatayı önlemek için N değişkenini hiç kullanmayabilirsiniz veya N'nin neyi temsil edebileceği açık olmayan durumlarda yalnızca kullanabilirsiniz.

Aslında, burada a ve b veya m ve n bile kullanmayacağım. Hangisinin hangisi olduğunu unutmak ve karıştırmak çok kolaydır. O(a²) çalışma zamanı, O(a*b) çalışma zamanından tamamen farklıdır.

Yeni terimleri tanımlayalım ve mantıklı isimler kullanalım:

- • s, en uzun stringin uzunluğu olsun.
- • a, dizinin uzunluğu olsun.

Şimdi adım adım ilerleyebiliriz:

- • Her bir stringi sıralamak O(s log s) işlemidir.
- • Bunun her bir string için yapılması gerektiği için (ve a tane string var), bu O(a*s log s) işlemine eşdeğerdir.
- • Şimdi tüm stringleri sıralamamız gerekiyor. a tane stringimiz var, bu nedenle bunun O(a log a) zaman alacağını söyleyebilirsiniz. Bununla birlikte, stringleri karşılaştırmanız da gerekiyor. Her bir string karşılaştırması O(s) zaman alır. O(a log a) karşılaştırma vardır, bu nedenle bu işlem <br>O(a*s log a) zaman alır.

Bu iki adımı topladığınızda, O(a*s(log a + log s)) elde edersiniz. Bu kadar. Daha da azaltmanız mümkün değildir.

<h5>Örnek 9</h5>
Aşağıdaki basit kod, dengeli bir ikili arama ağacındaki tüm düğümlerin değerlerini toplar. Zaman karmaşıklığı nedir?

```c
1   int sum(Node* node) {
2       if (node == NULL) {
3           return 0;
4       }
5       return sum(node->left) + node->value + sum(node->right);
6   }
```
Bir ikili arama ağacı olduğu için içinde mutlaka log var diye bir şey yok!

Bunu iki şekilde düşünebiliriz.
<h5>Bu Ne Demektir?</h5>
En basit yol, bu kodun ne anlama geldiğini düşünmektir. Bu kod, ağaçtaki her düğüme bir kez dokunur ve her "dokunma" ile sabit bir işlem yapar (özyineleme çağrıları hariç).

Bu nedenle, zaman karmaşıklığı düğüm sayısına göre doğrusaldır. Eğer N adet düğüm varsa, zaman karmaşıklığı O(N)'dir.

<h5>Özyinelemeli Desen</h5>
Birden çok dallara sahip özyinelliğin çalışma zamanının genellikle O(branchesᵈᵉᵖᵗʰ) olduğunu söyledik. Her çağrıda iki dal var, bu yüzden O(2ᵈᵉᵖᵗʰ) ile karşı karşıyayız.

Bu noktada, birçok kişi bir şeylerin yanlış gittiğini varsayabilir, çünkü üstel bir algoritmaya sahibiz - mantığımızda bir hata olduğunu veya yanlışlıkla üstel bir zaman algoritması oluşturduğumuzu düşünebiliriz (korkunç!).

İkinci ifade doğrudur. Gerçekten üstel bir zaman algoritmamız var, ancak düşündüğümüzden daha kötü değil. Derinlik ne anlama geliyor? Ağaç dengeli bir ikili arama ağacıdır. Bu nedenle, toplam N düğümü varsa, derinlik yaklaşık log N'dir.

Yukarıdaki denklemle O(2ˡᵒᵍ ᴺ) elde ederiz.

log₂'nin neyi ifade ettiğini hatırlayalım.

    2ᵖ = Q  - >   log₂Q  =  P

2ˡᵒᵍ ᴺ nedir? 2 ve log arasında bir ilişki var, bu nedenle bunu basitleştirebilmeliyiz.

P = 2ˡᵒᵍ ᴺ diyelim. log₂'nin tanımı gereği, bu ifadeyi log₂P = log₂N şeklinde yazabiliriz. Bu da P = N olduğu anlamına gelir.

Yani, 2ˡᵒᵍ ᴺ ifadesi N'e eşittir.

    Let P  = 2ˡᵒᵍ ᴺ
      -> log₂P =  log₂N
      -> p  = N
      -> 2ˡᵒᵍ ᴺ  = N

Bu nedenle, bu kodun çalışma zamanı N sayısıyla ifade edildiğinde O(N) şeklindedir, burada N düğüm sayısını temsil etmektedir.

<h5>Örnek 10</h5>
Aşağıdaki metod, sayının kendisinden küçük sayılara bölünebilir olup olmadığını kontrol ederek asal sayı olup olmadığını kontrol eder. Karekökünden büyük bir sayıya bölünebilirlik kontrol edildiği için, sadece kareköküne kadar olan sayılar kontrol edilir. 

Örneğin, 33, 11'den (33'ün karekökünden büyük olan bir sayı) bölünebilirken, 11'in "muadili" 3'tür (3 * 11 = 33). 33, 3 tarafından bir asal sayı olarak zaten elemine edilmiş olacak.

Bu işlevin zaman karmaşıklığı nedir?

```c
1   int isPrime(int n) {
2       for (int x = 2; x * x <= n; x++) {
3           if (n % x == 0) {
4               return 0;
5           }
6       }
7       return 1;
8   }
```
Birçok insan bu soruyu yanlış cevaplıyor. Mantığınızı dikkatli bir şekilde kullanırsanız, oldukça kolaydır.

For döngüsü içindeki işlem sabittir. Bu nedenle, en kötü durumda for döngüsünün kaç kez tekrar edeceğini bilmemiz yeterlidir.

For döngüsü, x = 2 olduğunda başlayacak ve x*x = n olduğunda sona erecektir. Başka bir deyişle, x = √n (x karekökü n kadar olduğunda) duracaktır.

Bu for döngüsü şöyle bir şeydir:

```c
1   int isPrime(int n)  {
2       for (int x =  2;  x <= sqrt(n);  x++)  {
3           if (n % X == 0)  {
4               return false;
5           }
6       }
7       return true;
8   }
```
Bu, O(√n) zamanda çalışır.

<h5>Örnek 11</h5>
Bu kod n! (faktöriyel) hesaplar. Zaman karmaşıklığı nedir?

```c
1   int factorial(int n)  {
2       if (n  <   0)  {
3           return -1;
4       }  else if (n == 0) {
5           return 1;
6       } else {
7           return n  * factorial(n - 1);
8       }
9   }
```
Cevap:
<span class="spoiler">
Bu sadece n'den n-1'e, n-2'ye kadar 1'e doğru düz bir özyinelemeli işlemdir. O(n) zamana ihtiyaç duyacaktır.
</span>

<h5>Örnek 12</h5>
Aşağıdaki java dilindeki kod bir dizinin tüm permütasyonlarını sayar.

```java
1   void  permutation(String str) {
2       permutation(str,  "");
3   }
4   
5   void  permutation(String str,  String prefix) {
6       if (str.length() ==  0)  {
7           System.out.println(prefix);
8       } else {
9           for (int i = 0; i < str.length();  i++)   {
10              String rem  =  str.substring(0, i) + str.substring(i + 1);
11              permutation(rem, prefix  + str.charAt(i));
12          }
13      }
14  }
```
Bu oldukça zorlu bir soru. Permütasyonun kaç kez çağrıldığını ve her çağrının ne kadar sürdüğünü düşünerek çözebiliriz. En dar üst sınıra ulaşmaya çalışacağız.

<h5>Permütasyonun temel durumunda kaç kez çağrılır?</h5>

Bir permütasyon oluşturacak olsaydık, her "slot" için karakterler seçmemiz gerekecekti. Diyelim ki dizide 7 karakter var. İlk yuvada 7 seçeneğimiz var. Orada harfi seçtikten sonra, bir sonraki yuvada 6 seçeneğimiz olacak. (Not edilmesi gereken şey, önceden 7 seçenek için 6 seçeneğimizin olmasıdır.) Sonra bir sonraki yuva için 5 seçenek, ve böyle devam eder.

Bu nedenle, toplam seçenek sayısı 7 * 6 * 5 * 4 * 3 * 2 * 1, ayrıca 7! (7 faktöriyel) olarak ifade edilir.

Bu bize n! permütasyonun olduğunu söyler. Bu nedenle, permütasyon tam permütasyon olduğunda (prefix tam permütasyon olduğunda), temel durumunda n! kez çağrılır.

<h5>Temel durumundan önce permütasyon kaç kez çağrılır?</h5>

Ancak, tabii ki, 9-12. satırların kaç kez tetiklendiğini de hesaba katmamız gerekiyor. Tüm çağrıları temsil eden büyük bir çağrı ağacını düşünün. Yukarıdaki gibi n! yapraklar vardır. Her yaprak, n uzunluğundaki bir yolun bir parçasıyla ilişkilidir. Bu nedenle, bu ağaçta hiçbir zaman n * n! 'dan daha fazla düğüm (fonksiyon çağrısı) olmayacağını biliyoruz.

<h5>Her fonksiyon çağrısı ne kadar sürer?</h5>

Satır 7'nin yürütülmesi O(n) zaman alır, çünkü her karakter yazdırılmalıdır.

10.satır ve 11. satır birleştirildiğinde, dize birleştirme nedeniyle O(n) zaman alacaktır. Kalan, prefix ve str.charAt (i) 'nin uzunluklarının toplamı her zaman n olacaktır.
Bu nedenle, çağrı ağacındaki her düğüm O(n) işleme karşılık gelir.

<h5>Toplam çalışma süresi nedir?</h5>

Permütasyonu O(n * n!) kez (üst sınır olarak) çağırdığımızdan ve her biri O(n) zaman aldığından, toplam çalışma süresi O(n² * n!) 'den fazla olmayacaktır.

Daha karmaşık matematiksel hesaplamalarla, daha sıkı bir çalışma zamanı denklemi türetebiliriz (ancak bu, normal bir mülakatın kapsamı dışında olacaktır).

<h5>Örnek 13</h5>
Aşağıdaki kod N. Fibonacci sayısını hesaplar.

```java
1   int fib(int n)  {
2       if (n  <=   0)  return  0;
3       else if (n  ==  1)  return 1;
4       return fib(n  -  1)  + fib(n -  2);
5   }
```
Cevap:
<span class="spoiler">
Daha önce recursive çağrılar için belirlediğimiz deseni kullanabiliriz: O(branchesᵈᵉᵖᵗʰ).<br>
Her çağrıda 2 dal var ve N kadar derin gidiyoruz, bu nedenle çalışma zamanı O(2ᴺ)'dir.
</span>

> Gerçekten çok karmaşık matematikler kullanarak daha sıkı bir çalışma zamanı elde edebiliriz. Zaman gerçekten üstel, ancak aslında O(1.6ᴺ)'ye daha yakındır. O(2ᴺ) olmamasının nedeni, çağrı yığınının en altında bazen sadece bir çağrı olmasıdır. Çok sayıda düğümün alt kısmında olduğu (genellikle ağaçlarda olduğu gibi) bu tek veya çift çağrıların aslında büyük bir fark yarattığı ortaya çıkar. Mülakat kapsamı için O(2ᴺ) yeterli olur, teknik olarak doğrudur. Aslında bundan daha az olacağını fark edebilirseniz "bonus puanlar" alabilirsiniz.

Genel olarak, birden fazla recursive çağrısı olan bir algoritma gördüğünüzde, üstel bir çalışma zamanına bakıyorsunuz demektir.

<h5>Örnek 14</h5>
Aşağıdaki kod 0'dan n'ye kadar tüm Fibonacci sayılarını yazdırır. Zaman karmaşıklığı nedir?

```c
1 int fib(int n) {
2    if (n <= 0) {
3        return 0;
4    } else if (n == 1) {
5        return 1;
6    } else {
7        return fib(n - 1) + fib(n - 2);
8    }
9 }
10
11 void allFib(int n) {
12    for (int i = 0; i < n; i++) {
13        printf("%d: %d\n", i, fib(i));
14    }
15 }
```
Çoğu kişi fib(n) fonksiyonunun O(2ⁿ) zaman aldığını ve bu fonksiyonun n defa çağrıldığına göre, bunun O(n2ⁿ) olduğu sonucuna varmaya çalışacaklardır.

Ancak acele etmeyin. Bu mantıkta bir hata var mı bulabilir misiniz?

Hata, n değişkeninin değişmesidir. Evet, fib(n) fonksiyonu O(2ⁿ) zaman alır, ancak bu n değerinin ne olduğu önemlidir.

Bunun yerine, her çağrıyı tek tek inceleyelim.

```
fib(1) ->  2¹ steps 
fib(2) ->  2² steps 
fib(3) ->  2³ steps 
fib(4) ->  2⁴ steps
...
fib(n) ->  2ⁿ steps
```
Therefore, the total amount of work is:
```
2¹   +  2²   +  2³   +  2⁴   +  ...  +  2ⁿ
```

İlk n Fibonacci sayısını (bu korkunç algoritmayı kullanarak) hesaplamak için çalışma zamanı hala O(2ⁿ) dir.

<h5>Örnek 15</h5>
Bu kod, 0'dan n'e kadar olan tüm Fibonacci sayılarını yazdırır. Ancak bu sefer, önceden hesaplanmış değerleri bir tamsayı dizisinde saklar (yani önbelleğe alır). Eğer daha önce hesaplandıysa, önbelleği döndürür. Zaman karmaşıklığı nedir?

```c
1  int fib(int n, int memo[]) {
2     if (n <= 0) return 0;
3     else if (n == 1) return 1;
4     else if (memo[n] > 0) return memo[n];
5     memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
6     return memo[n];
7  }
8
9  void allFib(int n) {
10     int memo[n + 1];
11     for (int i = 0; i < n; i++) {
12         printf("%d: %d\n", i, fib(i, memo));
13     }
14  }
```
Bu algoritmanın ne yaptığını adım adım inceleyelim.
```
fib(1) ->  return 1
fib(2)
    fib(1) ->  return 1 
    fib(0) ->  return 0 
    store 1  at memo[2]
fib(3)
    fib(2) ->  lookup memo[2]   ->  return 1 
    fib(1) ->  return 1
    store 2  at memo[3]
fib(4)
    fib(3) ->  lookup  memo[3]   ->  return 2 
    fib(2) ->  lookup  memo[2]   ->  return 1 
    store 3  at memo[4]
fib(5)
    fib(4) ->  lookup memo[4]   ->  return  3 
    fib(3) ->  lookup memo[3]   ->  return  2 
    store 5  at memo[5]
```
Her bir fib(i) çağrısında, fib(i-1) ve fib(i-2) değerlerini zaten hesaplamış ve saklamışız. Bu değerlere bakıyoruz, topluyoruz, yeni sonucu saklıyoruz ve geri döndürüyoruz. Bu işlem sabit bir zaman alır.

N defa sabit miktarda işlem yapıyoruz, bu nedenle zaman karmaşıklığı O(n)'dir.

Bu teknik, memoization olarak adlandırılan, üstel zamanlı özyinelemeli algoritmaları optimize etmek için çok yaygın olarak kullanılan bir tekniktir.
<h5>Örnek 16</h5>
Aşağıdaki fonksiyon, n dahil olmak üzere 1'den n'e kadar olan 2'nin üstlerini ekrana yazdırır. Örneğin, n 4 ise 1, 2 ve 4'ü yazdırır.Zaman karmaşıklığı nedir?

```c
1 int powersOf2(int n) {
2    if (n < 1) {
3        return 0;
4    } else if (n == 1) {
5        printf("%d\n", 1);
6        return 1;
7    } else {
8        int prev = powersOf2(n / 2);
9        int curr = prev * 2;
10        printf("%d\n", curr);
11        return curr;
12    }
13 }
```
Bu çalışma süresini hesaplayabileceğimiz birkaç yöntem var.

<h5>Ne İşe Yarar</h5>

powersOf2(50) gibi bir çağrıyı inceleyerek adım adım ilerleyelim.

```
powersOf2(50)
    ->  powersOf2(25)
        ->  powersOf2(12)
            ->  powersOf2(6)
                ->  powersOf2(3)
                    ->  powersOf2(1)
                        ->  print &   return 1
                    print &   return  2
                print &   return  4
            print &  return  8 print &  return 16
        print &   return  32
```     
O zaman çalışma süresi, 50'yi (veya n'yi) temel duruma (1) ulaşana kadar 2'ye bölebileceğimiz sayıdır. Sayfada 44'te tartıştığımız gibi, n'yi 1'e kadar yarıya bölebileceğimiz sayı O(log n)'dir.

<h5>Bunun Ne Anlama Geliyor?</h5>

Ayrıca, kodun ne yapması gerektiğini düşünerek çalışma süresine yaklaşabiliriz. Kod, 1'den n'e kadar olan 2'nin üstlerini hesaplaması gerekiyor.

Her powersOf2 çağrısı, tam olarak bir sayının yazdırılması ve döndürülmesiyle sonuçlanır (özyinelemeli çağrılarda neler olduğu hariç). Bu durumda, algoritma 13 değeri yazdırırsa, powersOf2 13 kez çağrılmıştır.

Bu durumda, bize 1 ile n arasındaki tüm 2'nin üstlerini yazdırdığı söyleniyor. Bu nedenle, fonksiyonun çağrılma sayısı (yani çalışma süresi), 1 ile n arasındaki 2'nin üslerinin sayısına eşit olmalıdır.

1 ve n arasında log n tane 2'nin üssü vardır. Bu nedenle, çalışma süresi O(log n)'dir.

<h5>Artış Hızı</h5>

Çalışma süresine yaklaşmanın son bir yolu, n büyüdükçe çalışma süresinin nasıl değiştiğini düşünmektir. Sonuçta, bu tam olarak büyük O zamanın ne anlama geldiğidir.

N, P'den P+1'e gittiğinde, powersOfTwo'a yapılan çağrı sayısı hiç değişmeyebilir. PowersOfTwo'a yapılan çağrı sayısı ne zaman artar? Her n iki katına çıktığında 1 artar.

Yani her iki katına çıktığında, powersOfTwo'a yapılan çağrı sayısı 1 artar. Bu nedenle, powersOfTwo'a yapılan çağrı sayısı, n'ye kadar 1'i iki katına çıkarabileceğiniz sayıdır. Denklemdeki x, 2^x = n'dir.

x'in değeri nedir? x'in değeri log n'dir. Bu tam olarak x = log n ile kastettiğimiz şeydir.

Bu nedenle, çalışma süresi O(log n)'dir.

---

<h3 id="13">Ek Problemler</h3>

---
**V1.1: Aşağıdaki kod, a ve b'nin çarpımını hesaplar. Zaman karmaşıklığı nedir?**

```c
int product(int a, int b)   {
    int sum  =  0;
    for (int i = 0; i < b;  i++)  {
        sum  +=  a;
    }
    return sum;
}
```
**V1.2: Aşağıdaki kod aᵇ'yi hesaplar. Zaman karmaşıklığı nedir?**

```c
int power(int a, int b) {
    if (b < 0) {
        return 0; // hata
    } else if (b == 0) {
        return 1;
    } else {
        return a * power(a, b - 1);
    }
}
```
**V1.3: Aşağıdaki kod, a%b işlemini hesaplar.**

```c
int mod(int  a,  int b)  {
    if (b <=  0) {
        return  -1;
    }
    int div  = a /  b;
    return a  -  div  * b;
}
```
**V1.4: Aşağıdaki bu kod bölme işlemini gerçekleştirir. Diyelim ki a ve b pozitif sayılardır. Kodun çalışma süresi nedir?**

```c
int bolme(int a, int b) {
    int sayac  =  0;
    int toplam =  b;
    while (toplam <=  a)  {
        toplam  +=  b;
        sayac++;
    }
    return  sayac;
}
```
**V1.5: Aşağıdaki kod, bir sayının [tamsayı] karekökünü hesaplar. Eğer sayı mükemmel kare değilse (tamsayı karekökü yoksa), -1 döndürür. Bunun için ardışık tahminler yapar. Örneğin, n=100 ise önce 50 tahmin edilir. Çok yüksek mi? Daha düşük bir şey deneyin - 1 ve 50'nin arasındaki yarıya bakın. Kodun çalışma süresi nedir?**

```c
#include<stdio.h>

int sqrt_helper(int n, int min, int max);

int sqrt(int n) {
    return sqrt_helper(n, 1, n);
}

int sqrt_helper(int n, int min, int max) {
    if (max < min) {
        return -1; // karekök yok
    }

    int guess = (min + max) / 2;
    if (guess * guess == n) { // bulundu!
        return guess;
    } else if (guess * guess < n) { // çok düşük
        return sqrt_helper(n, guess + 1, max); // daha yüksek deneyin
    } else { // çok yüksek
        return sqrt_helper(n, min, guess - 1); // daha düşük deneyin
    }
}

int main() {
    int n = 100;
    int result = sqrt(n);
    printf("sqrt(%d) = %d", n, result);
    return 0;
}
```

**V1.6: Aşağıdaki kod, bir sayının [tam] karekökünü hesaplar. Sayı tam bir karekök değilse (yani tam bir karekök yoksa), doğru değeri bulana kadar giderek artan sayıları dener (veya çok yüksek olur). Çalışma zamanı kaçtır?**

```c
#include <stdio.h>

int sqrt(int n)  {
    for (int guess  = 1;  guess  * guess  <=  n;  guess++)  {
        if (guess  *  guess  ==  n)  {
            return  guess;
        }
    }
    return  -1;
}

int main() {
    int num;
    printf("Bir sayı girin: ");
    scanf("%d", &num);
    int result = sqrt(num);
    if (result == -1) {
        printf("Bu sayının tam bir karekökü yok.");
    } else {
        printf("Karekök: %d", result);
    }
    return 0;
}
```
**VI.7: Eğer bir ikili arama ağacı dengeli değilse, bir elemanın bulunması (en kötü durumda) ne kadar sürer? Bunun zaman karmaşıklığı nedir?**

**VI.8: Bir binary tree'de belirli bir değeri arıyorsunuz, ancak ağaç bir ikili arama ağacı değil. Bunun zaman karmaşıklığı nedir?**

**VI.9: appendToNew yöntemi, yeni ve daha uzun bir dizi oluşturarak bir diziye bir değer ekler ve bu daha uzun diziyi döndürür. copyArray fonksiyonunu oluşturmak için appendToNew yöntemini tekrar tekrar çağırdınız. Bir dizinin kopyalanması ne kadar sürer?**

```c
int* copyArray(int* array, int length) {
    int* copy = (int*) malloc(sizeof(int));
    for (int i = 0; i < length; i++) {
        copy = appendToNew(copy, array[i], i+1);
    }
    return copy;
}

int* appendToNew(int* array, int value, int size) {
    int* bigger = (int*) realloc(array, sizeof(int) * size);
    bigger[size - 1] = value;
    return bigger;
}
```

**VI.10: Aşağıdaki kod bir sayıdaki rakamları toplar. Big O zaman karmaşıklığı nedir?**

```c
int sumDigits(int n) {
    int sum = 0;
    while (n > 0) {
        sum += n % 10;
        n /= 10;
    }
    return sum;
}
```

**VI.11: Aşağıdaki kod, karakterleri sıralanmış olan uzunluğu k olan tüm dizeleri yazdırır. Bunun için, uzunluğu k olan tüm dizeleri oluşturur ve ardından her birinin sıralanıp sıralanmadığını kontrol eder. Bu kodun çalışma süresi nedir? int numChars = 26;**

```c
#define NUM_CHARS 26

void printSortedStrings(int remaining, char* prefix);
bool isinOrder(char* s);
char ithLetter(int i);

void printSortedStrings(int remaining, char* prefix) {
    if (remaining == 0) {
        if (isinOrder(prefix)) {
            printf("%s\n", prefix);
        }
    } else {
        for (int i = 0; i < NUM_CHARS; i++) {
            char c = ithLetter(i);
            char* newPrefix = (char*) malloc((remaining+1)*sizeof(char));
            sprintf(newPrefix, "%s%c", prefix, c);
            printSortedStrings(remaining-1, newPrefix);
            free(newPrefix);
        }
    }
}

bool isinOrder(char* s) {
    for (int i = 1; i < strlen(s); i++) {
        int prev = ithLetter(s[i - 1]);
        int curr = ithLetter(s[i]);
        if (prev > curr) {
            return false;
        }
    }
    return true;
}

char ithLetter(int i) {
    return 'a' + i;
}
```
**V1.12 Aşağıdaki kod, iki dizinin kesişimini (ortak eleman sayısını) hesaplar. Her iki dizinin de yinelenen elemanları olmadığı varsayılır. Kesişimi hesaplamak için bir diziyi (dizi b) sıralayarak ve ardından dizi a'yı işlem yaparak her bir değerin dizi b'de olup olmadığını (binary arama kullanarak) kontrol eder. Bu algoritmanın çalışma süresi nedir?**

```c
int intersection(int a[], int b[], int size_a, int size_b) {
    mergesort(b, size_b);
    int intersect = 0;

    for (int i = 0; i < size_a; i++) {
        if (binarySearch(b, size_b, a[i]) >= 0) {
            intersect++;
        }
    }

    return intersect; 
}
```
---

Çözümler

---

1. O(b). For döngüsü sadece b üzerinden yinelemeler yapar.
2. O(b). Recursive kod, her seviyede bir azaltırken b üzerinden yinelemeler yapar.
3. O(1). Sabit miktarda iş yapar.
4. O(a/b). Değişken sayısı sonunda X'e eşit olacaktır. While döngüsü X kez yinelemeler yapar.
5. O(log n). Bu algoritma, kökü bulmak için temel olarak ikili arama yapıyor. Bu nedenle, çalışma süresi O(log n) olacaktır.
6. O(sqrt(n)). Bu sadece, tahmini tahmini n'nin karekökünden büyük olduğunda (veya başka bir deyişle, tahmin> sqrt (n)) durduğu basit bir döngüdür.
7. O(n), burada n ağaçtaki düğüm sayısıdır. Bir eleman bulmak için maksimum zaman, ağacın derinliğidir. Ağaç aşağı doğru düz bir liste olabilir ve derinliği n olabilir.
8. O(n). Düğümlerde herhangi bir sıralama özelliği olmadığı için tüm düğümleri aramak zorunda kalabiliriz.
9. O(N²), burada n dizideki eleman sayısıdır. appendToNew için ilk çağrı 1 kopya alır. İkinci çağrı 2 kopya alır. Üçüncü çağrı 3 kopya alır. Ve böyle devam eder. Toplam süre 1'den n'ye kadar olan toplamın toplamı olacaktır, bu da O(N²) olacaktır.
10. O(log n). Çalışma süresi sayıdaki basamak sayısı olacaktır. d basamağı olan bir sayı 10ᵈ değerine sahip olabilir. n = 10ᵈ ise, o zaman d = log n olacaktır. Bu nedenle, çalışma süresi O(log n) olacaktır.
11. O(kcᵏ), burada k dize uzunluğu ve c alfabe karakter sayısıdır. Her dize oluşturmak için O(cᵏ) süre gereklidir. Daha sonra, bunların her birinin sıralanıp sıralanmadığını kontrol etmemiz gerekiyor, bu da O(k) zaman alır.
12. O(b log b + a log b). İlk önce dizi b'yi sıralamamız gerekiyor, bu da O(b log b) süre alır. Ardından, a'nın her bir elemanı için, O(log b) sürede ikili arama yapıyoruz. İkinci kısım, O(a log b) süre alır.



[bigocheatsheet](https://www.bigocheatsheet.com/)<br>
