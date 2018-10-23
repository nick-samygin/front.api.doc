---
title: Изменён порядок папок при поиске зависимостей 
layout: default
---
Начиная с версии 5.2 при наличии dll-файлов с одинаковыми именами в папке плагина и папке приложения iikoFront будет загружаться файл из папки плагина.

Благодаря этому плагин сможет использовать такие же сторонние библиотеки, что и приложение iikoFront (например, log4net, Rx, Razor), используя свои собственные версии этих библиотек и, таким образом, оставаясь независимым от деталей внутреннего устройства приложения iikoFront.

В версиях до 5.2 приоритет отдавался файлам из папки iikoFront, даже если у них была неподходящая версия. При разработке плагина под Api V3 или V4 следует предусмотреть возможность коллизии между версиями сторонних библиотек, используемыми и плагином, и приложением iikoFront, и либо устанавливать свои версии этих библиотек в [GAC](https://msdn.microsoft.com/en-us/library/yf1d93sz.aspx), который имеет наивысший приоритет при поиске зависимостей, либо зарегистрировать обработчик события `AppDomain.AssemblyResolve` для возможности загрузки нужных библиотек вручную.

При возникновении проблем отследить, как проходил поиск библиотеки и какой файл в итоге был загружен, можно с помощью утилиты [Fuslog](https://msdn.microsoft.com/en-us/library/e74a18c4(v=vs.110).aspx).