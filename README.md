# Raspberry Pi VS Code Server

Merhaba, bu dökümanda raspberry pi 4b ile kurduğum VS Code serverını nasıl kurduğumu anlatacağım anlatacağım.

İlk olarak Node.js kuralım
```Bash
sudo apt install nodejs npm
```


Şimdi ise VS Code server sürümünü kuralım
```Bash
npm install -g code-server
```


Artık VS Code serverı başlatmak için hazırız
```Bash
code-server --host 0.0.0.0 --port 22
```
Serverı "--host 0.0.0.0" parametresi ile, tüm iplerden gelen isteklere ve "--port 22" ile sadece 22 portundan gelen isteklere açtık. Bu yaptığımız işlem ile VS Code'u sadece yerel ağınızda kullanabilirsiniz. İstersen öncelikle bir test edelim.

#### ❕ Not: Parametre olarak verdiğiniz portu, güvenlik duvarınızdan da izin vermeniz gerekiyor. Eğer UFW kullanıyorsanız bu şekilde yapabilirisniz.
```Bash
sudo ufw allow 22
```
```Bash
sudo ufw reload
```


Server ipmizin 192.168.1.2 olduğunu varsayalım. Serverınız ile aynı ağda bulunun herhangi bir cihazdan şu adrese gitmeyi deneyin.
```URL
192.168.1.2:22
```
Eğer her şey doğru ilerliyorsa, bu şekilde görünecek.
<img width="1359" alt="Ekran Resmi 2023-09-09 13 22 31" src="https://github.com/Muratmirsad/raspberry-vscode-server/assets/57044743/866e7979-2876-4fb4-84bd-a7ea120e6dc4">




<img width="1173" alt="Ekran Resmi 2023-09-09 12 57 57" src="https://github.com/Muratmirsad/raspberry-vscode-server/assets/57044743/6fe5dbbc-0ee3-41b0-a16d-3a114959458c">
