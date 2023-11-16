# Домашнее задание к занятию «Инструменты Git»

### Цель задания

В результате выполнения задания вы:

* научитесь работать с утилитами Git;
* потренируетесь решать типовые задачи, возникающие при работе в команде. 

### Инструкция к заданию

1. Склонируйте [репозиторий](https://github.com/hashicorp/terraform) с исходным кодом Terraform.
2. Создайте файл для ответов на задания в своём репозитории, после выполнения прикрепите ссылку на .md-файл с ответами в личном кабинете.
3. Любые вопросы по решению задач задавайте в чате учебной группы.

------

## Задание

В клонированном репозитории:

1. Найдите полный хеш и комментарий коммита, хеш которого начинается на `aefea`.
2. Ответьте на вопросы.

* Какому тегу соответствует коммит `85024d3`?
* Сколько родителей у коммита `b8d720`? Напишите их хеши.
* Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами  v0.12.23 и v0.12.24.
* Найдите коммит, в котором была создана функция `func providerSource`, её определение в коде выглядит так: `func providerSource(...)` (вместо троеточия перечислены аргументы).
* Найдите все коммиты, в которых была изменена функция `globalPluginDirs`.
* Кто автор функции `synchronizedWriters`? 

*В качестве решения ответьте на вопросы и опишите, как были получены эти ответы.*

## ОТВЕТЫ
1. Найдите полный хеш и комментарий коммита, хеш которого начинается на `aefea`.
   
   goddim@Ubuntu:~/terraform$ git log --oneline | grep -i aefea
aefead2207 Update CHANGELOG.md
---------------
* Какому тегу соответствует коммит `85024d3`?
  
  goddim@Ubuntu:~/terraform$ git describe --tags 85024d3
v0.12.23
------------------
* Сколько родителей у коммита `b8d720`? Напишите их хеши.
* 
goddim@Ubuntu:~/terraform$ git log --pretty=%P -n 1 b8d720

56cd7859e05c36c06b56d013b55a252d0bb7e158 9ea88f22fc6269854151c571162c5bcf958bee2b

Хеш первого родителя: 56cd7859e05c36c06b56d013b55a252d0bb7e158
Хеш второго родителя: 9ea88f22fc6269854151c571162c5bcf958bee2b
-----------------------------------------------------------------
* Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами  v0.12.23 и v0.12.24.
* 
  goddim@Ubuntu:~/terraform$ git log --oneline v0.12.23..v0.12.24

33ff1c03bb (tag: v0.12.24) v0.12.24

b14b74c493 [Website] vmc provider links

3f235065b9 Update CHANGELOG.md

6ae64e247b registry: Fix panic when server is unreachable

5c619ca1ba website: Remove links to the getting started guide's old location

06275647e2 Update CHANGELOG.md

d5f9411f51 command: Fix bug when using terraform login on Windows

4b6d06cc5d Update CHANGELOG.md

dd01a35078 Update CHANGELOG.md

225466bc3e Cleanup after v0.12.23 release
-----------------------------------------------
* Найдите коммит, в котором была создана функция `func providerSource`, её определение в коде выглядит так: `func providerSource(...)` (вместо троеточия перечислены аргументы).
  
  goddim@Ubuntu:~/terraform$ git log -S'func providerSource(' --oneline

8c928e8358 main: Consult local directories as potential mirrors of providers
--------------------------------------------------------
Найдите все коммиты, в которых была изменена функция `globalPluginDirs`.

ищем файл с функцией во всем репозитории:

goddim@Ubuntu:~/terraform$ git grep -n 'func globalPluginDirs('

plugins.go:21:func globalPluginDirs() []string {

теперь ищем иземенения в найденом файле:

goddim@Ubuntu:~/terraform$ git log --oneline -L :globalPluginDirs:plugins.go

78b1220558 Remove config.go and update things using its aliases



diff --git a/plugins.go b/plugins.go

--- a/plugins.go

+++ b/plugins.go

@@ -16,14 +18,14 @@

 func globalPluginDirs() []string {

        var ret []string

        // Look in ~/.terraform.d/plugins/ , or its equivalent on non-UNIX

-       dir, err := ConfigDir()

+       dir, err := cliconfig.ConfigDir()

        if err != nil {

                log.Printf("[ERROR] Error finding global config directory: %s", err)

        } else {

                machineDir := fmt.Sprintf("%s_%s", runtime.GOOS, runtime.GOARCH)

                ret = append(ret, filepath.Join(dir, "plugins"))

                ret = append(ret, filepath.Join(dir, "plugins", machineDir))

        }

 

        return ret

 }

52dbf94834 keep .terraform.d/plugins for discovery



diff --git a/plugins.go b/plugins.go

--- a/plugins.go

+++ b/plugins.go

@@ -16,13 +16,14 @@

 func globalPluginDirs() []string {

        var ret []string

        // Look in ~/.terraform.d/plugins/ , or its equivalent on non-UNIX

        dir, err := ConfigDir()

        if err != nil {

                log.Printf("[ERROR] Error finding global config directory: %s", err)

        } else {

                machineDir := fmt.Sprintf("%s_%s", runtime.GOOS, runtime.GOARCH)

+               ret = append(ret, filepath.Join(dir, "plugins"))

                ret = append(ret, filepath.Join(dir, "plugins", machineDir))

        }

 

        return ret

 }

41ab0aef7a Add missing OS_ARCH dir to global plugin paths



diff --git a/plugins.go b/plugins.go

--- a/plugins.go

+++ b/plugins.go

@@ -14,12 +16,13 @@

:



78b1220558 Remove config.go and update things using its aliases



diff --git a/plugins.go b/plugins.go

--- a/plugins.go

+++ b/plugins.go

@@ -16,14 +18,14 @@

 func globalPluginDirs() []string {

        var ret []string

        // Look in ~/.terraform.d/plugins/ , or its equivalent on non-UNIX

-       dir, err := ConfigDir()

+       dir, err := cliconfig.ConfigDir()

        if err != nil {

                log.Printf("[ERROR] Error finding global config directory: %s", err)

        } else {

                machineDir := fmt.Sprintf("%s_%s", runtime.GOOS, runtime.GOARCH)

                ret = append(ret, filepath.Join(dir, "plugins"))

                ret = append(ret, filepath.Join(dir, "plugins", machineDir))

        }

 

        return ret

 }

52dbf94834 keep .terraform.d/plugins for discovery



diff --git a/plugins.go b/plugins.go

--- a/plugins.go

+++ b/plugins.go

@@ -16,13 +16,14 @@

 func globalPluginDirs() []string {

        var ret []string

        // Look in ~/.terraform.d/plugins/ , or its equivalent on non-UNIX

        dir, err := ConfigDir()

        if err != nil {

                log.Printf("[ERROR] Error finding global config directory: %s", err)

        } else {

                machineDir := fmt.Sprintf("%s_%s", runtime.GOOS, runtime.GOARCH)

+               ret = append(ret, filepath.Join(dir, "plugins"))

                ret = append(ret, filepath.Join(dir, "plugins", machineDir))

        }

 

        return ret

 }

41ab0aef7a Add missing OS_ARCH dir to global plugin paths



diff --git a/plugins.go b/plugins.go

--- a/plugins.go

+++ b/plugins.go

@@ -14,12 +16,13 @@

:






78b1220558 Remove config.go and update things using its aliases



diff --git a/plugins.go b/plugins.go

--- a/plugins.go

+++ b/plugins.go

@@ -16,14 +18,14 @@

 func globalPluginDirs() []string {

        var ret []string

        // Look in ~/.terraform.d/plugins/ , or its equivalent on non-UNIX

-       dir, err := ConfigDir()

+       dir, err := cliconfig.ConfigDir()

        if err != nil {

                log.Printf("[ERROR] Error finding global config directory: %s", err)

        } else {

                machineDir := fmt.Sprintf("%s_%s", runtime.GOOS, runtime.GOARCH)

                ret = append(ret, filepath.Join(dir, "plugins"))

                ret = append(ret, filepath.Join(dir, "plugins", machineDir))

        }

 

        return ret

 }

52dbf94834 keep .terraform.d/plugins for discovery



diff --git a/plugins.go b/plugins.go

--- a/plugins.go

+++ b/plugins.go

@@ -16,13 +16,14 @@

 func globalPluginDirs() []string {

        var ret []string

        // Look in ~/.terraform.d/plugins/ , or its equivalent on non-UNIX

        dir, err := ConfigDir()

        if err != nil {

                log.Printf("[ERROR] Error finding global config directory: %s", err)

        } else {

                machineDir := fmt.Sprintf("%s_%s", runtime.GOOS, runtime.GOARCH)

+               ret = append(ret, filepath.Join(dir, "plugins"))

                ret = append(ret, filepath.Join(dir, "plugins", machineDir))

        }

 

        return ret

 }

41ab0aef7a Add missing OS_ARCH dir to global plugin paths



diff --git a/plugins.go b/plugins.go

--- a/plugins.go

+++ b/plugins.go

@@ -14,12 +16,13 @@

 func globalPluginDirs() []string {

        var ret []string

        // Look in ~/.terraform.d/plugins/ , or its equivalent on non-UNIX

        dir, err := ConfigDir()

        if err != nil {

                log.Printf("[ERROR] Error finding global config directory: %s", err)

        } else {

-               ret = append(ret, filepath.Join(dir, "plugins"))

+               machineDir := fmt.Sprintf("%s_%s", runtime.GOOS, runtime.GOARCH)

+               ret = append(ret, filepath.Join(dir, "plugins", machineDir))

        }

 

        return ret

 }

66ebff90cd move some more plugin search path logic to command



diff --git a/plugins.go b/plugins.go

--- a/plugins.go

+++ b/plugins.go

@@ -16,22 +14,12 @@

 func globalPluginDirs() []string {

        var ret []string

-

-       // Look in the same directory as the Terraform executable.

-       // If found, this replaces what we found in the config path.

-       exePath, err := osext.Executable()

-       if err != nil {

-               log.Printf("[ERROR] Error discovering exe directory: %s", err)

-       } else {

-               ret = append(ret, filepath.Dir(exePath))

-       }

-

        // Look in ~/.terraform.d/plugins/ , or its equivalent on non-UNIX

        dir, err := ConfigDir()

        if err != nil {

                log.Printf("[ERROR] Error finding global config directory: %s", err)

        } else {

                ret = append(ret, filepath.Join(dir, "plugins"))

        }

 

        return ret

 }

8364383c35 Push plugin discovery down into command package



diff --git a/plugins.go b/plugins.go

--- /dev/null

+++ b/plugins.go

@@ -0,0 +16,22 @@

+func globalPluginDirs() []string {

+       var ret []string

+

+       // Look in the same directory as the Terraform executable.

+       // If found, this replaces what we found in the config path.

+       exePath, err := osext.Executable()

+       if err != nil {

+               log.Printf("[ERROR] Error discovering exe directory: %s", err)

+       } else {

+               ret = append(ret, filepath.Dir(exePath))

+       }

+

+       // Look in ~/.terraform.d/plugins/ , or its equivalent on non-UNIX

+       dir, err := ConfigDir()

+       if err != nil {

+               log.Printf("[ERROR] Error finding global config directory: %s", err)

+       } else {

+               ret = append(ret, filepath.Join(dir, "plugins"))

+       }

+

+       return ret

+}

(END)




![image](https://github.com/goddim/HW_netology_main/assets/132663924/a6cf9789-7166-4570-8804-cf0410cb7e67)
