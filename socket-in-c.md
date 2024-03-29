# **Socket Programlama**

## Socket Programlama Nedir?
Socket programlama, alıcı ve verici ile iletişim yönetmek için kullanılan programlama tekniğinidir.

&nbsp;

Socket programlama birçok dille yapılabilir.

&nbsp;

HTTP, FTP, SMTP gibi protokoller socket programalama yapısı ile inşa edilmiştir.

&nbsp;

Socket kavramının temelini Berkeley Sockets tarafından oluşturulmuştur. Linux/Unix dağıtımlarda bu socketler POSIX olarak geçerken windows'da winsock olarak geçer.

&nbsp;

## Socket Programlamaya Giriş

Socket Programlamaya geçmeden önce şunu bilemekte fayda var. Sistem bir program çalıştırırken **veri girişi (stdin)**, **veri yazdırma (stdout)** ve hata işleme (stderr) için sabit tanımlar yapar. Mesela:

```c
int main(void) {

      fprintf(stdout, "hello world!"); // --> veri yazdirma
      return 0;
}
``` 

&nbsp;

Benzer şekilde bir dosya açılırsa da dosya işlemleri için de kullanabiliriz:

```c
#include <stdio.h>

int main(void) {
    
    FILE *fp = fopen("text.txt", "w");
    /* fopen fonksiyonu dosya islemleri icin (dosya okuma, yazma) kullanilir. */
    
        fprintf(fp, "Hello! I'm write C!");
        /* fprintf, fwrite gibi fonksiyonlar ile dosyalara yazma islemler yapilabilir. */
        
    fclose(fp);
    /* acilan fopen kapatmak icin kullanilir. */
    return 0;
```

&nbsp;

## **Socket Oluşturma**

Socket için kullanılacak fonksiyonlar, veri yapıları ve sabitler linux/unix tabanlı sistemler için aşağıdaki repolar kullanılır:

```c
#include <sys/socket.h>
#include <arpa/inet.h>
#include <netinet/in.h>
#include <unistd.h>
```

&nbsp;

Windows için de aşağıdaki repolar kullanılır:

```c
#include <winsock2.h>
#include <ws2tcpip.h>
```

&nbsp;

İki bilgisiyar arasında socket oluşturmak için **socket** fonksiyonu kullanılır:

```c
int socket(int <protokol-type>, int <sending-data>, int <transport-protokol>)
/*                 Domain               Type                  protocol*/
```

&nbsp;

**Domain** parametresi AF_UNIX (Unix Dosyası), AF_INET (IPv4), AF_INET6 (IPv6) sabitlerini

**Type** parametresi, SOCK_STREAM(TCP), SOCK_DGRAM (UDP), SOCK_RAW sabitlerini,

**Protocol** parametresi de genellikle 0 değerini alır:

```c
#include <stdio.h>
#include <sys/socket.h>

int main(void) {

       int path = socket(AF_INET, SOCK_STREAM, 0);
       /*                 Domain     Type    Protocol */
       return 0;
}
```

&nbsp;

## **errno.h**

errno.h, hata mesajlarını ekrana bastırmak için gerekli makroların tanımlı olduğu bir header dosyasıdır. 

Eğer program içerisinde bir hata algılanırsa bazı library functions (kütühane fonksiyonları) tarafından errno'a bir değer atanır. Program başladığında sakladığı değer sıfırdır. 

Library Functions yalnızca sıfırdan büyük değerler depolar. Aynı zamanda bir hata algılasar da algılamasalar da içerisindeki değerler dönmeden önce değerleri değişebilir. Genellikle bu kütüphanelere, pointer tarafından döndüren değer NULL ve tamsayı döndüren işlevler için -1 gibi özel değerler döndürerek hata mesajı algılanır.

Bununla ilgili aşağıda örnek verilmiştir:

```c
#include <stdio.h>
#include <error.h>
#include <sys/types.h>

//windows ortamında yazılmıştır.

void error(const char *msg) {

      perror(msg);
      exit(1);
}
```

Yukarıdaki örnekten yola çıkarsak, eğer -1 sonucunda bir hata meydana gelirse öncelikle bu hata mesajı, fonksiyon içerisinde oluşturulan <strong> *msg </strong>
pointer içerisine kaydedilecek ve **perror** fonksiyonu ile kaydedilen hata mesajı ekrana basılacaktır. 
