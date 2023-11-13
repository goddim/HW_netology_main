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

oddim@Ubuntu:~/terraform$ git log -p plugins.go

commit 53c34ff49cfbc1f70d7cdd3dca8040551c53737a

Author: hashicorp-copywrite[bot] <110428419+hashicorp-copywrite[bot]@users.noreply.github.com>

Date:   Thu Aug 10 23:43:27 2023 +0100



    Update copyright file headers to BUSL-1.1



diff --git a/plugins.go b/plugins.go

index defa9ddd2b..4e7415f676 100644

--- a/plugins.go

+++ b/plugins.go

@@ -1,5 +1,5 @@

 // Copyright (c) HashiCorp, Inc.

-// SPDX-License-Identifier: MPL-2.0

+// SPDX-License-Identifier: BUSL-1.1

 

 package main

 



commit 325d18262e9eeb20546e0d27ef002a14fbc21118

Author: hashicorp-copywrite[bot] <110428419+hashicorp-copywrite[bot]@users.noreply.github.com>

Date:   Tue May 2 15:33:06 2023 +0000



    [COMPLIANCE] Add Copyright and License Headers



diff --git a/plugins.go b/plugins.go

index be576e81ac..defa9ddd2b 100644

--- a/plugins.go

+++ b/plugins.go

@@ -1,3 +1,6 @@

+// Copyright (c) HashiCorp, Inc.

+// SPDX-License-Identifier: MPL-2.0

+

 package main

 

 import (



commit ffe056bacb9f2cf403fa3b6b894c5fbe1fa850a7

Author: Martin Atkins <mart@degeneration.co.uk>

Date:   Mon May 17 12:07:38 2021 -0700



    Move command/ to internal/command/

    

    This is part of a general effort to move all of Terraform's non-library

    package surface under internal in order to reinforce that these are for

    internal use within Terraform only.

    

    If you were previously importing packages under this prefix into an

    external codebase, you could pin to an earlier release tag as an interim

    solution until you've make a plan to achieve the same functionality some

    other way.



diff --git a/plugins.go b/plugins.go

index 47ae2e4f61..be576e81ac 100644

--- a/plugins.go

+++ b/plugins.go

@@ -6,7 +6,7 @@ import (

        "path/filepath"

        "runtime"

 

-       "github.com/hashicorp/terraform/command/cliconfig"

+       "github.com/hashicorp/terraform/internal/command/cliconfig"

 )

 

 // globalPluginDirs returns directories that should be searched for



commit 78b12205587fe839f10d946ea3fdc06719decb05

Author: Pam Selle <204372+pselle@users.noreply.github.com>

Date:   Mon Jan 13 16:50:05 2020 -0500



    Remove config.go and update things using its aliases



diff --git a/plugins.go b/plugins.go

index cf2d542535..47ae2e4f61 100644

--- a/plugins.go

+++ b/plugins.go

@@ -5,6 +5,8 @@ import (

        "log"

        "path/filepath"

        "runtime"

+

+       "github.com/hashicorp/terraform/command/cliconfig"

 )

 

 // globalPluginDirs returns directories that should be searched for

@@ -16,7 +18,7 @@ import (

 func globalPluginDirs() []string {

        var ret []string

        // Look in ~/.terraform.d/plugins/ , or its equivalent on non-UNIX

-       dir, err := ConfigDir()

+       dir, err := cliconfig.ConfigDir()

        if err != nil {

                log.Printf("[ERROR] Error finding global config directory: %s", err)

        } else {



commit 52dbf94834cb970b510f2fba853a5b49ad9b1a46

Author: James Bardin <j.bardin@gmail.com>

Date:   Wed Aug 9 17:46:49 2017 -0400



    keep .terraform.d/plugins for discovery



diff --git a/plugins.go b/plugins.go

index 668c516542..cf2d542535 100644

--- a/plugins.go

+++ b/plugins.go

@@ -21,6 +21,7 @@ func globalPluginDirs() []string {

                log.Printf("[ERROR] Error finding global config directory: %s", err)

        } else {

                machineDir := fmt.Sprintf("%s_%s", runtime.GOOS, runtime.GOARCH)

+               ret = append(ret, filepath.Join(dir, "plugins"))

                ret = append(ret, filepath.Join(dir, "plugins", machineDir))

        }

 



commit 41ab0aef7a0fe030e84018973a64135b11abcd70

Author: James Bardin <j.bardin@gmail.com>

Date:   Wed Aug 9 10:34:11 2017 -0400



    Add missing OS_ARCH dir to global plugin paths

    

    When the global directory was added, the discovery system still

    attempted to search for OS_ARCH subdirectories. It has since been

    changed only search explicit paths.



diff --git a/plugins.go b/plugins.go

index bf23978062..668c516542 100644

--- a/plugins.go

+++ b/plugins.go

@@ -1,8 +1,10 @@

 package main

 

 import (

+       "fmt"

        "log"

        "path/filepath"

+       "runtime"

 )

 

 // globalPluginDirs returns directories that should be searched for

@@ -18,7 +20,8 @@ func globalPluginDirs() []string {

        if err != nil {

                log.Printf("[ERROR] Error finding global config directory: %s", err)

        } else {

-               ret = append(ret, filepath.Join(dir, "plugins"))

+               machineDir := fmt.Sprintf("%s_%s", runtime.GOOS, runtime.GOARCH)

+               ret = append(ret, filepath.Join(dir, "plugins", machineDir))

        }

 

        return ret



commit 66ebff90cdfaa6938f26f908c7ebad8d547fea17

Author: James Bardin <j.bardin@gmail.com>

Date:   Wed May 3 22:24:51 2017 -0400



    move some more plugin search path logic to command

    

    Make less to change when we remove the old search path



diff --git a/plugins.go b/plugins.go

index 9717724a0a..bf23978062 100644

--- a/plugins.go

+++ b/plugins.go

@@ -3,8 +3,6 @@ package main

 import (

        "log"

        "path/filepath"

-

-       "github.com/kardianos/osext"

 )

 

 // globalPluginDirs returns directories that should be searched for

@@ -15,16 +13,6 @@ import (

 // older versions where both satisfy the provider version constraints.

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



commit 8364383c359a6b738a436d1b7745ccdce178df47

Author: Martin Atkins <mart@degeneration.co.uk>

Date:   Thu Apr 13 18:05:58 2017 -0700



    Push plugin discovery down into command package

    

    Previously we did plugin discovery in the main package, but as we move

    towards versioned plugins we need more information available in order to

    resolve plugins, so we move this responsibility into the command package

    itself.

    

    For the moment this is just preserving the existing behavior as long as

    there are only internal and unversioned plugins present. This is the

    final state for provisioners in 0.10, since we don't want to support

    versioned provisioners yet. For providers this is just a checkpoint along

    the way, since further work is required to apply version constraints from

    configuration and support additional plugin search directories.

    

    The automatic plugin discovery behavior is not desirable for tests because

    we want to mock the plugins there, so we add a new backdoor for the tests

    to use to skip the plugin discovery and just provide their own mock

    implementations. Most of this diff is thus noisy rework of the tests to

    use this new mechanism.



diff --git a/plugins.go b/plugins.go

new file mode 100644

index 0000000000..9717724a0a

--- /dev/null

+++ b/plugins.go

@@ -0,0 +1,37 @@

+package main

+

+import (

+       "log"

+       "path/filepath"

+

+       "github.com/kardianos/osext"

+)

+

+// globalPluginDirs returns directories that should be searched for

+// globally-installed plugins (not specific to the current configuration).

+//

+// Earlier entries in this slice get priority over later when multiple copies

+// of the same plugin version are found, but newer versions always override

+// older versions where both satisfy the provider version constraints.

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





----------------------------------
Кто автор функции `synchronizedWriters`? 

goddim@Ubuntu:~/terraform$ git log -S'synchronizedWriters' --pretty="%an <%ae>"

James Bardin <j.bardin@gmail.com>

James Bardin <j.bardin@gmail.com>

Martin Atkins <mart@degeneration.co.uk>

___________________________

![image](https://github.com/goddim/HW_netology_main/assets/132663924/9a88def1-85b4-4df4-9bd0-7d710af4bc1f)


---

### Правила приёма домашнего задания

В личном кабинете отправлена ссылка на .md-файл в вашем репозитории.

### Критерии оценки

Зачёт:

* выполнены все задания;
* ответы даны в развёрнутой форме;
* приложены соответствующие скриншоты и файлы проекта;
* в выполненных заданиях нет противоречий и нарушения логики.

На доработку:

* задание выполнено частично или не выполнено вообще;
* в логике выполнения заданий есть противоречия и существенные недостатки.
