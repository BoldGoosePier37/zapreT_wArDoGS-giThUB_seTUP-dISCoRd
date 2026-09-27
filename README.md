# BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd — сборка под War Dogs + Discord

Форк [BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd](https://github.com/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd), заранее настроенный так, чтобы работали **War Dogs** и **Discord** одновременно.

Главное отличие от оригинала — файл **`AUTO-PICK-ZAPRET.bat`**: он сам перебирает стратегии и останавливается на той, что работает сегодня. Руками по одной запускать больше не нужно.

## Как пользоваться

1. Скачать репозиторий: зелёная кнопка **Code → Download ZIP**
2. ПКМ по архиву → **Свойства** → галочка **«Разблокировать»** → ОК
3. Распаковать в путь **без кириллицы и пробелов** — например `C:\zapret`
4. ПКМ по **`AUTO-PICK-ZAPRET.bat`** → **«Запуск от имени администратора»**

Скрипт перебирает стратегии и на каждой проверяет три адреса Discord — сайт, gateway и CDN. Останавливается на первой, где отвечают все три, и оставляет её работать. Занимает от нескольких секунд до пары минут.

Доступность античита War Dogs проверяется отдельно и **на выбор стратегии не влияет** — почему, см. ниже.

Первой всегда пробуется `general (ALT11)` — она подтверждённо работает с War Dogs.

Результат последнего запуска пишется в `auto-pick-last-run.txt`.

## Что уже настроено

| Настройка | Значение | Зачем |
|---|---|---|
| Game Filter | `enabled (UDP)` | War Dogs использует UDP на портах выше 1023 |
| IPSet Filter | `any` | под фильтр попадает любой IP игры |
| `lists/list-general.txt` | 105 строк | штатные домены + Cloudflare + `codefusion.technology` (античит) |
| `lists/list-exclude.txt` | 129 строк | штатные исключения + Яндекс, Teams и прочее |

Списки — **надстройка** над оригинальными: все домены Discord и YouTube из штатной сборки на месте, ничего не удалено. Поэтому Discord не ломается.

### Почему античит не влияет на выбор стратегии

Все 8 доменов античита (`ac-*.codefusion.technology`) присутствуют **одновременно** в `list-general.txt` и в `list-exclude.txt`. В winws исключения имеют приоритет над списком обхода, поэтому zapret пропускает этот трафик нетронутым — при любой стратегии.

Скорее всего так и задумано: вмешиваться в трафик античита — плохая идея. Но следствие важно понимать: **по доступности античита нельзя отличить одну стратегию от другой**, результат будет одинаковым хоть с обходом, хоть без него. Поэтому `AUTO-PICK` выбирает стратегию по Discord, а античит показывает справочно — если он не отвечает, менять стратегию бессмысленно, проблема в сети.

Если захотите, чтобы античит всё же обходился, удалите строки `codefusion` из `lists/list-exclude.txt`. Конфиг из Discord-гайда я оставил как есть, потому что он у вас рабочий.

## Если не работает

- **Ни одна стратегия не прошла** — скрипт напишет, какая была лучшей, и запустит её. Часто этого достаточно.
- **`winws.exe` не стартует** — почти всегда антивирус забрал `WinDivert`. Добавьте папку в исключения или отключите детект PUA.
- **Нет прав администратора** — без них WinDivert не загрузится, обход не заработает в принципе.
- **Голосовой чат Discord висит на «подключении»** — нужны записи в `hosts`: запустите `service.bat` → пункт **9. Update Hosts File**. На машине, где диск откатывается после сессии, это придётся делать каждый раз.
- **Тормозят посторонние сайты** — это цена режима `IPSet any`. Вернуть: `service.bat` → **5. IPSet Filter**. Полный список лежит в `lists/ipset-all.txt.backup`.

## Ручной режим

Автоподбор ничего не ломает в оригинальной сборке — все штатные файлы на месте. Если хочется по-старому, просто запускайте `general (ALT11).bat` или любой другой напрямую, как раньше.

## Откуда взялся конфиг

Связку «ALT11 + Game Filter UDP + IPSet any + подменённые списки» подсказали на официальном Discord-сервере War Dogs. Стратегии со временем перестают работать и зависят от провайдера — поэтому и нужен автоподбор.

## Лицензия и происхождение

Оригинальный README сохранён рядом — [README-UPSTREAM.md](README-UPSTREAM.md), там полная документация по всем стратегиям и настройкам.

Оригинальный проект — [BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd](https://github.com/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd), лицензия MIT. Бинарники в `bin/` взяты из [bol-van/zapret-win-bundle](https://github.com/bol-van/zapret-win-bundle) — их можно сверить по контрольным суммам с оригиналом.

Отдельная благодарность [bol-van](https://github.com/bol-van) — автору [zapret](https://github.com/bol-van/zapret).

---

<p align="center">
  <a href="https://github.com/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd/releases/tag/1.10.3" target="_blank">
    <img src="https://img.shields.io/github/downloads/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd/total.svg?style=for-the-badge&logo=github&label=Downloads&color=0077FF" alt="Downloads">
  </a>
  <a href="https://github.com/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd/releases/tag/1.10.3" target="_blank">
    <img src="https://img.shields.io/github/v/tag/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd?style=for-the-badge&logo=github&label=Version&color=0077FF" alt="Version">
  </a>
  <a href="https://github.com/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd/releases/latest" target="_blank">
    <img src="https://img.shields.io/github/release-date-pre/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd?style=for-the-badge&logo=github&label=Last%20release&color=0077FF" alt="Last release">
  </a>
  <a href="https://github.com/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd/issues" target="_blank">
    <img src="https://img.shields.io/github/issues/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd?style=for-the-badge&logo=github&label=Issues&color=0077FF" alt="Issues">
  </a>
  <a href="https://github.com/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd/blob/main/LICENSE.txt" target="_blank">
    <img src="https://img.shields.io/github/license/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd?style=for-the-badge&logo=github&label=License&color=0077FF" alt="License">
  </a>
  <a href="https://github.com/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd/graphs/contributors" target="_blank">
    <img src="https://img.shields.io/github/contributors/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd?style=for-the-badge&logo=github&label=Contributors&color=0077FF" alt="Contributors">
  </a>
</p>

<p align="center">
  <a href="https://github.com/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd" target="_blank">
    <img src="https://img.shields.io/badge/Built%20with-Bash-blueviolet?style=for-the-badge&logo=gnu-bash&logoColor=white" alt="Built with Bash">
  </a>
  <a href="https://github.com/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd" target="_blank">
    <img src="https://img.shields.io/badge/Platform-Windows-informational?style=for-the-badge&logo=windows&logoColor=white" alt="Platform Windows">
  </a>
</p>

---

## NEW

> ⚠️ **Важно!**
>
> Внимательно прочитайте этот раздел, прежде чем использовать скрипт.
>
> **Антивирус:** Многие антивирусы детектируют `WinDivert.dll` и `WinDivert64.sys` как вредоносное ПО. Если у вас возникли проблемы с запуском `winws.exe`, добавьте папку с распакованным архивом в исключения антивируса или отключите детект PUA (Potentially Unwanted Application).
>
> **Права администратора:** Для корректной работы WinDivert необходимы права администратора. Запускайте `AUTO-PICK-ZAPRET.bat` через контекстное меню «Запуск от имени администратора».

---

## ФЕЙКИ

<details>
<summary>Подробнее о методах обхода</summary>

В репозитории присутствует несколько BAT-файлов, предназначенных для обхода блокировок. Основные методы, используемые в скриптах:

*   **FAKE TLS AUTO:** Имитация TLS-соединения для обхода DPI.
*   **SIMPLE FAKE:** Упрощенный метод имитации трафика.
*   **ALT:** Альтернативные варианты настройки, часто включающие модифицированные списки доменов.

Эти методы помогают маскировать трафик под легитимные соединения, что затрудняет его идентификацию и блокировку провайдерами.

</details>

---

## АНТИВИРУСЫ

<details>
<summary>Взаимодействие с антивирусами</summary>

Как упоминалось ранее, компоненты `WinDivert` могут детектироваться антивирусными программами. Это связано с их функциональностью, позволяющей перехватывать и модифицировать сетевой трафик.

**Рекомендации:**

1.  **Добавление в исключения:** Добавьте папку, где находится распакованный архив, в список исключений вашего антивируса.
2.  **Отключение детектирования PUA:** Если ваш антивирус имеет опцию отключения детектирования потенциально нежелательных приложений (PUA), активируйте её.

Без этих мер `winws.exe` может не запускаться, что приведет к невозможности работы обхода.

</details>

---

## Поддержка проекта

<details>
<summary>Как помочь проекту</summary>

Если вы нашли ошибку, у вас есть предложение по улучшению или вы хотите внести свой вклад в развитие проекта, пожалуйста, ознакомьтесь с разделом [Issues](https://github.com/BoldGoosePier37/zapreT_wArDoGS-giThUB_seTUP-dISCoRd/issues) на GitHub.

Вы также можете:

*   Форкнуть репозиторий и предложить свои изменения через Pull Request.
*   Сообщить о проблеме, описав шаги для её воспроизведения.

Спасибо за вашу поддержку!
</details>