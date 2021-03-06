# Звіт до лабораторної роботи 1
### Тема: _Дослідження роботи мережі згідно моделі OSI._
### Мета роботи: _Дослідити роботу мережевих пристроїв та прослідкувати як опрацьовуються дані на різних рівнях моделі OSI._
---
## Хід роботи
1. Скласти схему мережі у `Packet Tracer` та перейти у `Simulation mode`. (Вибірково: вибрати вкладку `Edit Filters` та зняти галочки зі всіх протоколів окрім ICMP, HTTP, HTTPS);
1. В процесі виконання роботи занотуйте всі відповіді та внесіть їх у звіт.
1. Запустити команду `ping` між комп’ютерами що під’єднані до повторювача (hub) та прослідкувати передачу пакетів між ними;
    - Кому належить (якому пристрою) MAC адреса призначення кадру (destination МАС)?
    
    **Відповідь: Пристрою, на який була спрямована команда ping**
    
    - Чи змінювалась адреса MAC після проходження повторювача (hub)?
    
    **Відповідь: Не змінювалась**
    
    - При проходженні кадру, яка інформація (дані) та якого рівня опрацьовуються на повторювачі (hub)?
    
    **Відповідь: На повторювачі опрацьовуються дані фізичного рівня моделі OSI. Цей рівень приймає кадр даних від канального рівня, кодує його в послідовність сигналів, які потім передаються у лінію зв'язку. Передача кадру даних через лінію зв'язку вимагає від фізичного рівня визначення таких елементів: тип середовища передавання; як повинні бути представлені біти даних у середовищі передавання; як кодувати дані; якими повинні бути схеми приймача і передавача.**
    
    - Чи можливе виникнення колізії на повторювачі (hub)?
    
    **Відповідь: Так**
    
    - Що стається з кадром при виникненні колізії?
    
    **Відповідь: Кадр втрачається**
    
    - Який рівень моделі OSI визначає чи кадр належить даному пристрою?
    
    **Відповідь: Канальний рівень (Data Link layer)**
    
    - Що стається з кадрами які надійшли на комутатор або на комп’ютери яким він не призначений?
   
    **Відповідь: Кадр буде відкинутий**
    
1. Запустити команду `ping` між комп’ютерами що під’єднані до комутатора (switch) та прослідкувати як комутатор опрацьовує дані.
    - Чия адреса MAC встановлюється у поле призначення кадру?
    
    **Відповідь: Пристрою, на який була спрямована команда ping**
    
    - Чи змінювалась адреса MAC після проходження комутатора (Switch)?
    
    **Відповідь: Не змінювалась**
    
    - При проходженні кадру, яка інформація (дані) та якого рівня опрацьовуються на комутаторі (switch)?
    
    **Відповідь: На комутаторі опрацьовуються дані канального рівня. На канальному рівні отримані з фізичного рівня дані упаковуються в кадри даних, перевіряються на цілісність, якщо потрібно — виправляються помилки й відправляються на мережний рівень.**
    
    - Чи можливе виникнення колізій на комутаторі (switch)? Чому?
    
    **Відповідь: Виникнення колізій на комутаторі не можливе. В комутаторі не використовується спільне середовище для передачі даних. Отриманий кадр комутатор відправляє лише на один потрібний вихідний порт, а не на всі. Якщо комутатору треба направити декілька кадрів на один порт, він зберігає їх у буфер та відправляє їх по черзі**
    
    - Зайдіть у командне вікно комутатора (вкладка CLI) та введіть наступні команди (команди вказані після символів > та #):
        ```shell script
        Switch> enable
        Switch# show mac-address-table
        ```
        ![alt text](https://github.com/sonyk33/Trishch---Lab---TOTK---2021-/blob/main/Lab-1/l1.png)
        
1. Яким пристроям належать МАС адреси що містяться в таблиці?

    **Відповідь: МАС адреси належать пристроям, на які були відправлені кадри**
    
    - Чи можливо що декілька МАС адрес прив’язані до одного порту в МАС таблиці комутатора? Чому і що це за адреси?
    
    **Відповідь: Так, це адреси пристроїв, які підключені до хабу**
    
1. Виконати наступні завдання:
    - На якому рівні моделі OSI працює комутатор (Switch)?
    
    **Відповідь: Канальний рівень**
    
    - Чи можливо запустити команду ping між комп’ютером та комутатором (switch)?
    
    **Відповідь: Так**
    
    - Із двох будь-яких комп’ютерів під’єднаних до одного комутатора запустіть команду ping 192.168.0.5 або ping 192.168.100.5 або ping 172.16.0.5 . Який пристрій опрацьовує дані? Яка МАС адреса встановлюється у поле адресата? Чому?
    
    **Відповідь: Дані опрацьовує комутатор. У поле адресата встановлюється MAC адреса мережі управління VLAN комутатора. МАС адреса береться з таблиці МАС адрес.**
    
    - Чому комутатор (switch) має одну ІР адресу яка доступна зі всіх портів?
    
    **Відповідь: Тому що, на комутаторах Cisco за замовчуванням на кожному порті доступна мережа управління VLAN1**
    
1. Запустити команду `ping` між комп’ютерами що знаходяться в різних мережах та прослідкувати як маршрутизатор опрацьовує пакети.
    - Запустити ping між комп’ютерами LAN_1 та LAN_2. Чия МАС адреса встановлюється у поле одержувача (destination)?
    
    **Відповідь: МАС адреса шлюзу мережі, з якої була відправлена команда ping**
    
    - Що таке шлюз мережі (gateway)? Вказати IP та МАС адреси шлюзу для кожної мережі (LAN_1, LAN_2, та LAN_3).
    
    **Відповідь: Шлюз - це вузол комп'ютерної мережі(маршрутизатор),який забезпечує вихід до іншої мережі**
      Мережа | МАС адреса | ІР адреса
      --- | --- | ---
      **LAN_1**|0060.4799.1301|192.168.0.1/24
      **LAN_2**|0060.4799.1302|192.168.100.1/24
      **LAN_3**|0002.177Е.А501|172.16.0.1/24
    
    - Чи змінювалась адреса MAC після проходження маршрутизатора (Router_LAN_1)? 
    
    **Відповідь: Так**
    
    - Чи змінюється ІР адреса після проходження маршрутизатора (Router_LAN_1)?
    
    **Відповідь: Ні**
    
    - При проходженні пакету, яка інформація (дані) та якого рівня опрацьовуються на маршрутизаторі (router)?
    
    **Відповідь: На маршрутизаторі опрацьовуються дані мережевого рівня. Цей рівень призначений для визначення шляху передачі даних. Відповідає за трансляцію логічних адрес й імен у фізичні, визначення найкоротших маршрутів, комутацію й маршрутизацію пакетів, відстеження неполадок і заторів у мережі.**
    
    - Зайдіть у командне вікно маршрутизатора (вкладка `CLI`) та введіть наступні команди (команди вказані після символів > та #):
        ```shell script
        Router> enable
        Router# show ip route
        ```
        ![alt text](https://github.com/sonyk33/Trishch---Lab---TOTK---2021-/blob/main/Lab-1/l1.2.png)
        
1. Маршрути до яких мереж присутні в таблиці маршрутизації? Вказати через які порти маршрутизатора доступна кожна з мереж.

    **Відповідь: Доступні маршрути до мереж LAN_1 та LAN_2. Мережа LAN_1 доступна через порт FastEthernet0/0, а мережа LAN_2 - FastEthernet0/1.**
    
    - Запустити ping між комп’ютерами LAN_1 та LAN_3. Як змінюється МАС адреса на Router_LAN_1?
    
    **Відповідь:  Передача даних між Router_LAN_1 та Router_LAN_2 забезпечуються за допомогою протоколу cHDLC. Структура фрейму cHDLC відрізняється від Ethernet, у фреймі cHDLC не використовується MAC адреса**
    
    - Які поля були у кадра Ethernet та кадра HDLC? Чому у кадра HDLC немає поля адреси?
    
    **Відповідь:**
    
    **Кадр Ethernet містить поля: PREAMBLE, Start of frame delimiter (SFD), Destination Address, Source Address, Type, Data, Frame checksum (FCS).**
    
    **Кадр HDLC містить поля: Flag (FLG), Address (ADR), CONTROL, DATA, Frame checksum (FCS)**
    
    **Структура фрейму Cisco HDLC (cHDLC) відрізняється від стандартного протоколу ISO HDLC. Поле адреса використовується для вказання типу пакету, що міститься в кадрі cHDLC; 0x0F для Unicast та 0x8F для Broadcast пакетів**
    
    - Що таке преамбула (Preamble) та прапорець (FLG). Якими вони є для технології Ethernet та HDLC?
    
    **Відповідь:**
    
    **Flag - це бітова комбінація 01111110, що позначає початок та кінець кадру. **
    
    **Преамбула - це комбінація 0 і 1, яка позначає початок кадру та використовується для синхронизації**
    

