# <h2>5. Відображення User Stories у UML-нотації (Sequence Diagrams)</h2>

# 

# <p>

# Нижче наведено діаграми послідовності для двох ключових сценаріїв:

# </p>

# 

# <ul>

# &nbsp;   <li><strong>Авторизація клієнта</strong></li>

# &nbsp;   <li><strong>Виконання грошового переказу</strong></li>

# </ul>

# 

# <p>

# Діаграми подані у форматі <strong>PlantUML</strong>.

# </p>

# 

# <hr>

# 

# <h3>5.1. Діаграма послідовності: Авторизація клієнта</h3>

# 

# <pre><code>@startuml

# actor Client

# participant "Web Interface" as UI

# participant "Auth Service" as Auth

# participant "User Database" as DB

# participant "2FA Service" as MFA

# 

# Client -> UI : Вводить логін і пароль

# UI -> Auth : Передати облікові дані

# Auth -> DB : Перевірити користувача

# DB --> Auth : Результат перевірки

# 

# alt Дані коректні

# &nbsp;   Auth -> MFA : Згенерувати одноразовий код

# &nbsp;   MFA -> Client : Надіслати SMS-код

# &nbsp;   Client -> UI : Ввести код підтвердження

# &nbsp;   UI -> Auth : Перевірити код

# &nbsp;   Auth --> UI : Доступ дозволено

# &nbsp;   UI --> Client : Відображення головної сторінки

# else Дані некоректні

# &nbsp;   Auth --> UI : Помилка автентифікації

# &nbsp;   UI --> Client : Повідомлення про помилку

# end

# @enduml</code></pre>

# 

# <hr>

# 

# <h3>5.2. Діаграма послідовності: Виконання грошового переказу</h3>

# 

# <pre><code>@startuml

# actor Client

# participant "Web Interface" as UI

# participant "Transaction Service" as TS

# participant "Account Database" as DB

# participant "2FA Service" as MFA

# participant "Audit Log" as Log

# 

# Client -> UI : Ввести дані переказу

# UI -> TS : Створити транзакцію

# TS -> DB : Перевірити баланс

# 

# alt Баланс достатній

# &nbsp;   TS -> MFA : Згенерувати код підтвердження

# &nbsp;   MFA -> Client : Надіслати код

# &nbsp;   Client -> UI : Ввести код

# &nbsp;   UI -> TS : Підтвердити операцію

# &nbsp;   TS -> DB : Списати кошти

# &nbsp;   TS -> Log : Записати подію

# &nbsp;   TS --> UI : Операція успішна

# &nbsp;   UI --> Client : Підтвердження транзакції

# else Недостатньо коштів

# &nbsp;   TS --> UI : Відмова в операції

# &nbsp;   UI --> Client : Повідомлення про помилку

# end

# @enduml</code></pre>

# 

# <hr>

# 

# <h3>5.3. Висновок до розділу</h3>

# 

# <p>

# Побудовані діаграми послідовності відображають взаємодію між користувачем і компонентами системи відповідно до визначеної архітектури.

# </p>

# 

# <p>

# Вони демонструють:

# </p>

# 

# <ul>

# &nbsp;   <li>порядок викликів між компонентами системи;</li>

# &nbsp;   <li>обробку альтернативних сценаріїв (alt-блоки);</li>

# &nbsp;   <li>взаємодію із сервісами автентифікації, транзакцій та журналювання.</li>

# </ul>

# 

# <p>

# Застосування UML-нотації дозволяє формалізувати поведінку системи, зменшити неоднозначність у трактуванні вимог та забезпечити узгодженість між етапами аналізу і проєктування.

# </p>

