[İsteklerin Kontrol Edilmesi](#)
--------------------------------

  

    [×](#) **Bunları biliyor muydunuz?**  
"Konsoldan 'php zerocore create-grand-vision' gibi basit bir komutla tüm veritabanı ve tablolarının model dosyasını oluşturabilirsiniz."

* * *

Kontrolcüler, kullanıcı isteklerine göre duruma bağlı olarak model ile etkileşime girip ilgili görünümün çağrılması için kullanılan ve Nesne Yönelimli Proglama (OOP) ile tasarlanan sınıflardır. Kullanıcıların URL istekleri, bu sınıfların ilgili yöntemlerine yapılır. Bu URL istekleri bir sınıfa ait yöntemi çalıştırır. Kullanıcıların ilk etkileşime girdiği yapılar kontrolcüler olduğu için anlatıma bu bölüme başlıyoruz.

**Dizin:** Projects/Any/Controllers/

**Not:** Anlatımda kullanılan URL örneklerini localhost üzerinde çalıştığınız varsayılarak verilmiştir.

#### # Bölüm Başlıkları

* * *

> **# [Basit Bir Kod Çalıştırmak](#Basit Bir Kod Çalıştırmak)**
> 
> ● [Kontrolcü Bölümü](#controller-segment)  
> ● [Kontrolcü Yöntemi Bölümü](#controller-method-segment)  
> ● [Parametreler Bölümü](#controller-method-parameters-segment)  
> ● [Otomatik Enjeksiyon Çözümleme](#automatic-injection-resolving) (ZN >= 5.7.7)  
> ● [Ajax İsteklerinin Kontrolü](#control-of-ajax-requests) (ZN >= 6.0.2.0)
> 
> **# [Varsayılan Açılış Kontrolcüsü](#Varsayılan Açılış Kontrolcüsü)  
> # [Başlangıç Kontrolcüleri](#starting-controllers)**
> 
> ● [Hariç Tutma](#exclude)  
> ● [Dahil Tutma](#include)  
> ● [Çoklu Başlangıç Kontrolcüsü Kullanma](#multi-starting-controllers)  
> ● [Alt Kontrolcülere Data Gönderimi](#send-data-subcontroller)
> 
> **# [Kontrolcü Restorasyonu](#controller-restoration)**
> 
> ● [Yapılandırma](#configurations)  
> ● [Restore Sabiti](#const-restore)

#### # [Basit Bir Kod Çalıştırmak](#Basit Bir Kod Çalıştırmak)

* * *

Aşağıda _"Welcome to World of ZN"_ iletisini veren örnek bir kod yer almaktadır. Sizde aşağıda yolu belirtilen dizine aynı isimle Blog.php dosyası oluşturup içeriği aşağıdaki gibi düzenleyin.

**Dosya:** Projects/Frontend/Controllers/Blog.php

    <?php namespace Project\Controllers;
    
    class Blog extends Controller
    {
        public function main()
        {
            echo "Welcome to World of ZN";
        }
    }

Bu kodu çalıştırmak için adres çubuğuna girilmesi gereken URL aşağıdadır.

**Çalıştır:** localhost/blog/main veya localhost/blog

Welcome to World of ZN

Kontrolcü Bölümü

ZN'nin mevcut ön tanımlı kontrolcüsü Home.php dir. Ve bu kontrolcü içinde  main yöntemi bulunmaktadır. URL üzerinden yapılan isteklerde main ibaresinin adres çubuğunda kullanımına gerek yoktur. Home.php içerisinde yer alan main yöntemini çalıştırmak için adres çubuğuna localhost/home yazılması yeterlidir.

**Dosya:** Projects/Frontend/Controllers/Blog.php

    <?php namespace Project\Controllers;
    
    class Blog extends Controller
    {
        public function main()
        {
            echo 'Home Page';
        }
    }

**Çalıştır:** localhost/blog

Kontrolcü Yöntemi Bölümü

Adres çubuğuna birinci bölüme erişilecek kontrolcünün dosya adı, ikinci bölüme ise o kontrolcüye ait çalıştırılacak yöntem adı yazılır. Eğer yöntem ismi main ise URL üzerinde belirtilmesine gerek yoktur.

**Dosya:** Projects/Frontend/Controllers/Blog.php

    <?php namespace Project\Controllers;
    
    class Blog extends Controller
    {
        public function main()
        {
            echo 'Welcome to World of ZN';
        }
    
        public function comments()
        {
            echo 'Run Now!';
        }
    }

Yukarıda yer alan comments yöntemini çalıştırmak için URL adresimizi şu şekilde düzenliyoruz.

**Çalıştır:** localhost/blog/comments

Main yöntemini çalıştırmak için URL adresine kontrolcü adını yazmanız yeterlidir.

**Çalıştır:** localhost/blog

Parametreler Bölümü

URL üzerinden yöntemlere parametre göndermek için URL adresinin 3. ve sonraki bölümleri kullanılır. Eğer parametre gönderimi yapılan main yöntemi ise 2. ve sonraki bölümler parametre olarak kullanılır. URL üzerinden gönderilen parametrik değerleri ilgili yöntemin parametreleri tutar. Aşağıdaki örnekte gelen parametrelerin nasıl kullanılabileceği gösterilmiştir.

**Dosya:** Projects/Frontend/Controllers/Products.php

    <?php namespace Project\Controllers;
    
    use Output;
    
    class Products extends Controller
    {
        public function main($price, $value)
        {
            Output::write('{0} - {1}', [$price, $value]);
        }
    
        public function computer($price, $value)
        {
            Output::write('{0} - {1}', [$price, $value]);
        }
    }

**Çalıştır:** localhost/products/computer/price/1000

price - 1000

Main yöntemine istek yapacaksanız yöntem adını kullanmanız gerekli değildir.

**Çalıştır:** localhost/products/price/5000

price - 5000

Otomatik Enjeksiyon Çözümleme (ZN >= 5.7.7)

ZN Framework belirtilen sürüm itibari ile kontrolcü yöntemlerine nesne enjeksiyonu yapmaya izin verir. Yani herhangi bir kütüphaneyi yöntemlerde parametre olarak çağırabilirsiniz.

**Dosya:** Projects/Frontend/Controllers/Products.php

    <?php namespace Project\Controllers;
    
    class Products extends Controller
    {
        protected $database;
    
        public function __construct(\DB $db)
        {
            $this->database = $db;
        }
    
        public function main(\Post $post, \Get $get)
        {
            $post::name('Example');
        }
    }

Dikkat edilirse yöntemlerin içerisine belirtilen kütüphaneler otomatik enjeksiyon çözümlemesi sayesinde kullanılabilmektedir.

**Uyarı:** Bu kullanım standart URI parametre gönderimini yok sayar. Bu nedenle parametrik değerleri kullanabilmek için URI:: kütüphanesinin kullanımı tavsiye edilir.

Otomatik çözümleme ile aynı zamanda parametre ile belirtilen kütüphaneler belirtilen değişken isimleri ile görünümlerin içerisinde de kullanılabilir.

**Dosya:** Projects/Frontend/Views/Products/main.wizard.php

    {{ $post::name() }}

Example

Ajax İsteklerinin Kontrolü (ZN >= 6.0.2.0)

Kontrolcü yönteminin **return type** değeri void olarak ayarlanarak ajax kontrolü eklenebilir. Böylece bu yönteme ajax dışında yapılan istekler exit ile sonlandırılarak işleme alınmaz.

**Dosya:** Projects/Frontend/Controllers/Home.php

    <?php namespace Project\Controllers;
    
    use Http;
    
    class Home extends Controller
    {
        public function ajaxControlProcess() : void
        {
            # your codes...
        }
    }

#### # Varsayılan Açılış Kontrolcüsü

* * *

ZN kod çatısında varsayılan olarak ayarlanmış açılış kontrolcüsü Home.php dosyasıdır. Açılış kontrolcüsünü URL üzerinde belirtmenize gerek yoktur. Bu nedenle URL adresine localhost/ yazıldığında doğrudan bu kontrolcü çalışmaktadır. Bunu değiştirmek için Config/Routing.php dosyasını açıp aşağıdaki openController ayarını değiştirmeniz yeterlidir.

**Dosya:** Projects/Frontend/Config/Routing.php

    'openController' => 'home'

#### # Başlangıç Kontrolcüleri

* * *

Tüm kontrolcülerden önce tüm sistem için geçerli olacak kodlar çalıştırmak isteyebilirsiniz. Mevcut kontrolcülerinizden birini sistemin tümünde çalışacak kodları yazmak için kullanabilirsiniz. Başlangıçta çalıştırılacak kontrolcüler aşağıdaki yapılandırma dosyasından belirtilir.

**Dosya:** Config/Starting.php

**Başlangıç Kontrolcüleri**

mixed

$constructors = 'Initialize'

Tüm kontrolcüler üzerinde geçerli ve önce çalışan kontrolcüleri belirtmek için kullanılır. Ön tanımlı olarka Initialize:: kontrolcüsü tanımlıdır. Controllers/ dizini içine bakılırsa Initizalize.php kontrolcüsünün var olduğunu görebilirsiniz.

mixed

$destructors

Tüm kontrolcüler üzerinde geçerli ve sonra çalışan kontrolcüleri belirtmek için kullanılır.

Eğer birden fazla kontrolcü veya aynı kontrolcüye bağlı fonksiyon çalıştıracaksanız değeri dizi olarak belirtmeniz gerekir.

    'constructors' => ['StartingController1:functionName', 'StartingController2:functionName']

Aşağıda örnek bir kullanıma yer verilmiştir.

**File:** Controllers/Initialize.php

    <?php namespace Project\Controllers;
    
    use User;
    
    class Initialize extends Controller
    {
        public function main()
        {
            if( CURRENT_CFPATH !== 'user/login' && ! User::isLogin() )
            {
                redirect('user/login');
            }
        }
    }

**Not:** Fonksiyon adı main() ise yapılandırmada belirtmeye gerek yoktur.

**Hariç Tutma (ZN >= 5.2.0)**

Bazı durumlarda bazı kontrolcülerde başlangıç kontrolcüsünün çalışmamasını isteyebilirsiniz. Örneğin bir login işlemi yapılacağında başlangıç kontrolcüsündeki login kontrolü yüzünden login kontrolcüsü yönlendirmeye girebilir. Bu gibi durumlar nedeni ile bazı kontrolcüleri hariç tutmanız gerekir. Bunun için exclude sabiti kullanılır. Hariç tutulacak kontrolcüler bu diziye belirtilirken **kontrolcünün dosya adı** kullanılmalıdır.

**File:** Controllers/Initialize.php

    <?php namespace Project\Controllers;
    
    use User;
    
    class Initialize extends Controller
    {
        const exclude = ['Login']; # Kontrolcünün dosya adı belirtilmelidir.
    
        public function main()
        {
            if( ! User::isLogin() )
            {
                redirect('Login');
            }
        }
    }

Kontrolcünün yanı sıra URI bilgisi de hariç tutulabilir. Bu durumda exclude dizisine yazılacak veri **küçük harflerden** oluşacak şekilde yazılmalıdır.

**File:** Controllers/Initialize.php

    <?php namespace Project\Controllers;
    
    use User;
    
    class Initialize extends Controller
    {
        const exclude = ['account/login']; # It should be written in lower case.
    
        public function main()
        {
            if( ! User::isLogin() )
            {
                redirect('account/login');
            }
        }
    }

**Dahil Tutma (ZN >= 5.2.0)**

Sayfaları hariç tutmanın tam tersidir. Bu sabitin (include) kullanımında başlangıç kontrolcüsünün hangi kontrolcüler üzerinde geçerli olacağını belirtir. İstenirse hem exclude hem include sabitleri bir arada kullanılabilir.

**File:** Controllers/Initialize.php

    <?php namespace Project\Controllers;
    
    use User;
    
    class Initialize extends Controller
    {
        const include = ['home', 'product', 'contact'];
    
        public function main()
        {
            
        }
    }

Çoklu Başlangıç Kontrolcüsü Kullanma

Çoklu başlangıç kontrolcü kullanımına bazı kodların tüm kontrolcülerde bazılarının ise belirli kontrolcülerde geçerli olması veya olmaması gereken durumlarda ihtiyaç duyulur.

Öncelikle hangi kontrolcülerin başlangıç kontrolcüsü olarak kullanılacağı yapılandırma dosyasına belirtilmelidir.

**Dosya:** Config/Starting.php

    'constructors' => ['Initialize', 'Master'],

Yukarıdaki yapılandırmadan sonra artık hem Initialize hem de Master kontrolcüleri başlangıç kontrolcüsü olarak kullanılacaktır.

**Dosya:** Controllers/Master.php

    <?php namespace Project\Controllers;
    
    class Master extends Controller
    {
        const exclude = ['Login'];
    
        public function main()
        {
            # Masterpage'nin kullanacağı head ve body sayfaları belirtiliyor.
            Masterpage::headPage('head')->bodyPage('body');
        }
    }

Yukarıda Masterpage:: kullanımı Login kontrolcüsü için devre dışı bırakılırken;

**Dosya:** Controllers/Initialize.php

    <?php namespace Project\Controllers;
    
    use Config;
    
    class Initialize extends Controller
    {
        public function main()
        {
            # Config/Database.php -> database
            # Veritabanı ayarı yapılandırılıyor.
            Config::database('database', 
            [
                'database' => 'test',
                'user'     => 'root',
                'password' => '123456'
            ]);
        }
    }

Yukarıda yer alan veritabanı yapılandırması hem Login hem de diğer tüm kontrolcüler için devrede olacaktır. 

Görüldüğü üzere birden fazla başlangıç kontrolcüsü kullanımı bu tip yapılandırmaların ayrıştırılması gereken durumlarda gerekli olmaktadır.

**Alt Kontrolcülere Data Gönderimi (ZN >= 5.3.9)**

Görünüme data göndermek için kulanılan View sınıfı ile istenirse o an çalışan kontrolcüyede data gönderebilir. Bunun için 2 yöntem vardır.

> ● Kontrolcüde const extract = true tanımlaması.  
> ●  Config/Starting.php \-> extractViewData = true tanımlaması.

**File:** Controllers/Initialize.php

    <?php namespace Project\Controllers;
    
    class Initialize extends Controller
    {
        public function main()
        {
            View::sendData('Send Data')->otherData('Other Data');
        }
    }

Yukarıdaki örnek data gönderiminden sonra belirtilen 2 yöntemden biri kullanıldığı taktirde kontrolcüde $this nesnesi ile bu değerlere ulaşılabilir.

**File:** Controllers/MyController.php

    <?php namespace Project\Controllers;
    
    class MyController extends Controller
    {
        const extract = true;
    
        public function main()
        {
            echo $this->sendData;
            echo $this->otherData;
        }
    }

Send Data  
Other Data

Gönderimler tüm kontrolcüler için geçerli olacaksa her kontrolcüde const extract tanımlası yerine bunu Config/Starting.php değerinden aktif edilmesi daha akıllıca olacaktır.

**Doğrudan Erişim (ZN >= 5.6.0)**

Bu güncelleme ile const extract kullanmadan doğrudan doğruya aşağıdaki gibi de verileri alabilirsiniz.

    <?php namespace Project\Controllers;
    
    class MyController extends Controller
    {
        public function main()
        {
            echo View::sendData();
            echo View::otherData();
        }
    }

Send Data  
Other Data

#### # Kontrolcü Restorasyonu (ZN >= 4.3.0)

* * *

Yayında olan bir projenizde bazı kontrolcüler üzerinde kodsal düzenlemeler yaparken kullanıcıların bu düzenlemelere yönelik sonuçlarla karşılamasını istemeyip farklı bir sayfaya yönlendirilmesini sağlayabilirsiniz.

Bu işlem 2 şekilde yapılabilir;

● Yapılandırma dosyası ile.  
● Kontrolcü içinde const restore sabiti ile.

Yapılandırma

Restorasyon ayarları aşağıdaki yapılandırma dosya üzerinden yapılmaktadır. Bu yapılandırma dosyasında yer alan ayarlar aşağıda verilmiştir.

**Yapılandırma Dosyası:** Config/Project.php

**Restoration**

string

$mode = ''

Restorasyon işlemlerini başlatmak için bu ayar 'restoration' olarak ayarlanmalıdır.

mixed

$machinesIP = \[\]

Restore çalışmaları hangi bilgisayarlar üzerinde gerçekleştirilecekse o bilgisayarlara ait IP bilgisi belirtilir. Birden fazla IP bilgisi girilecekse dizi türünde belirtilebilir.

mixed

$pages = \[\]

Onarım işlemi yapılan sayfalar belirtiliyor. Tek bir sayfa ise string atama yapabilirsiniz. Birden çok sayfa belirtilecekse dizi içerisinde sırası ile onarım yapılan sayfalar belirtilir. Eğer tüm sayfalarda onarım yapılıyorsa string **"all"** ataması kullanılır. Burada unutulmaması gereken sayfada bir hatanın var olması ve kullanıcıların bu hata ile karşılaşıyor olması durumunda bu ayarın yapılması gerektiğidir. Aksi halde çalışan sayfa için yönlendirilmek üzere sayfa ayarlamak çok akıllıca değildir. Onarıma alınan sayfa ziyaret edildiğinde kullanıcıların hangi sayfaya yönlenmesi isteniyorsa o sayfanın yolu belirtilir.

string

$routePage

Restoration Pages ayarına belirtilmiş sayfalarından herhangi birine istek yapıldığında bu ayarın belirtildiği sayfaya yönlendirilir. Bu bölüme yazılması gereken sayfa adı değildir controller/function bilgisidir.

**Restore Sabiti**

Bu kullanımda $mode değerinin değiştirilmesine gerek yoktur. 

machinesIP

Hangi IP/IPS adreslerinin çalışma yapacağı. Birden fazla ip belirtilecekse dizi kullanılır.

functions

Hangi fonksiyonlarda çalışma yapılacağı. Birden fazla fonksiyon için dizi veya tümü için all belirtilebilir.

routePage

Kullanıcıların bu sayfaları ziyaret etmesi durumunda hangi kontrolcü/fonksiyona gideceği.

    <?php namespace Project\Controllers;
    
    class Home extends Controller
    {
        const restore =
    
        [
            'machinesIP' => '127.0.0.2',   // Array or String
            'functions'  => 'main',        // Array or String
            'routePage'  => 'home/restore' // Route Controller/Function
        ];
    
        public function main(string $params = NULL)
        {
    
        }
    
        public function restore()
        {
            echo 'System Restore!';
        }
    }