<div align="center">

## ** Socket Programlama Nedir? **


Socket programlama, alıcı ve verici ile iletişim yönetmek için kullanılan programlama tekniğinidir.

Socket programlama birçok dille yapılabilir.

    HTTP,
    FTP,
    SMTP gibi portlar socket yapısı ile inşa edilmiştir.

    Socket programlamaya geçmeden önce şunu bilmekte fayda var.
    Sistem bir program çalıştırırken veri girişi (stdin), veri yazdırma (stdout), hata işleme (stderr) için sabit tanım yapar. Bunlar sayesinde okuma ve yazma işlemeri yapılabilir. Mesela:

    ```c
        #include <stdio.h>

        int main(void) {

            fprintf(stdout, "Hello World!\n");
            return 0;
        } 
    ```
</div>