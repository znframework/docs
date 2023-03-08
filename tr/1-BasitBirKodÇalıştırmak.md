# Basit Bir Kod Çalıştırmak

- [Giriş](#giris)
- [PHP ve HTML İlişkisi](#php-ve-html-iliskisi)

<a name="giris"></a>
## Giriş

ZN Framework ilk çalıştırıldığında Ulu Önderimizin "Hayata en hakiki mürşit ilimdir." yazısı karşılamaktadır. ZN Framework üzerinde web sayfaları oluşturmak ve erişmek oldukça kolaydır. En temel olarak üzerinde çalıştığımız sayfalara ait PHP ve HTML içerikler iki ayrı dosya bulunur. Aşağıda bu iki tür dosyaların hangi dizinlerde yer alacağı ve arasında nasıl iletişim kurulacağı anlatılmıştır.

<a name="php-ve-html-iliskisi"></a>
## PHP ve HTML İlişkisi

Kısaca PHP kodları kontrolcüler(Controllers), HTML içerikleri ise görünümlerde(Views) yer alırlar. Aşağıda örnek bir kontrolcü ve görünüm örneklerine yer verilmiştir.

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

### HTML

```shell
Projects/Frontend/Views/Home/main.wizard.php
```

```html
<strong>Home Page</strong>
```