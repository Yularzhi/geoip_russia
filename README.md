# geoip_russia

[![Build geoip.dat](https://github.com/Yularzhi/geoip_russia/actions/workflows/build-geoip.yml/badge.svg)](https://github.com/Yularzhi/geoip_russia/actions/workflows/build-geoip.yml)
[![Latest Release](https://img.shields.io/github/v/release/Yularzhi/geoip_russia)](https://github.com/Yularzhi/geoip_russia/releases/latest)
[![Last Commit](https://img.shields.io/github/last-commit/Yularzhi/geoip_russia)](https://github.com/Yularzhi/geoip_russia/commits/main)

Кастомный `geoip.dat` и `sing-box` rule-set для Xray / v2fly / Sing-box / Happ и других клиентов.

Репозиторий автоматически (ежедневно) собирает и публикует набор GeoIP-категорий, полезных для маршрутизации и обхода блокировок в России.

## 📦 Состав

В итоговом `geoip.dat` и sing-box rule-set входят следующие категории:

| Категория | Источник |
| --- | --- |
| `ru-blocked` | antifilter.download (ipresolve.lst + subnet.lst) |
| `ru-whitelist` | hxehex/russia-mobile-internet-whitelist |
| `viber` | собственный список (`Data/viber.txt`, может быть неполным) |
| `ddos-guard` | MaxMind GeoLite2-ASN (по номерам AS) |
| `yandex` | MaxMind GeoLite2-ASN (по номерам AS) |
| `cloudflare`, `cloudfront`, `facebook`, `fastly`, `google`, `netflix`, `telegram`, `twitter`, `ru`, `private` | заимствованы из сборки [Loyalsoldier/geoip](https://github.com/Loyalsoldier/geoip) |

## ⬇️ Скачать

Ссылки всегда ведут на последний nightly-релиз:

### GeoIP

```
https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip.dat
```

Контрольная сумма:

```
https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip.dat.sha256
```

### Sing-box

Архив со всеми файлами:

```
https://github.com/Yularzhi/geoip_russia/releases/latest/download/sing-box-rule-set-geoip.zip
```

Файлы:

| Категория | Raw-ссылка |
| --- | --- |
| `ru-blocked` | `https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-ru-blocked.srs` |
| `ru-whitelist` | `https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-ru-whitelist.srs` |
| `viber` | `https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-viber.srs` |
| `cloudflare` | `https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-cloudflare.srs` |
| `cloudfront` | `https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-cloudfront.srs` |
| `facebook` | `https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-facebook.srs` |
| `fastly` | `https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-fastly.srs` |
| `google` | `https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-google.srs` |
| `netflix` | `https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-netflix.srs` |
| `telegram` | `https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-telegram.srs` |
| `twitter` | `https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-twitter.srs` |
| `ddos-guard` | `https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-ddos-guard.srs` |
| `yandex` | `https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-yandex.srs` |
| `ru` | `https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-ru.srs` |
| `private` | `https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-private.srs` |

## ⚙️ Использование

### Xray / V2Ray

Пример тегов в конфиге:

```json
{
  "type": "field",
  "outboundTag": "proxy",
  "domain": ["geosite:category-ru"],
  "ip": [
    "geoip:ru-blocked",
    "geoip:telegram",
    "geoip:cloudflare"
  ]
}
```

Доступные теги: `geoip:ru-blocked`, `geoip:ru-whitelist`, `geoip:viber`, `geoip:cloudflare`, `geoip:cloudfront`, `geoip:facebook`, `geoip:fastly`, `geoip:google`, `geoip:netflix`, `geoip:telegram`, `geoip:twitter`, `geoip:ddos-guard`, `geoip:yandex`, `geoip:ru`, `geoip:private`.

Установите скачанный `geoip.dat` в каталог ассетов клиента (см. документацию вашего клиента: Xray, v2fly, Happ и др.).

### Sing-box

```json
{
  "route": {
    "rule_set": [
      {
        "type": "remote",
        "tag": "geoip-ru-blocked",
        "format": "binary",
        "url": "https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-ru-blocked.srs",
        "download_detour": "direct"
      },
      {
        "type": "remote",
        "tag": "geoip-telegram",
        "format": "binary",
        "url": "https://github.com/Yularzhi/geoip_russia/releases/latest/download/geoip-telegram.srs",
        "download_detour": "direct"
      }
    ],
    "rules": [
      {
        "rule_set": ["geoip-ru-blocked", "geoip-telegram"],
        "outbound": "proxy"
      }
    ]
  }
}
```

## 🔄 Автоматизация

Репозиторий автоматически (ежедневно, GitHub Actions):

- скачивает исходные текстовые IP/CIDR-списки
- нормализует их и подготавливает конфигурацию сборки
- собирает `geoip.dat` (билдер [runetfreedom/geoip](https://github.com/runetfreedom/geoip))
- конвертирует `geoip.dat` в sing-box `srs` ([runetfreedom/geodat2srs](https://github.com/runetfreedom/geodat2srs))
- публикует итоговые файлы в ветку `release` и в GitHub Releases

## 📚 Источники

| Источник | Что берётся |
| --- | --- |
| [antifilter.download](https://antifilter.download) | списки подсетей/адресов, заблокированных в РФ (`ru-blocked`) |
| [hxehex/russia-mobile-internet-whitelist](https://github.com/hxehex/russia-mobile-internet-whitelist) | CIDR-whitelist российских мобильных сетей (`ru-whitelist`) |
| [Loyalsoldier/geoip](https://github.com/Loyalsoldier/geoip) | базовые категории (cloudflare, google, telegram, ru и др.) + GeoLite2-ASN CSV |
| [runetfreedom/geoip](https://github.com/runetfreedom/geoip) | инструмент сборки (builder) |
| [runetfreedom/geodat2srs](https://github.com/runetfreedom/geodat2srs) | конвертер dat → srs |
| [v2fly/geoip](https://github.com/v2fly/geoip) | экосистема и формат GeoIP |

## ⚠️ Примечания

- `ru-blocked` — данные antifilter (подсети, до которых наблюдаются блокировки со стороны РФ)
- `ru-whitelist` — подсети, через которые рекомендован мобильный интернет в РФ
- `viber` — собственный неполный список, пополняется вручную
- `ddos-guard` и `yandex` собираются по ASN из GeoLite2-ASN (лицензия MaxMind требует атрибуции — см. [LICENSE](LICENSE))

## 📄 Лицензия

См. [LICENSE](LICENSE). Репозиторий агрегирует данные из сторонних источников — условия их использования также описаны в LICENSE.

## 💬 Обратная связь

Хочешь добавить или улучшить категорию — создавай issue или pull request.
