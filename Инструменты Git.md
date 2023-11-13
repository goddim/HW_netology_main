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

goddim@Ubuntu:~/terraform$ git log -p -S'globalPluginDirs'

commit 65c4ba736375607b6af6c035972f7f151232b6c6

Author: Valeriy Pastushenko <i@combin.name>

Date:   Sat May 21 19:53:24 2022 +0300



    Remove terraform binary



diff --git a/terraform b/terraform

deleted file mode 100644

index d22a47ad86..0000000000

Binary files a/terraform and /dev/null differ



commit 125eb51dc40b049b38bf2ed11c32c6f594c8ef96

Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>

Date:   Thu May 5 10:12:00 2022 -0400



    Remove accidentally-committed binary

    

    Also add this path to .gitignore to prevent future mistakes.



diff --git a/terraform b/terraform

deleted file mode 100755

index 4453f47bf1..0000000000

Binary files a/terraform and /dev/null differ

:...skipping...

commit 65c4ba736375607b6af6c035972f7f151232b6c6

Author: Valeriy Pastushenko <i@combin.name>

Date:   Sat May 21 19:53:24 2022 +0300



    Remove terraform binary



diff --git a/terraform b/terraform

deleted file mode 100644

index d22a47ad86..0000000000

Binary files a/terraform and /dev/null differ



commit 125eb51dc40b049b38bf2ed11c32c6f594c8ef96

Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>

Date:   Thu May 5 10:12:00 2022 -0400



    Remove accidentally-committed binary

    

    Also add this path to .gitignore to prevent future mistakes.



diff --git a/terraform b/terraform

deleted file mode 100755

index 4453f47bf1..0000000000

Binary files a/terraform and /dev/null differ



commit 22c121df8631c4499d070329c9aa7f5b291494e1

Author: Anna Winkler <3526523+annawinkler@users.noreply.github.com>

Date:   Tue May 3 12:28:41 2022 -0600



    Bump compatibility version to 1.3.0 for terraform core release (#30988)

    

    * Bump compatibility version to 1.3.0 for terraform core release

    

    Co-authored-by: Brandon Croft <brandon.croft@gmail.com>



diff --git a/terraform b/terraform

new file mode 100755

index 0000000000..4453f47bf1

Binary files /dev/null and b/terraform differ



commit 7c7e5d8f0a6a50812e6e4db3016ebfd36fa5eaef

Author: Valeriy Pastushenko <i@combin.name>

Date:   Fri Sep 3 18:33:10 2021 +0300



    Don't show data while input if sensitive



diff --git a/terraform b/terraform

new file mode 100644

index 0000000000..d22a47ad86

Binary files /dev/null and b/terraform differ

~

:


commit 65c4ba736375607b6af6c035972f7f151232b6c6

Author: Valeriy Pastushenko <i@combin.name>

Date:   Sat May 21 19:53:24 2022 +0300



    Remove terraform binary



diff --git a/terraform b/terraform

deleted file mode 100644

index d22a47ad86..0000000000

Binary files a/terraform and /dev/null differ



commit 125eb51dc40b049b38bf2ed11c32c6f594c8ef96

Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>

Date:   Thu May 5 10:12:00 2022 -0400



    Remove accidentally-committed binary

    

    Also add this path to .gitignore to prevent future mistakes.



diff --git a/terraform b/terraform

deleted file mode 100755

index 4453f47bf1..0000000000

Binary files a/terraform and /dev/null differ



commit 22c121df8631c4499d070329c9aa7f5b291494e1

Author: Anna Winkler <3526523+annawinkler@users.noreply.github.com>

Date:   Tue May 3 12:28:41 2022 -0600



    Bump compatibility version to 1.3.0 for terraform core release (#30988)

    

    * Bump compatibility version to 1.3.0 for terraform core release

    

    Co-authored-by: Brandon Croft <brandon.croft@gmail.com>



diff --git a/terraform b/terraform

new file mode 100755

index 0000000000..4453f47bf1

Binary files /dev/null and b/terraform differ



commit 7c7e5d8f0a6a50812e6e4db3016ebfd36fa5eaef

Author: Valeriy Pastushenko <i@combin.name>

Date:   Fri Sep 3 18:33:10 2021 +0300



    Don't show data while input if sensitive



diff --git a/terraform b/terraform

new file mode 100644

index 0000000000..d22a47ad86

Binary files /dev/null and b/terraform differ



commit 35a058fb3ddfae9cfee0b3893822c9a95b920f4c

Author: Martin Atkins <mart@degeneration.co.uk>

Date:   Thu Oct 19 17:40:20 2017 -0700



    main: configure credentials from the CLI config file



diff --git a/commands.go b/commands.go

index b3380884de..39e30220df 100644

--- a/commands.go

+++ b/commands.go

@@ -4,10 +4,11 @@ import (

        "os"

        "os/signal"

 

+       "github.com/hashicorp/terraform/command"

+       pluginDiscovery "github.com/hashicorp/terraform/plugin/discovery"

+       "github.com/hashicorp/terraform/svchost"

        "github.com/hashicorp/terraform/svchost/auth"

        "github.com/hashicorp/terraform/svchost/disco"

-

-       "github.com/hashicorp/terraform/command"

        "github.com/mitchellh/cli"

 )

 

@@ -34,7 +35,7 @@ func initCommands(config *Config) {

                inAutomation = true

        }

 

-       credsSrc := auth.NoCredentials // TODO: Actually expose credentials here

+       credsSrc := credentialsSource(config)

        services := disco.NewDisco()

        services.SetCredentialsSource(credsSrc)

 

@@ -342,3 +343,43 @@ func makeShutdownCh() <-chan struct{} {

 

        return resultCh

 }

+

+func credentialsSource(config *Config) auth.CredentialsSource {

+       creds := auth.NoCredentials

+       if len(config.Credentials) > 0 {

+               staticTable := map[svchost.Hostname]map[string]interface{}{}

+               for userHost, creds := range config.Credentials {

+                       host, err := svchost.ForComparison(userHost)

+                       if err != nil {

+                               // We expect the config was already validated by the time we get

+                               // here, so we'll just ignore invalid hostnames.

+                               continue

+                       }

+                       staticTable[host] = creds

+               }

+               creds = auth.StaticCredentialsSource(staticTable)

+       }

+

+       for helperType, helperConfig := range config.CredentialsHelpers {

+               available := pluginDiscovery.FindPlugins("credentials", globalPluginDirs())

+               available = available.WithName(helperType)

+               if available.Count() == 0 {

+                       break

+               }

+

+               selected := available.Newest()

+

+               helperSource := auth.HelperProgramCredentialsSource(selected.Path, helperConfig.Args...)

+               creds = auth.Credentials{

+                       creds,

+                       auth.CachingCredentialsSource(helperSource), // cached because external operation may be slow/expensive

+               }

+

+               // There should only be zero or one "credentials_helper" blocks. We

+               // assume that the config was validated earlier and so we don't check

+               // for extras here.

+               break

+       }

+

+       return creds

+}



commit c0b17610965450a89598da491ce9b6b5cbd6393f

Author: James Bardin <j.bardin@gmail.com>

Date:   Mon Jun 12 15:04:40 2017 -0400



    prevent log output during init

    

    The extra output shouldn't be seen by the user, and is causing TFE to

    fail.



diff --git a/config_unix.go b/config_unix.go

index 4694d5114d..d28d749248 100644

--- a/config_unix.go

+++ b/config_unix.go

@@ -5,7 +5,6 @@ package main

 import (

        "bytes"

        "errors"

-       "log"

        "os"

        "os/exec"

        "path/filepath"

@@ -33,7 +32,12 @@ func configDir() (string, error) {

 func homeDir() (string, error) {

        // First prefer the HOME environmental variable

        if home := os.Getenv("HOME"); home != "" {

-               log.Printf("[DEBUG] Detected home directory from env var: %s", home)

+

+               // FIXME: homeDir gets called from globalPluginDirs during init, before

+               // the logging is setup.  We should move meta initializtion outside of

+               // init, but in the meantime we just need to silence this output.

+               //log.Printf("[DEBUG] Detected home directory from env var: %s", home)

+

                return home, nil

        }

 



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



diff --git a/commands.go b/commands.go

index 409f4d85df..c4dca2d670 100644

--- a/commands.go

+++ b/commands.go

@@ -30,9 +30,10 @@ func init() {

        }

 

        meta := command.Meta{

-               Color:       true,

-               ContextOpts: &ContextOpts,

-               Ui:          Ui,

+               Color:            true,

+               GlobalPluginDirs: globalPluginDirs(),

+               PluginOverrides:  &PluginOverrides,

+               Ui:               Ui,

        }

 

        // The command list is included in the terraform -help

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
