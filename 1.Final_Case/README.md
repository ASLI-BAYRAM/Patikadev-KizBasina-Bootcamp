# AIRLINE PASSENGER SATISFACTION VERİ SETİNİN ANALİZİ
Bu klasör, Patika Dev  Kız Başına Bootcamp final projesini içermektedir.

## VERİ SETİ HİKAYESİ
Veri seti bir havayolu şirketine ait yolcu anketlerinden elde edilmiştir. Yolcuların uçuş öncesi, sırası ve sonrası deneyimlerine dair değerlendirmeleri, memnuniyet durumu ile birlikte sunulmuştur. Hedef değişkenimiz, yolcunun **memnuniyet durumudur** (`satisfied` veya `neutral/dissatisfied`).Uçak yolcularının seyahat sürecine dair yaşadığı deneyimleri (hizmet kalitesi, konfor, gecikme süresi, rezervasyon kolaylığı gibi) analiz ederek, hangi faktörlerin memnuniyet üzerinde en çok etkili olduğunu ortaya koymaktır.

## KULLANILAN VERİ SETİ
Kaynak: [Kaggle - Airline Passenger Satisfaction](https://www.kaggle.com/datasets/teejmahal20/airline-passenger-satisfaction)

**Veri Setinde Bulunan Değişkenler:**

id:	Kimlik Numarası / Yolcu ID

Gender:	Cinsiyet

Customer Type:	Müşteri Türü

Age:	Yaş

Type of Travel:	Seyahat Türü

Class:	Uçuş Sınıfı

Flight Distance:	Uçuş Mesafesi

Inflight wifi service:	Uçak İçi Wi-Fi Hizmeti

Departure/Arrival time convenient:	Kalkış/Varış Saati Uygunluğu

Ease of Online booking:	Çevrimiçi Rezervasyon Kolaylığı

Gate location:	Kapı Konumu / Kapıya Uzaklık

Food and drink:	Yiyecek ve İçecek Hizmeti

Online boarding:	Çevrimiçi Biniş İşlemi

Seat comfort:	Koltuk Konforu

Inflight entertainment:	Uçak İçi Eğlence

On-board service:	Uçuş Sırasındaki Hizmet

Leg room service:	Bacak Mesafesi Hizmeti

Baggage handling:	Bagaj İşlemleri

Checkin service:	Check-in Hizmeti

Inflight service:	Uçak İçi Hizmetler

Cleanliness:	Temizlik

Departure Delay in Minutes:	Kalkış Gecikmesi (Dakika)

Arrival Delay in Minutes:	Varış Gecikmesi (Dakika)

satisfaction:	Memnuniyet

##  UYGULANAN ADIMLAR
Projeye başlamadan önce test ve train olarak ayrılan veri setleri birleştirilmiştir. Birleştirmesindeki amaç özellik mühendisliği ve veri analizi gibi adımlarının tüm veri üzerinde tutarlı biçimde uygulanabilmesini sağlamaktır.

Birleştirilmiş veri setinde toplamda 129880 gözlem, 24 adet değişken bulunmaktadır.Veri setinde sayısal, kategorik ve float veri tipinde değişkenler mevcut. Bazı değişkenler 1-5 arasında memnuniyet skorları ile puanlandırılmıştır. Bunlar sayısal veri olarak görünsede aslında kategorik değişkendir. Analiz yaparken bunlar kategorik değişken olarak değerlendirilicektir.

**ADIM 1: SAYISAL VE KATEGORİK DEĞİŞKENLERİN BELİRLENMESİ**

Veri setinde yer alan değişkenlerin türleri, uygulanacak analiz yöntemlerinin belirlenmesi açısından büyük önem taşımaktadır. Bu nedenle analiz sürecine başlamadan önce, değişkenleri veri tiplerine göre sınıflandırmak hedeflenmiştir.Kod kısmı py. uzantılı dosyada bulunmaktadır. 

**ADIM 2: İSTATİSTİKSEL ÖZET**
Veri setine ait temel istatistiksel analiz, değişkenlerin dağılımı, merkezi eğilim ölçüleri ve aykırı değerlerin ilk tespiti amacıyla yapılmıştır.Sayısal değişkenlerde ortalama, medyan, minimum ve maksimum değerler incelenmiştir.Flight Distance, Departure Delay, Arrival Delay gibi değişkenlerde geniş dağılım gözlemlenmiştir.

Inflight wifi service, Seat comfort, On-board service gibi derecelendirme değişkenlerinde genellikle 1–5 arası değerler mevcuttur ve bu dağılım müşteri tercihlerini analiz etmede kullanılmıştır.

**ADIM 3: EKSİK DEĞER ANALİZİ**
Eksik değer, bir veri setinde bazı gözlemlerin belirli değişkenler için bilgi içermemesi durumudur. Yani bir hücrede beklenen veri yoksa, bu eksik değer (missing value) olarak adlandırılır.Eksik değerler birçok nedenle ortaya çıkmış olabilir. Eksik değerleri tespit ettikten sonra bunlara nasıl müdahale edileceğine karar verilmelidir.

Veri setimizde Arrival Delay in Minutes değişkeninde 393 tane eksik değer bulunmaktadır. Burada eksik değerlere herhangi bir müdahalede bulunulmamıştır.Dilersek eksik değer probleminin çözülmesi için aşağıdaki yöntemlerden birini tercih edebiliriz:

* Veri seti gözlem açısından zengin ise eksik değerleri veri setinden silebiliriz.
* Basit atama yöntemleri ile eksik değerleri doldurabiliriz.Arrival Delay in Minutes sayısal bir değişken eksik değerleri bu değişkenin medianı yada ortalaması ile doldurmayı tercih edebiliriz.
* Kategorik değişken kırılımlarında değer atayabiliriz. Örneğin cinsiyete göre kırılım alıp ortalaması ile doldurmak gibi ya da Type of Travel değişkenine göre kırılım yapıp ortalama ya da medaianı ile doldurmak gibi.
* Tahmine Dayalı Atama ile Doldurma (Bir makine öğrenmesi modeli tekniği oluşturarak tahmine dayalı doldurma)

**ADIM 4: AYKIRI  DEĞER ANALİZİ**
Aykırı değer, bir veri setinde diğer gözlemlerden önemli ölçüde farklı olan, yani ortalamanın çok dışında kalan veri noktalarıdır.Bu değerler genellikle verideki hatalardan, nadir olaylardan, ya da gerçekten var olan olağandışı durumlardan kaynaklanır. Biz aykırı değerleri IQR yöntemi ve box plot yöntemlerini kullanarak inceledik.Elde ettiğimiz sonuç aşağıdaki gibidir:

* Flight Distance: 2855 aykırı değer var (2.20%)
* Departure Delay in Minutes: 18098 aykırı değer var (13.93%)
* Arrival Delay in Minutes: 17492 aykırı değer var (13.47%)

Analiz sonucunda elde ettiğimiz aykırı değerleri veri setininin yapısını bozmadan baskılamayı tercih edebiliriz.

**ADIM 5: DEĞİŞKENLERİN GÖRSELLEŞTİRİLMESİ**
Kategorik değişkenlerin analizinde sütun grafik (barplot) kullanılarak, her bir kategorinin sınıf frekansları görselleştirdik. Ayrıca, her bir sınıfın toplam veri seti içindeki oranları hesaplayarak, değişkenlerin dağılım dengesi ve veri setindeki temsil düzeyleri değerlendirilmiştir. Bu sayede dengesiz sınıfların (class imbalance) tespiti yapılmıştır.Değişkenler hakkında yapılan yorumlara py. uzantılı dosyada yer verilmiştir.

Sayısal değişkenlerin dağılımını analiz etmek amacıyla seaborn.histplot() fonksiyonu kullanılmıştır. Histogramlar 10 eşit aralığa bölünmüş (bins=10) ve dağılımın yoğunluğu kde=True parametresi ile gösterilmiştir.
Bu sayede her değişkenin dağılım tipi, simetrik olup olmadığı ve olası çarpıklık durumu görsel olarak değerlendirilmiştir. Bu bilgiler, aykırı değer analizi ve uygun dönüşüm yöntemlerinin belirlenmesinde yol gösterici olmuştur.

**SONUÇ**
Bu çalışmada, yolcu memnuniyeti verileri detaylıca analiz edilmiştir. Verinin yapısı ve değişkenlerin dağılımı grafiklerle incelenmiş, eksik ve aykırı değerler tespit edilmiştir. Elde edilen bulgular, veriyi daha iyi anlamamızı sağlamış ve ileride yapılacak modelleme çalışmaları için temel oluşturmuştur.
