> **Docker**, `container` teknolojisini kullanarak uygulama oluşturmayı, dağıtmayı ve çalıştırmayı kolaylaştırmak için tasarlanan bir araçtır.

> **Container**, kodu ve tüm bağımlılıklarını paketleyen standart bir yazılım birimidir. Böylece uygulama bir bilgisayar ortamından diğerine hızlı ve güvenilir bir şekilde paylaşılır ve çalıştırılır. Container'lar, temeldeki bilgisayarı sanal bir makina gibi sanallaştırmak yerine yalnızca "işletim sistemini" sanallaştırırlar.

> **Image**, amaca yönelik container'ların çalışması için gerekli önceden tasarlanmış kalıplardır. Image örnekleri : postgres, ppadmin, mysql

---
### Açıklama
#### Programcı, kendi bilgisayarında uygulamayı tamamlar ve bu uygulamayı tester'e verip test ettirmesini ister fakat bu uygulama için gerekli programları tester'inde kurması gerekir. Bir bilgisayarda farklı uygulamalar için farklı sürümler gerektiren örneğin Java8, Java11, Python2.7, Python2.8 gibi birden çok program kurdurulması gerekebilir. Bu programların birbirinden izole şeklinde çalışması gerekir. Programların birbirinden izole şeklinde çalışması için Virtual Machine - Sanal Makine (VM) icat edildi. 
#### `Docker`, 2013'de sanal makinelere alternatif olan ve  birçok konularda avantaj sağlayan bir yazılımdır ve açık kaynaklı koddur. 

---

## Virtual Machine VS Docker Container

![](https://raw.githubusercontent.com/mustafakarakas61/Images/main/vmVSdocker.png)

| Virtual Machine                                        | Docker Container                                               |
|--------------------------------------------------------|----------------------------------------------------------------|
| Donanım düzeyinde sanallaştırma                        | İşletim sistemi düzeyinde sanallaştırma                        |
| Her sanal makine kendi işletim sisteminde çalışır      | Tüm konteynerler ana bilgisayar işletim sistemini paylaşır     |
| Ağırdır (onlarca GB boyutundadırlar)                   | Hafiftir (sadece MB boyutundadırlar)                           |
| Başlatılması dakikalar alır                            | Başlatılması saniyeler alır                                    |
| Tamamen izole edilmiş                                  | İşletim sistemi seviyesinde proses düzeyinde izolasyon         |
| Sanal makine sıfırdan hazırlamak çok zaman alır        | Dakikalar içinde hazırlanabilir                                |
| Çok kaynak kullanır                                    | Oldukça az kaynak kullanır                                     |
| Makinede sadece donanım kadar sanal makine çalışabilir | Birçok konteyner çalışabilir                                   |
| Güncelleme ve güvenlik yamaları çok zahmetlidir        | Güncellenme ve güvenlik yamaları çok kolay bir şekilde yapılır |

- Not : Bir image aramak veya daha fazlası için [hub.docker.com](https://hub.docker.com/) adresine gidiniz.

| Komut (örneklerde image olarak 'mysql', 'redis'  ve 'phpmyadmin/phpmyadmin' kullanıldı)                  | Açıklama                                                                                                                                                                                                                                                      |
|----------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| docker pull **mysql**                                                                                    | Bir imaj çekmek için kullanılır. Örneğin mysql imajını pull ettik. Sadece pull edilir, run edilmeyecektir yani çalıştırılmayacaktır.                                                                                                                          |
| docker images                                                                                            | İndirdiğimiz imajları listelemek için kullanılır.                                                                                                                                                                                                             |
| docker run **redis**                                                                                     | Bilgisayarımızda bulunan imajı çalıştırmak için kullanılır. Örneğin redis imajı daha önce indirilmemişse önce pull edip sonra run yapar.                                                                                                                      |
| docker run -it **mysql**                                                                                 | İlgili imajın içine girmek için kullanılır. Çıkmak için exit yazılır veya ctrl+c yapılır. -it flag'ı kullanılmazsa tepki vermez, açılır ve kapanır. Kullanıcı girişli birşey varsa -it flag'ı kullanılır.                                                     |
| docker ps                                                                                                | Ayakta olan konteynerleri gösterir.                                                                                                                                                                                                                           |
| docker ps --all                                                                                          | Geçmişe yönelik konteynerleri listelemek için kullanılır.                                                                                                                                                                                                     |
| docker ps -a                                                                                             | -a flag'ı, --all'ın kısaltımıdır. Aynı işleve sahiptir.                                                                                                                                                                                                       |
| docker container ls                                                                                      | Aktif olan konteynerlerin listesidir.                                                                                                                                                                                                                         |
| docker container ls -a                                                                                   | Geçmişe yönelik konteynerleri listelemek için kullanılır. docker ps -a ile aynı işleve sahiptir.                                                                                                                                                              |
| docker run -it --name custom_container_name_mysql **mysql**                                              | Buradaki --name flag'ı  bir konteynera isim vermek için kullanılır. Eğer kullanılmazsa docker, konteynere rastgele isim verecektir.                                                                                                                           |
| docker start **container_name**                                                                          | Önceden hazırladığımız, komutlarını yazdığımız konteyneri çalıştırmak için start komutu kullanılır.                                                                                                                                                           |
| docker stop **container_name**                                                                           | Konteyner'i durdurmak için kullanılır.                                                                                                                                                                                                                        |
| docker rm **container_name**                                                                             | Bir konteyneri silmek için kullanılır.                                                                                                                                                                                                                        |
| docker container rm $(docker container ls -aq)                                                           | Tüm konteynerleri silmek için kullanılır. $(docker container ls-aq) tüm konteynerlerin listesini verecektir.                                                                                                                                                  |
| docker run **redis**:5                                                                                   | ':' sonrası tag'i belirtir. Kullandığımız 5 ise redis'in 5. versiyonunu yükleyip çalıştırtacaktır. Kullanılmadığında varsayılan olarak latest versionu yüklenir.                                                                                              |
| docker image tag **mysql**   my_custom_mysql                                                             | Bir imajı özelleştirmek için kullanılır.                                                                                                                                                                                                                      |
| docker run -d redis                                                                                      | İmajı detach modda yani arkaplanda çalıştırmak için kullanılır. Loglarını göremeyiz.                                                                                                                                                                          |
| docker attach **container_name**                                                                         | Arkaplanda çalışan imajı attach modda yani önplanda çalıştırmak için kullanılır. Böylece loglarını görebiliriz.                                                                                                                                               |
| docker container logs **container_name**                                                                 | Detach modda çalıştığından itibaren tüm logları listelemek için kullanılır.                                                                                                                                                                                   |
| docker run -p 3306:3306 **mysql**                                                                        | Port ayarı. ':''ın sol tarafındaki port, docker'da olan portun kendi bilgisayarımızdaki karşılığıdır. Docker'da bulunan port değiştirilemez. Kullanılan imajın dökümanında port bilgileri mevcuttur.                                                          |
| docker run -v /opt/data:/var/lib/mysql **mysql**                                                         | Docker host üzerinde konteynerler herhangi bir bilgi içerisinde kayıt edilemez. Konteyneri durdurduğumuzda kayıt edilen bilgiler silinir. Bu durumu ortadan kaldırmak için volume mapping yapılır.  Kullanılan imajın dökümanında volume bilgileri mevcuttur. |
| docker inspect **container_name**  ya da    **image_name**                                               | Bir konteyner ya da imaj hakkında detaylı bilgiler almak için kullanılır.                                                                                                                                                                                     |
| docker run -e MYSQL_ROOT_PASSWORD=12345 -d **mysql**                                                     | Bazı imajların ortam değişkenlerine (environment variable) ihtiyacı olabiliyor. Bunları belirtmek ve ayarlamak için kullanılan imajın ilgili dökümanını okuyunuz.                                                                                             |
| docker pull phpmyadmin/phpmyadmin                                                                        | Örneğin mysql'e erişmek için phpmyadmin kurmalıyız. kullanıcıadı/imaj şeklinde kullanılır. Eğer bir publisher değilseniz phpmyadmin için default olarak phpmyadmin kullanılır.                                                                                |
| docker run --name pmyadmin -p 8000:80 --link **custom_container_name_mysql**:db -d phpmyadmin/phpmyadmin | --link flag'ı ile phpmyadmin ayağa kalktığında buna bağlanacak imajı bu şeklide bağlıyoruz. ':db' ise localhost karşılığı olan bir alias'dır.                                                                                                                 |

- Not : Her container'in kendine ait bir **name**'i ve **id**'si, her image'nin kendine ait bir **tag**'ı ve **id**'si vardır. Bir komutta name veya tag yerine `id` kullanılabilir.

## docker-compose.yml build etme

- Build etmek için : docker-compose build
- Ayağa kaldırmak için : docker-compose up -d
- Kapatmak için : docker-compose down

### docker-compose.yml örneği:
    version: "3.1"
    services:
        s_nginx:          ________________________             
            container_name: c_nginx               \
            image:nginx                            \
            ports:                                  > docker run -d -p 8080:80 -p 8081:80 --name c_nginx nginx
              - 8080:80                            /
              - 8081:80   ________________________/
        s_html:
            container_name: c_html
            image: httpd
            volumes:
               - html:/usr/local/apache2/htdocs/    > kendi bilgisayarımdaki klasör:docker içinde kullandığı klasör
            ports:                                 
               - 9091:80
               - 9092:80
    volumes:
        html:                                       > oluşturduğumuz volume'ler burada tanımlanmalıdır

- Not : Kullanılan image'in [hub.docker.com](https://hub.docker.com/) adresinde bulunan ilgili dökümanlarında ilgili bilgiler verilmiştir. Hangi volume'nin, hangi environment'in, hangi portun vs kullanılacağı ve nasıl kullanılacağı hakkında bilgi almak için ilgili dökümanı okuyunuz.

***

### Kaynaklar

* <http://kablosuzkedi.com/>
* <https://github.com/mustafakarakas61>
