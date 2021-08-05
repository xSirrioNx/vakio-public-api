# vakio-public-api
Открытый API для интеграции приборов Vakio в системы умного дома

### Регистрация

1) Загрузите приложение Vakios Smart Control с App store или Google Play.
2) Зарегистрируйтесь и подтвердите Email.
3) Отправьте письмо на почту developer@vakio.ru с пометкой "Регистрация индивидуального API", в тексте укажите Email, имя и номер теелфона, которые относятся к этому аккаунту.
4) Мы вышлем вам данные для авторизации.

### Получение токена для авторизации с помощью пароля

*Адрес* 
```
POST https://api.vakio.ru/oauth/token
```
*Заголовки* 
```
headers: {
    'Content-Type': 'application/json'
},
```
*Тело*
```
{
    "client_id": "<client_id>",
    "client_secret": "<client_secret>",
    "grant_type": "password",
    "username": "<you email>",
    "password": "<your password, not SHA1ed>"
}
```

### Получение Refresh токена

*Адрес* 
```
POST https://api.vakio.ru/oauth/token
```
*Заголовки* 
```
headers: 
{
    'Content-Type': 'application/json'
},
```
*Тело*
```
{
    "client_id": "<client_id>",
    "client_secret": "<client_secret>",
    "grant_type": "refresh_token",
    "refresh_token": "<you refresh_token>",
}
```
*Успешный ответ*
```
{
    "access_token": "f33e31633a2d70c29ef13adef639c36dc1445a93",
    "expires_in": 86400,
    "token_type": "Bearer",
    "scope": null,
    "refresh_token": "24bbee6297ee59d3b25e145a758cdf2b6504f39f"
}
```

### Получение данных обо всех устройствах пользователя

*Адрес* 
```
GET https://api.vakio.ru/devices
```
*Заголовки* 
```
headers: {
    'Content-Type': 'application/json',
    Authorization: 'Bearer <token>',
},
```
*Успешный ответ*
```
{
    "code": 200,
    "content": [
        {
            "id": 19,
            "device_name": "Мой прибор 1",
            "device_type": {
                "name": "Vakio Plus Series",
                "slug": "vakio-window-plus",
                "image": "https://connect.vakio.ru/wp-content/uploads/vakio-window-plus.jpg",
            },
            "device_group": "кухня",
            "capabilities": {
                "on_off": "off",
                "mode": "inflow",
                "speed": "5"
            },
            "properties": [],
            "relation": {
                            "on_off_dependence":"<on/off>",
                            *// Для Atmosphere*
                            "dependence":{
                                "mode":"<inflow/outflow/recuperator>",
                                "device_id_master":"<device_id_master>",
                                "min_value":"<device_id_master>",
                                "step":"<device_id_master>",
                                "parametr":"<co2/temp/hud>"
                            }
                            *// Для Base Smart*
                            "dependence":{
                                "mode":"<sync/async>",
                                "device_id_master":"<device_id_master>",
                            }
                        },
            "verified": 1,
            "device_type_id": 2
        }
    ]
}
```
    
    
### Получение данных об устройстве пользователя

*Адрес* 
```
POST /devices/{DEVICE_ID}
```
*Заголовки* 
```
headers: {
    'Content-Type': 'application/json',
    Authorization: 'Bearer <token>',
},
```

*Успешный ответ*
```
см. Получение данных обо всех устройствах пользователя
```
