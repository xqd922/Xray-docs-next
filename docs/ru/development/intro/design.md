# Цели проектирования

- Ядро Xray предоставляет платформу, которая поддерживает необходимые функции сетевого прокси, и на ее основе можно выполнять дальнейшую разработку для улучшения пользовательского опыта.
- Кроссплатформенность является основным принципом, чтобы снизить затраты на вторичную разработку.

## Архитектура

![Architecture](./framework.png)

Ядро состоит из трех уровней: уровня приложений, уровня прокси и транспортного уровня.

Каждый уровень содержит несколько модулей, которые независимы друг от друга, и модули одного типа могут быть легко заменены.

### Уровень приложений

Уровень приложений содержит некоторые функции, которые часто используются на уровне прокси. Эти функции абстрагированы, чтобы их можно было повторно использовать в разных модулях прокси.

Модули уровня приложений должны быть реализованы чисто программным способом, без привязки к аппаратному обеспечению или платформе.

Список важных модулей:

- Dispatcher: используется для передачи данных, полученных входящим прокси, исходящему прокси;
- Router: модуль маршрутизации, см. [настройки маршрутизации](../../config/routing.md);
- DNS: встроенный модуль DNS-сервера;
- Proxy Manager: менеджер прокси;

### Уровень прокси

Уровень прокси делится на две части: входящий прокси (Inbound Proxy) и исходящий прокси (Outbound Proxy).

Эти две части независимы друг от друга, входящий прокси не зависит от какого-либо конкретного исходящего прокси, и наоборот.

#### Входящий прокси

- Реализует интерфейс [proxy.Inbound](https://github.com/xtls/Xray-core/blob/main/proxy/proxy.go);

#### Исходящий прокси

- Реализует интерфейс [proxy.Outbound](https://github.com/xtls/Xray-core/blob/main/proxy/proxy.go);

### Транспортный уровень

Транспортный уровень предоставляет модули инструментов, связанных с передачей сетевых данных.
