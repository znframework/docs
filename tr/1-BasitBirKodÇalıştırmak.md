# Basit Bir Kod Çalıştırmak

- [Giriş](#giris)
- [PHP ve HTML İlişkisi](#php-ve-html-iliskisi)
    - [PHP](#php-ve-html-iliskisi-php)
    - [HTML](#php-ve-html-iliskisi-html)
    - [Erişim](#php-ve-html-iliskisi-erisim)
    - [Farklı Bir Sayfa Oluşturun](#php-ve-html-iliskisi-farkli-bir-sayfa-olusturun)


## Giriş <a name="giris"></a>

ZN Framework ilk çalıştırıldığında Ulu Önderimizin "Hayata en hakiki mürşit ilimdir." yazısı karşılamaktadır. ZN Framework üzerinde web sayfaları oluşturmak ve erişmek oldukça kolaydır. En temel olarak üzerinde çalıştığımız sayfalara ait PHP ve HTML içerikler iki ayrı dosya bulunur. Aşağıda bu iki tür dosyaların hangi dizinlerde yer alacağı ve arasında nasıl iletişim kurulacağı anlatılmıştır.


## PHP ve HTML İlişkisi <a name="php-ve-html-iliskisi"></a>

Kısaca PHP kodları kontrolcüler(Controllers), HTML içerikleri ise görünümlerde(Views) yer alırlar. Aşağıda örnek bir kontrolcü ve görünüm örneklerine yer verilmiştir.

### PHP <a name="php-ve-html-iliskisi-php"></a>

```shell
Projects/Frontend/Controllers/Home.php
```

```php
namespace Project\Controllers

class Home extends Controller
{
    public function main()
    {
        Masterpage::title('Home');
    }
}
```

### HTML <a name="php-ve-html-iliskisi-html"></a>

```shell
Projects/Frontend/Views/Home/main.wizard.php
```

```html
<strong>Home Page</strong>
```
 
### Erişim <a name="php-ve-html-iliskisi-erisim"></a>

ZN Framework ilk olarak adres çubuğunda çalıştırıldığında ki bunun localhost olduğunu varsayarsak ön tanımlı açlış kontrolcüsü Home.php ve bu kontrolcünün çağırdığı Home/main.wizard.php görünümüdür. 

Yukarıdaki örneği çalıştırmak için adres çubuğuna aşağıdaki URL'yi yazınız.

```shell
localhost/
```

Aslında çalıştırılan URL aşağıdaki gibidir.

```shell
localhost/Home/main
```

> **Note**
> Ön tanımlı olarak Home kontrolcüsü ve bu kontrolcüye bağlı `Home/main` yöntemi ayarlı olduğundan adres çubuğunda belirtilmesine gerek yoktur.

> **Note**
> Kontrolcü ile görünümü bağlamak için Kontrolcünün adı ve yöntemi ile aynı isme sahip görünüm dizini ve sayfası oluşturulması gerekir. 
> `Home` kontrolcüsünün `main` yöntemi bir görünüme otomatik olarak erişecekse görünüm `Views/Home/main.wizard.php` gibi bir dosya içermek zorundadır.
> Görüldüğü üzere `Home::main -> Home/main.wizard.php` ilişkisi kurulmuştur.

### Farklı Bir Sayfa Oluşturun <a name="php-ve-html-iliskisi-farkli-bir-sayfa-olusturun"></a>

Bu sefer iletişim(Contact) isimli bir kontrolcü ve onun çağıracağı bir görünüm tasarlayalım.

```shell
Projects/Frontend/Controllers/Contact.php
```

```php
namespace Project\Controllers

class Contact extends Controller
{
    public function main()
    {
        Masterpage::title('Contact');
    }
}
```

```shell
Projects/Frontend/Views/Contact/main.wizard.php
```

```html
<strong>Contact Page</strong>
```

Erişmek için aşağıdaki bağlantıyı kullanın.

```shell
localhost/Contact
```

> **Note**
> Bir kontrolcünün ön tanımlı açlış yöntemi <b>main</b> olmasından dolayı adres çubuğunda belirtilmesine gerek yoktur.

