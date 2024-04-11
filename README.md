# Базовый boilerplate sveltekit + tailwind + vscode + devcontainer
Boilerplate больше ориентируется на настройку связки стандартных вещей. Создан исключительно для того чтобы не тратить время на "глупую" первоначальную настройку.

## Установлено
- [sveltekit](https://kit.svelte.dev/)
- [tailwindcss](https://tailwindcss.com/)
- [theme-change](https://www.npmjs.com/package/theme-change)
- [prettier](https://prettier.io/)
- [prettier-plugin-tailwindcss](https://github.com/tailwindlabs/prettier-plugin-tailwindcss)

## Зачем и почему?
Я привык использовать svelte и tailwind в связи с тем что я начал изучать tailwind очень давно хотя и не выучил полностью. Поэтому sveltekit и tailwindcss ставятся по умолчанию.

theme-change нужен для быстрой настройки переключения темы (обратите внимание на изменения в файлах [app.html](./src/app.html) и [+page.svelte](./src/routes/+page.svelte)).

prettier используется вместе с расширением vscode [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode) для автоформатирования (обратите внимание на [settings.json](.vscode/settings.json)) хотя можно и ручками через npm run format.

prettier-plugin-tailwindcss используется для автосортировки стилей при форматировании больше об читайте на странице [настроек редакторов для tailwind](https://tailwindcss.com/docs/editor-setup#automatic-class-sorting-with-prettier).

Ну и разумеется самым главным фактором является запуск проекта почти при полном отсутствии рабочего окружения за исключением vscode и docker благодаря [Development Containers](https://containers.dev/). 

## Установка

### Linux
Устанавливаем [docker](https://docs.docker.com/engine/install/) стандартными средствами или используя средства автоматизации (типа [ansible](https://www.ansible.com/)) по желанию [добавляем себя в группу docker](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user).

По необходимости настраиваем autocomplete для вашего шела. После устанавливаем [vscode допустим из snap](https://snapcraft.io/code) что то вроде:
```bash
sudo snap install code --classic
```

### Windows
Устанавливаем wsl, docker desktop, vscode, а также советую установить [windows terminal](https://apps.microsoft.com/detail/9n0dx20hk701?hl=ru-ru&gl=RU).

Делать всё это я советую через [winget](https://learn.microsoft.com/ru-ru/windows/package-manager/winget/) или другой пакетный менеджер (допустим [chocolatey](https://chocolatey.org/))

```ps
# install winget
wsl --install
winget install Microsoft.VisualStudioCode Microsoft.WindowsTerminal
winget install Docker.DockerDesktop
```

Также при желании добавляем в wsl autocomplete docker для вашего шела.Автокомплиты можете взять с [оффициального репозитория docker/cli](https://github.com/docker/cli/tree/master/contrib/completion)

```bash
#Как пример для баша будет выглядить примерно вот так
curl https://raw.githubusercontent.com/docker/cli/master/contrib/completion/bash/docker -o /etc/bash_completion.d/docker
```

## Запуск, как это работает и зачем столько конфигов

После установки клонируем данный репозиторий и открываем через vscode:
```bash
# cd $projectsdir
git clone --depth 1 https://github.com/shvargon/svapp
cd svapp
code ./
```
Открыв проект в vscode мы увиди предложение установить расширение [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) благодаря [механизму рекомендаций расширений workspace](https://code.visualstudio.com/docs/editor/extension-marketplace#_workspace-recommended-extensions) пример смотрите в файле [extensions.json](.vscode/extensions.json). 
Соглашаемся после чего vscode предложит переоткрыть проект в контейнере соглашаемся.

Далее vscode выкачает docker образ (или запустит compose) указаный в файле [devcontainer.json](.devcontainer/devcontainer.json) в нашем случае это образ для запуска nodejs строчка:
```json
{
    "image": "mcr.microsoft.com/devcontainers/typescript-node:1-20-bookworm"
}
```
И на его основе запустит сборку нового образа в которую будут включены расширения указанные в devcontainer.json в нашем случае это расширения для svelte и tailwind:

```json
{
    "customizations": {
		"vscode": {
			"extensions": ["svelte.svelte-vscode", "bradlc.vscode-tailwindcss"]
		}
	},
}
```

После этого [благодаря конфигурации запуска](https://code.visualstudio.com/docs/editor/debugging#_launch-configurations) мы можем запустить проект с отладкой F5 или без неё (Ctrl+F5). Как пример посмотрите файл [launch.json](.vscode/launch.json). 

Стоит также отметить что [применена конфигурация](https://github.com/tailwindlabs/tailwindcss/discussions/5258
) для исправления ошибки линтера при использовании tailwind.

После чего vscode заметит что у нас запустился сервер и предложит открыть в браузере страницу http://localhost:5173/.

Как итог у нас есть полностью работоспособный контейнер с легким запуском который хранит в себе всё начиная от компилятора | интерпритатора в нашем случае nodejs и заканчивая возможно ненужными ему расширениями для vscode.

И очистка рабочей машины от рабочего окружения необходимого для запуска чужого проекта сводится к удалению контейнера и лишних образов docker.

## Может быть стоит добавить или исправить
- [editorconfig](https://editorconfig.org/)
- пример pipeline gitlab ci/cd
- пример pipeline github action
- Не помню точно но svelte надо конфигурировать под typescript
- Возможно добавить что то похожее для [WebStorm JetBrains IDEs](https://www.jetbrains.com/help/webstorm/connect-to-devcontainer.html)
- добавить [daisyUI](https://daisyui.com/) и [lucide icon](https://lucide.dev/) отдельной веткой