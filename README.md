# geoip_russia

Кастомный `geoip.dat` и `sing-box` rule-set для Xray / v2fly / Sing-box / Happ и других клиентов.

Репозиторий автоматически подготавливает и публикует набор GeoIP-категорий, полезных для маршрутизации и обхода блокировок в России.

## 📦 Состав

В итоговом `geoip.dat` и `sing-box` rule-set планируются следующие категории:

- `ru-blocked`
- `cloudflare`
- `cloudfront`
- `facebook`
- `fastly`
- `google`
- `netflix`
- `telegram`
- `twitter`
- `ddos-guard`
- `yandex`
- `ru`
- `private`

## ⬇️ Скачать

### GeoIP

`https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip.dat`

Контрольная сумма:

`https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip.dat.sha256`

### Sing-box

Архив со всеми файлами:

`https://github.com/yularzhi/geoip_russia/releases/latest/download/sing-box-rule-set-geoip.zip`

Файлы:

| Категория | Raw-ссылка |
| --- | --- |
| `ru-blocked` | `https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip-ru-blocked.srs` |
| `ru-whitelist` | `https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip-ru-whitelist.srs` |
| `cloudflare` | `https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip-cloudflare.srs` |
| `cloudfront` | `https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip-cloudfront.srs` |
| `facebook` | `https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip-facebook.srs` |
| `fastly` | `https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip-fastly.srs` |
| `google` | `https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip-google.srs` |
| `netflix` | `https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip-netflix.srs` |
| `telegram` | `https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip-telegram.srs` |
| `viber` | `https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip-viber.srs` |
| `twitter` | `https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip-twitter.srs` |
| `ddos-guard` | `https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip-ddos-guard.srs` |
| `yandex` | `https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip-yandex.srs` |
| `ru` | `https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip-ru.srs` |
| `private` | `https://github.com/yularzhi/geoip_russia/releases/latest/download/geoip-private.srs` |

## ⚙️ Использование

Примеры тегов:

- `geoip:ru-blocked`
- `geoip:cloudflare`
- `geoip:cloudfront`
- `geoip:facebook`
- `geoip:fastly`
- `geoip:google`
- `geoip:netflix`
- `geoip:telegram`
- `geoip:twitter`
- `geoip:ddos-guard`
- `geoip:yandex`
- `geoip:ru`
- `geoip:private`

Для `sing-box` используй `rule_set` с файлами из `release/sing-box/rule-set-geoip/`, например `geoip-ru-blocked.srs`.

## 🔄 Автоматизация

Репозиторий автоматически:
- скачивает исходные текстовые IP/CIDR-списки
- нормализует их
- подготавливает конфигурацию сборки
- конвертирует `geoip.dat` в `sing-box` `srs`
- публикует итоговые файлы в ветку `release`

Обновление выполняется ежедневно через GitHub Actions.

## 📚 Источники

### 🇷🇺 Заблокированные в РФ сети
- [runetfreedom/russia-blocked-geoip](https://github.com/runetfreedom/russia-blocked-geoip)

### 📦 Upstream GeoIP
- [v2fly/geoip](https://github.com/v2fly/geoip)
- [Loyalsoldier/geoip](https://github.com/Loyalsoldier/geoip)

## 🙏 Благодарности

Огромное спасибо авторам следующих проектов:

### 🔹 runetfreedom
https://github.com/runetfreedom/russia-blocked-geoip  
За GeoIP-категории по заблокированным в России адресам и сетям.

### 🔹 v2fly
https://github.com/v2fly/geoip  
За базовый GeoIP toolchain и экосистему V2Ray/Xray.

### 🔹 Loyalsoldier
https://github.com/Loyalsoldier/geoip  
За расширенные GeoIP-сборки и идеи кастомизации.

## ⚠️ Примечания

- `ru-blocked` берётся из источников `runetfreedom`
- дополнительные популярные сети берутся из их же GeoIP-модели
- `ru` и `private` опираются на upstream GeoIP-источники

## 📄 Лицензия

Репозиторий агрегирует данные из сторонних источников.  
Лицензии и условия использования смотри в исходных проектах.

## 💬 Обратная связь

Если хочешь улучшить список категорий или добавить новые — создавай issue или pull request.
