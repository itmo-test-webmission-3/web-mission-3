# Часть 0 - создаем базу данных  
https://drive.google.com/file/d/1GuZ1_s_fDpWvgYCR6wCvUsLq6gkuE2fg/view?usp=sharing
# Часть 1 - авторизация  
https://drive.google.com/file/d/18iBmi2UmMBjWAnJeWH2xs1qGjN9E2ZFG/view?usp=sharing  
# Часть 2 - отправка сообщений   
https://drive.google.com/file/d/1dydioIEnSCHdDqOLH_BRV2TfvCTP76sK/view?usp=sharing  
# Часть 3 - select’ы
1. Получить список юзернеймов пользователей  
```sql  
SELECT username
FROM users
```  
2. Получить кол-во отправленных сообщений каждым пользователем  
```sql  
SELECT users.username, count(messages.id) as number_of_sent_messages  
FROM users  
LEFT JOIN messages  
ON users.id = messages.sender  
GROUP BY users.username  
ORDER BY number_of_sent_messages
```
3. Получить пользователя с самым большим кол-вом полученных сообщений и само количество
```sql
SELECT users.username, count(messages.id) as number_of_received_messages
FROM users
LEFT JOIN messages
ON users.id = messages.to
GROUP BY users.username
ORDER BY number_of_received_messages DESC
LIMIT 1
```
4. Получить среднее кол-во сообщений, отправленное каждым пользователем
```sql
SELECT users.username, COALESCE(FLOOR(AVG(messages.id)), 0) as avg_number_of_sent_messages
FROM users
LEFT JOIN messages
ON users.id = messages.sender
GROUP BY users.username
ORDER BY avg_number_of_sent_messages
```
