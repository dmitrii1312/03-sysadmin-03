## 1 Какой системный вызов делает команда cd?

	stat("/tmp", {st_mode=S_IFDIR|S_ISVTX|0777, st_size=4096, ...}) = 0
	chdir("/tmp")
	
## 2 Используя strace выясните, где находится база данных file

	/usr/share/misc/magic.mgc
	
## 3 Основываясь на знаниях о перенаправлении потоков предложите способ обнуления открытого удаленного файла (чтобы освободить место на файловой системе).

При помощи gdb подключиться к процессу, закрыть старый файл, и на этом дескрипторе открыть новый.

## 4 Занимают ли зомби-процессы какие-то ресурсы в ОС (CPU, RAM, IO)?

Нет, не занимают. это только дескриптор процесса с необработанным кодом возврата.

## 5 На какие файлы вы увидели вызовы группы open за первую секунду работы утилиты

	sudo opensnoop-bpfcc -d 1
	PID    COMM               FD ERR PATH
	665    irqbalance          6   0 /proc/interrupts
	665    irqbalance          6   0 /proc/stat
	665    irqbalance          6   0 /proc/irq/8/smp_affinity
	665    irqbalance          6   0 /proc/irq/9/smp_affinity

## 6 Какой системный вызов использует uname -a? Приведите цитату из man по этому системному вызову, где описывается альтернативное местоположение в /proc, где можно узнать версию ядра и релиз ОС.

	uname()

Part of the uname information is also accessible via /proc/sys/kernel/{ostype, hostname, osrelease, version, domainname}.

## 7 Чем отличается последовательность команд через ; и через && в bash? Есть ли смысл использовать в bash &&, если применить set -e?

; - следующая команда выполняется не зависимо от результата предыдущей

&& - следующая команда выполняется в случае успешного выполнения предыдущей

set -e настроит поведение при выполнении списка команд ";" так же как с "&&", так что смысла нет

## 8 Из каких опций состоит режим bash set -euxo pipefail и почему его хорошо было бы использовать в сценариях?

	-e  Exit immediately if a command exits with a non-zero status.
	-u  Treat unset variables as an error when substituting.
	-x  Print commands and their arguments as they are executed.
	-o pipefail     the return value of a pipeline is the status of
                  the last command to exit with a non-zero status,
                  or zero if no command exited with a non-zero status

## 9 наиболее часто встречающийся статус у процессов в системе

Наиболее часто встречаются статусы:

I - Idle kernel thread

S - interruptible sleep (waiting for an event to complete)
