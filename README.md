# "Digitalocean Node app deploy with nginx & SSL" або "Записки божевільного про перший в житті деплой"
## Від автора
Вітаю! 
Якщо вас занесло сюди, то скоріше за все ви або збираєтесь деплоїти власну апку, або вже в процесі сексу з деплоєм :) Цей гайд розрахований саме на таких як ми з вами, тому що я пройшов крізь цю хуйню і можу сказати, що це така мозгойобка єбана блядь...я посивів блядь, я полисів, і карочє... і все це за один деплой. Звісно це був мій перший раз, але блять. 
Отже я сподіваюся, що мої страждання і єбля не пропадуть даром і я зможу комусь допомогти) 

**P.S.** По своїй суті це перекат досить сухого гайду з частково застарілою інформацією [отуто](https://gist.github.com/bradtraversy/cd90d1ed3c462fe3bddd11bf8953a896). Саме після того як я пройшовся по ньому декілька разів і все ж таки зміг задеплоїти свою хуйню я вирішив зробити апдейт по цій хуйні, щоб наступним хто буде цим займаться було вже набагато легше.

**WARNING ⚠** Багато нецензурної лексики, але тут по-іншому не можна, це ж деплой
____ 
### Крок перший - DigitalOcean
Першим ділом топаємо на [DigitalOcean](https://cloud.digitalocean.com/registrations/new) та створюємо собі акаунт. Ніяких прихованих рефералок в посиланні нема, якщо шо. 
____ 
### Крок другий - Droplet
0. Після реєстрації ви отримаєте велкам бонус (звісно якшо це перша ваша реєстрація) на 60 днів і на цей час про бабосіки можна не паритись). Отже, тицяємо у правому верхньому куті на кніпочку крєате та обираємо "Droplets":

![image](https://github.com/ohiienko-r/digitalocean-droplet-deploy/assets/109099364/a0ee3315-2e1a-4475-963e-6135834dd991)


1.Обираємо локацію цього чуда:

![image](https://github.com/ohiienko-r/digitalocean-droplet-deploy/assets/109099364/a2a2dca7-6537-43ff-97e4-f9aed3fa4c4b)

2. Потім і операціонку на якій він буде раниться:

![image](https://github.com/ohiienko-r/digitalocean-droplet-deploy/assets/109099364/a2b92b0f-6ad1-482d-a46f-05d7c35340ad)

3. Далі треба обрати конфігурацію дроплєта. Я обрав для себе третій з кінця бо апка буде мати навантаження у орієнтовно 50 людей, а їбаться з цим потім не дуже хочється. В будь якому випадку конфіг завжди можна змінити після створення:

![image](https://github.com/ohiienko-r/digitalocean-droplet-deploy/assets/109099364/9e4bc3d4-d74f-4f43-90dd-9dd1e04df31a)

4. Вішаємо пароль/ssh ключ для доступу (я обрав для себе пароль):

![image](https://github.com/ohiienko-r/digitalocean-droplet-deploy/assets/109099364/18b41f85-7512-4249-984c-d60d80c6f2c2)

5. Додаємо безкоштовний моніторинг метрік дроплєта та обираємо проект для якого цей дроплєт створюється:

![image](https://github.com/ohiienko-r/digitalocean-droplet-deploy/assets/109099364/8e2211e0-1ef0-465a-8cc4-3ec5e347cfea)

6. Вуаля! Тицяємо в крєате дроплєт і думаємо про життя поки воно там шось собі думає.

7. Покурили? Тепер треба і заглянуть на наш дроплєт і запустить його консоль:

![image](https://github.com/ohiienko-r/digitalocean-droplet-deploy/assets/109099364/cf23648b-1300-472a-86cc-cad89d512bac)


8. Сміливо клікаємо по лонч дроплєт консолє. Мої конгратуляції, ми єбать які молодці з вами: 

![image](https://github.com/ohiienko-r/digitalocean-droplet-deploy/assets/109099364/275b6948-c539-4044-b44e-37366fa0bd88)



____ 
### Крок третій - Node/NPM

На наш любімий дроплєт тепер треба накатить ноду. В моєму випадку в мене на дроплєті накочєна юбунтУ 22.04 тому я і буду використовувать туторіал для неї. Посиланнячко на інструкцію [отуто](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-22-04). Обираєте зручний для вас варіант з трьох і єбать його в рот.
____ 
### Крок четвертий - Git
Тепер же ш нам треба загнать наш з вами проект на любімий дроплєт. Будем тягнуть все це діло з гітхаб репозиторію: 
```
git clone yourproject.git
```
Тіки той, не забудьте замінити `yourproject.git` на посилання на ваш проект, а то я вас блять знаю. 
____ 
### Крок п'ятий - Dependencies
Зклонувать зклонували, тепер же ш нада і пакєти накатить!: 
```
#переходимо в свій проект
cd yourproject

#Вращаєм барабан
npm install

#Сєктор пріз на барабані!
npm start (або яка там в вас команда)

#Зупиняєм все це діло, бо справ ще по самі гланди
ctrl+C
```
____ 
### Крок шостий - PM2 
Оця хуйня нам треба шоб наш з вами додаток ранився константно і не їбав ні нам, ні юзвєрям голову:
```
sudo npm i pm2 -g

#Якшо консоль матюкнеться на судо, приберіть його, воно і так зі свистом залітає на наш любімий дроплєт
```
Після цього можна і спробувать запуститься:
```
pm2 start app #міняємо app на назву свого корнєвого файлу сєрвєра (в моєму випадку це index) і буде вам щастя
```
Якшо все гуд, а все має бути гут, треба ще перестрахуваться і зробить так шоб PM2 запускався разом із системою нашого любімого дроплєта:
```
pm2 startup ubuntu
```
І бонусом прілагається ще список команд для PM2 які допоможуть вам в майбутньому якшо будете якісь проблеми вирішувати: 
```
pm2 show app
pm2 status
pm2 restart app
pm2 stop app
pm2 logs #я думаю понятно шо воно показує?
pm2 flush #а оце треба шоб почистить всі логи
```
Тепееееер в нас з вами є можливість подивиться на нашу аплікуху якщо впіхуюріть в адресну строку браузєра айпішнік любімого дроплєта з портом на якому раниться апка.
____ 
### Крок сьомий - UFW (Uncomplicated Firewall)
Ну тут все просто. Степ бай степ хуячим команди в консолькє любімого дроплєта і радуємся життю: 
```
sudo ufw enable
sudo ufw status
sudo ufw allow ssh 
sudo ufw allow http 
sudo ufw allow https 
```
____
### Крок восьмий - NGINX та його конфігурація
В цілому процесс його вствновлення та конфігурації простий, але сам по собі він може вас так виєбать і висушить шо жити не захочється. Більше детально я опишу проблеми які виникли з ним у мене в розділі "Додатки".

Отже, все шо від нас треба на старті: 
```
sudo apt install nginx

sudo nano /etc/nginx/sites-available/default
```

Після другої команди нас закине в такий собі конфіг цього йобаного nginx де нам з вами треба буде знайти рядок з директивою `location /` і в середину фігурних дужок додати наступний код: 
```
proxy_pass http://localhost:5000; #порт звісно вказуємо свій
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection 'upgrade';
proxy_set_header Host $host;
proxy_cache_bypass $http_upgrade;
```

Також нам треба вказати в тому ж конфігу ваш домєн для апки, якщо нема, то вказуємо пока шо просто апішнік любімого дроплєта після директиви `server_name`. І в результаті оце все діло має мати наступний вигляд: 
```
server_name yourdomain.com www.yourdomain.com;

    location / {
        proxy_pass http://localhost:5000; #порт звісно вказуємо свій
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
```

Тицяємо `Ctrl+X`, погоджуємося зберегти зміни `y` та жмемо `Enter` щоб нарешті вийти звідти.

Тепер давайте перевіримо а чи працює ця йобань по-людські, чи нє: 
```
# Перевіряємо працездатність конфігу
sudo nginx -t

# Робимо nginx рестарт
sudo service nginx restart
```

Якшо клята машина вийобується, перевірте чи все ви правильно закопіпастили і чи не пропустили де крапку з комою.

Ну тупер вже можна подивиться на апку в браузері через айпішнік любімого дроплєта без указанія порта. 
____
### Крок дев'ятий - Домєн блять!

Особисто я купляв домєн собі на [namecheap](https://www.namecheap.com/) (тут також нема рефералок ніяких в посиланні), але ви можете купляти їх де заманеться. Тим не менш, я опишу процес прихуярівання домєна до любімого дроплєта через `namecheap`. 

0. Переходим по посиланню, рєгаєм собі акаунт і топаєм на головну сторінку:

![image](https://github.com/ohiienko-r/digitalocean-droplet-deploy/assets/109099364/2ef2de37-1862-48e3-abed-d33087f902b1)

1. В пошукове поле вписуєм домєн який вас цікавить, натискаємо на сьорч і ахуєваємо від цін на деякі домєни:

![image](https://github.com/ohiienko-r/digitalocean-droplet-deploy/assets/109099364/584284eb-d9ae-40e8-897b-d452e8f343e8)









