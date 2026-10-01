# I-0 — Capacitor technical spike

Статус: **частично выполнен; device validation остаётся обязательной перед закрытием I-0**.

## Что проверено в рамках автономной реализации

Клиент зафиксирован на Capacitor 8 и содержит foundation/кандидаты для обязательных capabilities:

| Capability | Foundation / candidate | Статус в этой среде |
|---|---|---|
| secure storage | `@aparajita/capacitor-secure-storage` | adapter реализован; native runtime не запускался |
| SQLite | `@capacitor-community/sqlite` | dependency зафиксирована; device runtime не запускался |
| camera | `@capacitor/camera` | dependency зафиксирована; device runtime не запускался |
| GPS | `@capacitor/geolocation` | dependency зафиксирована; device runtime не запускался |
| push | `@capacitor/push-notifications` | dependency зафиксирована; credentials/device runtime не доступны |
| background execution | `@capacitor/background-runner` | candidate зафиксирован; OS kill/recovery не проверены |
| MapLibre | `maplibre-gl` | dependency зафиксирована; native WebView/offline tiles не проверены |
| media upload/resume | HTTP/application-level mechanism | реализация media domain вне I-0; native interruption test не выполнен |

## Что нельзя достоверно проверить в текущей среде

Среда автономного выполнения не предоставляет Android SDK/emulator, Xcode/iOS simulator, физические устройства, APNs/FCM/RuStore credentials и возможность воспроизводить OS kill/background ограничения. Поэтому нельзя утверждать, что следующие пункты прошли acceptance test:

- background sync после сворачивания приложения;
- восстановление фоновой операции после OS kill;
- push delivery на Android/iOS;
- реальная Keychain/Keystore запись и восстановление после restart;
- SQLite/SQLCipher на реальном устройстве;
- MapLibre + offline tiles в native WebView;
- camera/GPS permission lifecycle;
- resumable media upload при потере сети.

## Обязательная device matrix перед merge/закрытием I-0

Минимум один поддерживаемый Android 9+ device/emulator и один iOS 15+ device/simulator. Для каждого пункта выше записать: OS/device, plugin version, шаги, observed result, ограничения. OS-kill проверки предпочтительно выполнять на физическом Android и iPhone, потому что simulator/emulator не полностью воспроизводят ограничения фонового исполнения.

## Вывод

Архитектурный риск не замаскирован: persistence/token abstractions и зависимости заложены, но device-dependent часть spike остаётся явным blocking item для формального Definition of Done I-0.
