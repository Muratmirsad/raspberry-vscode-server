# Raspberry Pi ile VS Code server kurulumu

Merhaba, bu dokümanda raspberry pi 4b ile kurduğum VS Code serverını nasıl kurduğumu anlatacağım.<br>

İlk olarak Node.js kuralım.
```Bash
sudo apt install nodejs npm
```

Şimdi ise VS Code server sürümünü kuralım.
```Bash
npm install -g code-server
```

Artık VS Code serverı başlatmak için hazırız.
```Bash
code-server --host 0.0.0.0 --port 22
```
Serverı "--host 0.0.0.0" parametresi ile, tüm iplerden gelen isteklere ve "--port 22" ile sadece 22 portundan gelen isteklere açtık. Bu yaptığımız işlem ile VS Code'u sadece yerel ağınızda kullanabilirsiniz. İstersen öncelikle bir test edelim.<br>

#### ❕ Not: Parametre olarak verdiğiniz portu, güvenlik duvarınızdan da izin vermeniz gerekiyor. Eğer UFW kullanıyorsanız bu şekilde yapabilirisniz. (daha fazla güvenlik için varsayılan 22 portu yerine, farklı bir port kullanmak önemlidir)
```Bash
sudo ufw allow 22
```
```Bash
sudo ufw reload
```

Server ipmizin 192.168.1.2 olduğunu varsayalım. Serverınız ile aynı ağda bulunun herhangi bir cihazdan tarayıcı kullanarak şu adrese gitmeyi deneyin.
```URL
192.168.1.2:22
```
Eğer her şey doğru ilerliyorsa, bu şekilde görünecek.
<img width="1359" alt="Ekran Resmi 2023-09-09 13 22 31" src="https://github.com/Muratmirsad/raspberry-vscode-server/assets/57044743/866e7979-2876-4fb4-84bd-a7ea120e6dc4">

Varsayılan olarak atanan şifreye buradan ulaşabilir veya isterseniz değiştirebilirsiniz.
```Bash
cat ~/.config/code-server/config.yaml
```

<br>Buraya kadar her şey tamamsa, şimdi serverımıza internetten erişmek için ayarlamalar yapalım. Kendi evimdeki ağı basit bir şekilde çizdim.

<img width="1173" alt="Ekran Resmi 2023-09-09 12 57 57" src="https://github.com/Muratmirsad/raspberry-vscode-server/assets/57044743/6fe5dbbc-0ee3-41b0-a16d-3a114959458c">

#### ❕ Not: Ben statik ip kullanıyorum, dinamik ip ile test etmedim.
## ❗️ Uyarı: Ev ağınızı internete açmak oldukça risklidir; sık kullanılan bir port açmaktan kaçınıp, güçlü şifreler kullanmayı (tavsiyem ssh public key oluşturup bunu şifre olarak kullanmanız) ve eğer ssh kullanıyorsanız, şifre ile oturum açmayı kapatıp, sadece private key ile oturum açma yöntemi kullanmanız önemli.

Öncelikle, internete çıkmak için kullandığınız routerın arayüzüne giriş yapın. Örnek olarak 22 portuna gelen istekleri servera yönlendireceğim.

<img width="1217" alt="Ekran Resmi 2023-09-10 14 13 40" src="https://github.com/Muratmirsad/raspberry-vscode-server/assets/57044743/7864307e-3c8a-4f2a-bb0f-4fc51a37c3a3">

Bu adımı tamamladıktan sonra, yerel ağınız ile kendinizin bağlantısını kesip, serverınıza internetten erişebilirsiniz.

Son olarak işinizi kolaştıracak bir script göstereceğim. "xx.xx.xx.xx" yazan kısma ev ağınızın, internete çıkmak izin kullandığı ip adresinizi yazın.
```Bash
echo "cat ~/.config/code-server/config.yaml
echo "ip: xx.xx.xx.xx"
code-server --port 22 --host 0.0.0.0" >> script.sh
```
Artık tek bir komut ile ihtiyacınız olan her şeye ulaşabilirsiniz.
```Bash
bash script.sh
```
<img width="1305" alt="Ekran Resmi 2023-09-09 14 36 50" src="https://github.com/Muratmirsad/raspberry-vscode-server/assets/57044743/a7854dbe-65a8-4a44-b32b-917f3871364a">


## İyi günler dilerim :)
