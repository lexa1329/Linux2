Вопросы:
Назовите основные отличия и преимущества systemd от sysvinit, опишите подходы

		Sysvinit – запускает все демоны последовательно, друг за другом, нет возможности сделать зависимость запуска одного сервиса от другого. Используется система с runlevel.
		Systemd – создаёт сокеты отдельно от запуска демонов, что позволяет начать работу намного раньше. Также systemd поддерживает множество технологий, которые не поддерживает sysvinit. в Systemd нет runlevel, 	вместо этого есть targets, определяющие зависимости одних юнитов от других.


Каким образом происходит параллельный запуск всех процессов но в то же время сервисы стартуют с нужными зависимостями друг относительно друга

	Systemd знает необходимые зависимости для каждого сервиса и может запускать сервисы без зависимостей параллельно, таким образом, для каждого сервиса поднимаются его зависимости и сам сервис. Также systemd может заранее создать сокет для сервиса, что позволит начать работу всей системы раньше.

Каким образом проверить работает процесс в sysvinit и в systemd?
	
		Sysvinit: 
			chkconfig service_name или service --status-all
		Systemd: 
			systemctl status [unit]


Как добавить в автозагрузку init скрипт в sysvinit и в systemd?
		
		Sysvinit:
			Добавить скрипт в директорию /etc/init.d
			chkconfig srvice_name on


		Systemd:
			Добавить файл с описанием модуля в /etc/systemd/system/
			sysctemctl enable service

Как посмотреть логи в системе systemd по нужному нам процесс

		journalctl -u <имя_юнита>

Задачи:
написать простой скрипт на любом языке программирования который будет работать в режиме демона
	
	mydemon.sh

установить дистрибутив Debian 8 и написать sysvnit скрипт для запуска процесса, добавить в автозагрузку, проверить автозагрузку и работу start stop аргументов

 [daemon](script.sh)
	update-rc.d daemon.sh start
	
	service daemon status
	
	![linux_console](https://i.imgur.com/6YN262n.png)

	service daemon start
	
	![linux_console](https://i.imgur.com/6GZpyiK.png)

Установить Debian 10, написать systemd unit, ш в автозагрузку, проверить что скрипт запускается после рестарта, проверить start stop status unit-а

![linux](https://i.imgur.com/vtw2r1C.png)

написать timer для systemd который раз в 5 минут пишет что-либо в лог файл


Создаем файл /etc/systemd/system/mytimer.timer
![linux](https://i.imgur.com/bqqicPQ.png)
Создаем файл /etc/systemd/system/mytimer.service:
![linux](https://i.imgur.com/ft3Vz2a.png)