# Basit Bir Kod Çalıştırmak

- [Giriş](#giris)
- [PHP ve HTML İlişkisi](#php-ve-html-iliskisi)
    - [PHP](#php-ve-html-iliskisi-php)
    - [HTML](#php-ve-html-iliskisi-html)
    - [Erişim](#php-ve-html-iliskisi-erisim)
    - [Farklı Bir Sayfa Oluşturun](#php-ve-html-iliskisi-farkli-bir-sayfa-olusturun)

<a name="giris"></a>
## Giriş

ZN Framework ilk çalıştırıldığında Ulu Önderimizin "Hayata en hakiki mürşit ilimdir." yazısı karşılamaktadır. ZN Framework üzerinde web sayfaları oluşturmak ve erişmek oldukça kolaydır. En temel olarak üzerinde çalıştığımız sayfalara ait PHP ve HTML içerikler iki ayrı dosya bulunur. Aşağıda bu iki tür dosyaların hangi dizinlerde yer alacağı ve arasında nasıl iletişim kurulacağı anlatılmıştır.

<a name="php-ve-html-iliskisi"></a>
## PHP ve HTML İlişkisi

Kısaca PHP kodları kontrolcüler(Controllers), HTML içerikleri ise görünümlerde(Views) yer alırlar. Aşağıda örnek bir kontrolcü ve görünüm örneklerine yer verilmiştir.
<a name="php-ve-html-iliskisi-php"></a>
### PHP

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
<a name="php-ve-html-iliskisi-html"></a>
### HTML

```shell
Projects/Frontend/Views/Home/main.wizard.php
```

```html
<strong>Home Page</strong>
```
<a name="php-ve-html-iliskisi-erisim"></a>
### Erişim

ZN Framework ilk olarak adres çubuğunda çalıştırıldığında ki bunun localhost olduğunu varsayarsak ön tanımlı açlış kontrolcüsü Home.php ve bu kontrolcünün çağırdığı Home/main.wizard.php görünümüdür. 

Yukarıdaki örneği çalıştırmak için adres çubuğuna aşağıdaki URL'yi yazınız.

```shell
localhost/
```

Aslında çalıştırılan URL aşağıdaki gibidir.

```shell
localhost/Home/main
```

Ön tanımlı olarak Home kontrolcüsü ve bu kontrolcüye bağlı Home/main yöntemi ayarlı olduğundan adres çubuğunda belirtilmesine gerek yoktur.
<a name="php-ve-html-iliskisi-farkli-bir-sayfa-olusturun"></a>
### Farklı Bir Sayfa Oluşturun

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

**Not**
Bir kontrolcünün ön tanımlı açlış yöntemi <b>main</b> olmasından dolayı adres çubuğunda belirtilmesine gerek yoktur.