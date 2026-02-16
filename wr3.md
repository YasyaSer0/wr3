# МІНІСТЕРСТВО ОСВІТИ І НАУКИ УКРАЇНИ  
## КИЇВСЬКИЙ ФАХОВИЙ КОЛЕДЖ ЗВ’ЯЗКУ  

---

# ЗВІТ  
## про виконання work-case №3 
### з дисципліни «Операційні системи»

---

**Виконала:**  
студентка групи **БІКС-33**  
**Сербіна Ярослава Вячеславівна**

---

**Перевірила:**  
**Сушанова Вікторія Сергіївна**

---

**Київ — 2026**

---

# Work-case №3
## Операційні системи

---

### 1. Клонування та експорт віртуальної машини
## 1.1 Клонування віртуальної робочої ОС

У середовищі Oracle VirtualBox було виконано клонування віртуальної машини VM2_Linux_CLI, створеної у Work-case 2.

- Крок 1. Вибір машини для клонування

<img width="659" height="192" alt="image" src="https://github.com/user-attachments/assets/044a961a-ca0a-4e70-93e4-2ab54ee0612e" />

Скрін 1 – Виклик команди «Клонувати…»

---

- Крок 2. Налаштування параметрів клонування

У вікні «Клонувати віртуальну машину» було виконано такі налаштування:
- Назва нової ВМ: VM2_Linux_CLI клон
- Тип клонування: Повний клон (Full Clone)
- Зріз: Current Machine State
- MAC Address Policy: за замовчуванням
- Опції Keep Disk Names та Keep Hardware UUIDs – не відмічались

Повний клон створює незалежну копію диска та налаштувань ВМ.

<img width="957" height="624" alt="image" src="https://github.com/user-attachments/assets/9970f21b-10c1-4d8e-9606-cc334838eb9c" />

Скрін 2 – Вікно налаштування параметрів клону

---

- Крок 3. Результат клонування

Після завершення процесу у списку VirtualBox Manager з’явилась нова віртуальна машина.

<img width="611" height="225" alt="image" src="https://github.com/user-attachments/assets/ac3d76f7-30b4-4418-b28c-12a316038a8c" />

Скрін 3 – Список віртуальних машин після клонування

## 1.2 Експорт віртуальної машини в OVA-формат

Для перенесення віртуальної ОС у інше віртуальне середовище використовується функція експорту.

- Крок 1. Виклик команди експорту

У меню VirtualBox було обрано:
Файл → Експортувати образ віртуальної машини

<img width="536" height="203" alt="image" src="https://github.com/user-attachments/assets/934833f2-7993-4961-a3e9-b9eadbd64678" />

Скрін 4 – Меню «Експортувати образ віртуальної машини»

---

- Крок 2. Вибір машини для експорту

У списку було обрано необхідну віртуальну машину для експорту.

<img width="623" height="294" alt="image" src="https://github.com/user-attachments/assets/53e07ade-be52-4565-91bd-add144a60d7f" />

Скрін 5 – Вікно вибору віртуальної машини

---

- Крок 3. Налаштування формату експорту

У розділі Format settings було обрано:
- Формат: Open Virtualization Format 1.0
- Розширення файлу: .ova
- Увімкнено: Write Manifest File
- ISO-образ не включався

Файл було збережено у вибрану директорію.

<img width="714" height="272" alt="image" src="https://github.com/user-attachments/assets/d586cce8-5e14-4d8b-9904-bc7cad2bc439" />

Скрін 6 – Вікно Format settings (OVA формат)

---

**Пояснення**

Клонування дозволяє створити повну копію віртуальної машини для тестування або резервування.
Експорт у форматі OVA дозволяє перенести віртуальну машину в інше середовище (наприклад, VMware або інший комп’ютер).

---

## 2. Організація мережевих з’єднань у VirtualBox

У середовищі VirtualBox підтримуються різні типи мережевих підключень між віртуальними машинами. Нижче наведено їх опис та особливості.

### NAT (Network Address Translation)

NAT дозволяє віртуальній машині отримувати доступ до Інтернету через основну операційну систему.  
Віртуальна машина використовує IP-адресу хоста, але при цьому інші пристрої локальної мережі не можуть напряму підключитися до неї.

**Особливість:**
- Є доступ до Інтернету
- Немає прямого доступу між віртуальними машинами
- Найбільш безпечний варіант

---

### Bridged Adapter (Мережевий міст)

У цьому режимі віртуальна машина підключається безпосередньо до фізичної мережі, як окремий комп’ютер.

**Особливість:**
- Отримує IP-адресу з тієї ж мережі, що й хост
- Видима для інших пристроїв у мережі
- Підходить для серверних рішень

---

### Host-only Adapter (Лише головний адаптер)

Створюється окрема ізольована мережа між хостом та віртуальними машинами.

**Особливість:**
- Віртуальні машини можуть спілкуватися між собою
- Є доступ до хоста
- Немає прямого доступу до Інтернету (якщо не додати другий адаптер NAT)

---

### Internal Network (Внутрішня мережа)

Створюється повністю ізольована мережа лише між віртуальними машинами.

**Особливість:**
- Машини бачать лише одна одну
- Немає доступу до хоста
- Немає доступу до Інтернету

---

### Перелік типів мереж у налаштуваннях VirtualBox

<img width="665" height="417" alt="image" src="https://github.com/user-attachments/assets/b594c696-0c77-47e4-ad9e-26c1cfbb2a22" />

## 3. Розгортання мережі між робочою ОС та її клоном
### 3.1 Налаштування мережевих адаптерів

Для організації взаємодії між віртуальною машиною та її клоном було налаштовано два мережеві адаптери:
- Adapter 1 — NAT (для доступу до Інтернету)
- Adapter 2 — Host-Only Adapter (для локальної мережі між ВМ)

Налаштування виконано у:
```bash
Settings → Network
```

<img width="1251" height="415" alt="image" src="https://github.com/user-attachments/assets/25aea7e8-eea1-4713-b899-34d5fb6d8838" />

<img width="1257" height="379" alt="image" src="https://github.com/user-attachments/assets/36deff64-2f7e-4524-bd43-2e5862f629b4" />

Скрін 1 — Налаштування мережевих адаптерів основної віртуальної машини (NAT + Host-Only).

### 3.2 Перевірка IP-адрес

Для перевірки мережевих параметрів використано команду:
```bash
ip a
```

<img width="1036" height="787" alt="image" src="https://github.com/user-attachments/assets/5474e7eb-9e23-47f5-8d09-87a49ebba616" />

Скрін 2 — IP основної ВМ (inet 192.168.56.102)

---

<img width="1086" height="846" alt="image" src="https://github.com/user-attachments/assets/68df7fdb-1244-4421-b48f-6b05ead1ebca" />

Скрін 3 — IP клону(inet 192.168.56.101)

### 3.3 Перевірка локального з’єднання (ping)

На основній ВМ:
```bash
ping 192.168.56.102
```
<img width="783" height="403" alt="image" src="https://github.com/user-attachments/assets/7f6bdc62-f952-495f-8f14-04a369258046" />

Скрін 4 — Ping з основної ВМ

--- 

На клоні:
```bash
ping 192.168.56.101
```
<img width="744" height="460" alt="image" src="https://github.com/user-attachments/assets/03ab2931-685b-4ff0-9f91-59fab09c813b" />

Скрін 5 — Ping з клону

### 3.4 Перевірка доступу до Інтернету

Було відкрито браузер Firefox та переглянуто відео на YouTube.

<img width="1053" height="838" alt="image" src="https://github.com/user-attachments/assets/50cf235a-62ae-49b3-84e3-8099f8014257" />

Скрін 6 — YouTube на основній ВМ

---

<img width="833" height="754" alt="image" src="https://github.com/user-attachments/assets/3064e44b-7341-4a9f-bc1c-8c1dd1832c69" />

Скрін 7 — YouTube на клоні

### 3.5 Обмін повідомленнями через netcat

Встановлення:
```bash
sudo apt install netcat-openbsd
```

На клоні (клієнт):
```bash
nc -l 1234
```

<img width="438" height="69" alt="image" src="https://github.com/user-attachments/assets/7d74923c-8e29-42d0-9459-95b4a94aa4f5" />

Скрін 8 — Запуск nc -l 1234

На основній ВМ (сервер):
```bash
nc 192.168.56.101 1234
```

<img width="788" height="111" alt="image" src="https://github.com/user-attachments/assets/d7d88bb2-60dd-466b-9738-efdd271871ff" />

Скрін 9 — Передача повідомлення

### 3.6 Налаштування спільної папки (Samba)

На основній ВМ

Створення папки:
```bash
mkdir ~/shared
```

Створення тестового файлу:
```bash
echo "Test from Main VM" > ~/shared/test.txt
```
<img width="1147" height="118" alt="image" src="https://github.com/user-attachments/assets/50a4f610-7fdb-43d7-8556-83b969025383" />

Скрін 10 — Створення shared та test.txt

Редагування smb.conf
```bash
sudo nano /etc/samba/smb.conf
```
Додано:
```bash
[shared]
path = /home/yaroslava/shared
browsable = yes
read only = no
guest ok = yes
force user = yaroslava
create mask = 0777
directory mask = 0777
```

<img width="1044" height="871" alt="image" src="https://github.com/user-attachments/assets/682eb5c8-bd70-4ae3-9c18-19d29721a30c" />

Скрін 11 — Файл smb.conf після редагування

Перезапуск служби:
```bash
sudo systemctl restart smbd
```

<img width="1028" height="853" alt="image" src="https://github.com/user-attachments/assets/1eb1c06c-28bd-4862-9e23-0a7696962a35" />

Скрін 12 — Status smbd

### 3.7 Монтування папки на клоні

Створення точки монтування:
```bash
mkdir ~/shared_from_main
```

Монтування:
```bash
sudo mount -t cifs //192.168.56.102/shared ~/shared_from_main -o guest
```

<img width="1060" height="145" alt="image" src="https://github.com/user-attachments/assets/247ecf5f-c7e2-4aba-8e4a-c8602220938a" />

Скрін 13 — Успішне монтування мережевої папки з основної ВМ на клон

Копіювання файлу:
```bash
cp ~/shared_from_main/test.txt ~/Desktop/
```

<img width="837" height="100" alt="image" src="https://github.com/user-attachments/assets/c1a1e6ce-3fa9-497c-8392-39c3736bde57" />

Скрін 14 — Файл на Desktop клону
