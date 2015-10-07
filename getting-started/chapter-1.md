## Getting up and running
## Preparando a Instalação
Nesse capítulo você começará com o básico, incluindo a instalação do CLI NativeScript, começando um novo projeto e por seu primeiro app pra rodar.

In this chapter you're going to start with the basics, including installing the NativeScript CLI, starting a new project, and getting your first app up and running.

### Instale NativeScript e configure seu ambiente de produção
### Install NativeScript and configure your environment

O CLI NativeScript tem alguns requisitos de sistema que você precisa ajustar antes de construir apps com NativeScript. Como primeiro passo, siga as instruções para o seu sistema operacional:

The NativeScript CLI has a few system requirements you must have in place before building NativeScript apps. As a first step, start by going through the instructions for your operating system:

- [Windows](/setup/ns-cli-setup/ns-setup-win.html)
- [OS X](/setup/ns-cli-setup/ns-setup-os-x.html)
- [Linux](/setup/ns-cli-setup/ns-setup-linux.html)

> **TIP**: If you're a bit overwhelmed by these requirements, or if you're looking for a way to build iOS apps on Windows, you might be interested in [using NativeScript with Telerik AppBuilder](/setup/quick-setup.md#the-appbuilder-tool-set). Telerik AppBuilder provides tooling for NativeScript apps, including the ability to perform iOS and Android builds in the cloud, which removes the need to complete these system requirements.

> **DICA**: Se você estiver um pouco preocupado com esses requisitos, ou quiser desenvolver apps iOS no Windows, você poderá se interessar em [usar o AppBuilder NativeScript da Telerik](/setup/quick-setup.md#the-appbuilder-tool-set).
O Telerik AppBuilder provê ferramentas pra aplicativos NativeScript, incluindo o recurso de criar apps iOS e Android na nuvem, o que elimina a necessidade de completar esses requisitos de sistema.

After completing the setup you should have two commands available from your terminal: `tns`—which is short for <b>T</b>elerik <b>N</b>ative<b>S</b>cript—and `nativescript`. The two commands are equivalent, so we'll stick with the shorter `tns`.

Após completar o setup você deve ter poder rodar dois comandos na linha de comando: `tns`-uma sigla para <b>T</b>elerik <b>N</b>ative<b>S</b>cript-e `nativescript`. Os dois comandos são equivalentes, por isso usaremos a versão mais curta: `tns`.

You can verify the installation was successful by running `tns` in your terminal. You should see something like this:
Você pode verificar se a instalação deu certo rodando `tns` na linha de comando. Você deve ver algo como:

```
$ tns
# NativeScript
┌─────────┬─────────────────────────────────────────────────────────────────────┐
│ Usage   │ Synopsis                                                            │
│ General │ $ tns <Command> [Command Parameters] [--command <Options>]          │
│ Alias   │ $ nativescript <Command> [Command Parameters] [--command <Options>] │
└─────────┴─────────────────────────────────────────────────────────────────────┘
```

### Start your app
### Comece a desenvolver seu app

With the NativeScript CLI installed, it's time to start building your app. Normally, you would [use the `tns create` command to create an empty NativeScript application](https://github.com/NativeScript/NativeScript-cli#create-project). For this guide, we've scaffolded out a boilerplate project to act as a starting point for [Groceries](https://github.com/NativeScript/sample-Groceries).

Com o NativeScript CLI instalado, é hora de começar a desenvolver seu app. Normalmente, você [usa o comando `tns create` para criar uma aplicação vazia](https://github.com/NativeScript/NativeScript-cli#create-project).

<h4 class="exercise-start">
    <b>Exercise</b>: Get the Groceries starting point
</h4>

<h4 class="exercise-start">
    <b>Exercício</b>: Vá até o ponto de partida do app Groceries
</h4>

Navigate to a folder where you want to keep your app code:
Navegue até a pasta onde você quer manter seu código:

<div class="no-copy-button"></div>

```
cd the-folder-you-want-groceries-to-be-in
```

```
cd nome-da-pasta-que-guardará-os-arquvivos-do-app
```

Next, assuming you have [git installed](http://www.git-scm.com/), clone the Groceries repo from GitHub:
Depois, assumindo que você tenha o [git installado](http://www.git-scm.com/), clone o repositório do app Groceries do GitHub.

```
git clone https://github.com/NativeScript/sample-Groceries.git
```

After that, change to the newly cloned repo's folder:
Depois disso, altere a pasta do repositório recém-criado. 

```
cd sample-Groceries
```

The master branch has the final state of the Groceries app. Feel free to [refer back to it](https://github.com/NativeScript/sample-Groceries) at any time, but for now, switch over to the “start” branch for this guide's starting point:

O branch master tem o estado final do app Grocieries. Sinta-se livre para [trabalhar nele](https://github.com/NativeScript/sample-Groceries) a qualquer momento, mas, por enquanto, mude para o branch "start" iniciar no objetivo deste guia.

```
git checkout start
```

<div class="exercise-end"></div>

### Add target development platforms
### Adicione as plataformas alvo

Your app is now set up, but before you run it, you need to initialize a platform-specific native project for each platform you intend to target.

Seu app já está configurado, mas antes de executá-lo, você precisa inicializar um projeto nativo específico para cada plataforma alvo.

<h4 class="exercise-start">
    <b>Exercise</b>: Add the iOS and Android platforms
</h4>

<h4 class="exercise-start">
    <b>Exercício</b>: Adicione a plataforma iOS e Android.
</h4>

If you're on a Mac, start by adding the iOS platform:
Se você estiver num Mac, comece adicionando a plataforma iOS:

```
tns platform add ios
```

Next, add the Android platform with the same `platform add` command:
Depois, adicone a plataforma Android com o mesmo comando `platform add`:

```
tns platform add android
```

<div class="exercise-end"></div>

>**IMPORTANT:** You can add platforms only for SDKs that you already have installed on your development machine. If you get errors running `tns platform add`, refer back to the section on [setting up your development environment](#install-nativescript-and-configure-your-environment).

>**IMPORTANTE:** Você pode adicionar apenas plataformas para as quais você já instalou o SDK em sua máquina de desenvolvimento. Se você receber erros ao rodar `tns platform add`, consulte a seção [configurando sua máquina de ssenvolvimento](#install-nativescript-and-configure-your-environment).

The `platform add` command adds a folder called `platforms` to your project, and copies all of the required native SDKs into this folder. When you build the application, the NativeScript CLI will copy your application code into the `platforms` folder so that a native binary can be created.

O comando `platform add` adiciona uma pasta chamada `platforms` ao seu projeto, e copia para ela todos os arquivos dos SDKs nativos necessários. Quando você faz um <i>build</i> (uma espécie de compilação) o CLI NativeScript copia todo o código de seu app para a pasta `platforms`, assim um arquivo binário nativo pode ser criado. 

### Running your app
### Executando seu app

With the platform initialization complete, you can run your app in an emulator or on devices.
Com a inicialização de plataforma completa, você pode rodar seu app em um emulador ou nos dispositivos.

<h4 class="exercise-start">
    <b>Exercício</b>: Execute seu app
</h4>

If you're on a Mac, start by running the app in an iOS simulator with the following command:
Se estiver num Mac, comece rodando o app num simulador de iOS com o seguinte comando:

```
tns run ios --emulator
```

If all went well, you should see something like this:
Se tudo correr bem, você deve ver algo como:

![iOS login](img/cli-getting-started/chapter1/ios/1.png)

Next, run your app on an Android emulator with the following command:
Depois, rode seu app num emulador de Android com o seguinte comando:

```
tns run android --emulator
```

> **WARNING**:
> * You must have at least one Android AVD (Android Virtual Device) configured for this command to work. If you get an error, try [setting up an AVD](https://www.genymotion.com/#!/) and then run the command again.
> * If you're using Genymotion, launch your Genymotion virtual device, and then run `tns run android`.

>**ATENÇÃO**:
> * Você precisa ter ao menos um Android AVD (Android Virtual Device) configurado pra esse comando funcionar. Se você obter um erro, consulte [configurando um AVD](https://www.genymotion.com/#!/) e rode o comando de novo.
> * Se você estiver usando Genymotion, abra seu dispositivo virtual e então execute `tns run android`.

If all went well, you should see your app running in an Android emulator:
Se tudo correu bem, você deve ver seu app rodando num emulador de Android.

![Android login](img/cli-getting-started/chapter1/android/1.png)

<div class="exercise-end"></div>

Here are a few other tips for running NativeScript apps.
Aqui algumas outras dicas para executar apps NativeScript.

> **TIP**:
> * To run on a USB-connected Android or iOS device, use the same `run` command without the `--emulator` flag—i.e. `tns run android` and `tns run ios`.
> * The `tns device` command lists all USB-connected iOS devices, USB-connected Android devices, and Genymotion virtual devices that `tns run` can deploy to. Note that `tns device` does not list iOS simulators.

> **DICA**:
> * Para executar num Android ou iOS conectados via USB, use o mesmo comando `run` sem a flag `--emulator`- Por exemplo: `tns run android` e `tns run ios`.
> * O comando `tns device` lista todos os dispositivos (iOS e Android) conectados via USB e dispositivos virtuais Genymotion com os quais `tns run` está habilitado pra trabalhar. Note que `tns device` não lista simuladores de iOS.

### Development workflow
### Fluxo de Trabalho

At this point, you have the NativeScript CLI downloaded and installed, as well as the iOS and Android dependencies that you need to run your app. Now you need a good workflow that lets you make changes and see results fast.

Até aqui, você já tem o CLI NativeScript baixado e instalado, bem como as dependências do Android e iOS que você precisa pra rodar seu app. Agora você precisa de um bom fluxo de trabalho que lhe permita fazer alterações e ver os resultados rapidamente.

A good way to see your changes is to execute `tns run ios` or `tns run android` after you save files. To see this action, let's make a trivial update to your app.

Um bom jeito de ver suas mudanãs é executar `tns run ios` ou `tns run android` depois de salvar os arquivos. Pra ver isso em ação, vamos fazer uma atualização trivial em seu app.

<h4 class="exercise-start">
    <b>Exercício</b>: Sua primeira alteração num app NativeScript
</h4>

If your previous `tns run ios` or `tns run android` task is still running, type `Ctrl+C` in your terminal to kill it.
Se o comando `tns run ios` ou `tns run android` ainda estão rodando, digite `Ctrl+C` na linha de comando para finalizá-los.

Open your app's `app/views/login/login.xml` file in your text editor of choice and change `<Label text="hello world" />` to `<Label text="hello NativeScript" />`.

Abra o arquivo `app/views/login/login.xml` num editor de texto de sua escolha e altere `<Label text="hello world" />` para `<Label text="hello NativeScript" />`.

Return to your terminal and run either `tns run ios --emulator` (if you're on a Mac), or `tns run android --emulator`. You should see the app relaunch and the updated text displayed.

Retorne ao console e execute `tns run ios --emulator` (Se estiver num Mac), ou `tns run android --emulator`. Você deve ver o app reabrir e a mudança no texto ser exibida. 

<div class="exercise-end"></div>

As you might have noticed, the `tns run` command blocks your terminal while your app is running (it's the task you had to use `Ctrl` + `C` to kill). The task shows both the output of `console.log()` statements as your app executes, as well as stack traces when things go wrong. So if your app crashes at any time during this guide, look to the terminal for a detailed report of the problem.

Como talvez tenha notado, o comando `tns run` bloqueia o console enquanto seu app está executando (é pra isso que você deve usar `Ctrl` + `C` pra finalizar). A tarefa mostra a saída do comando `console.log()` à medida que seu app executa, e também log de erros quando as coisas dão errado. Assim, se seu app travar durante esse tutorial, veja no console a descrição detalhada do problema. 

The iOS and Android logs can be a bit noisy, so you might have to scroll up a bit to find the actual problem. For example if I try to call `foo.bar()` when `foo` does not exist, here's the information I get on iOS:

Os logs do iOS e Andoroid podem ser meio esquisitos, por isso você talvez precise navegar pelo log pra encontrar o problema real. Por exemplo, se tentar chamar o método `foo.bar()` sendo que `foo` não existe, aqui está a informação obtida no iOS:

```
/app/path/to/file.js:14:8: JS ERROR ReferenceError: Can't find variable: foo
1   0xe3dc0 NativeScript::FFICallback<NativeScript::ObjCMethodCallback>::ffiClosureCallback(ffi_cif*, void*, void**, void*)
```

And here's the same information in the Android logs:
E aqui a mesma informação nos logs do Android:

```
E/TNS.Native( 2063): ReferenceError: foo is not defined
E/TNS.Native( 2063): File: "/data/data/org.nativescript.groceries/files/app/./views/login/login.js, line: 13, column: 4
```

> **TIP**: When you're trying to debug a problem, you can also try adding `console.log()` statements in your JavaScript code—exactly as you would in a browser-based application.

> **DICA**: Quando estiver tentando debugar um problema, você pode também chamar o método  `console.log()` em seu código JavaScript - Exatamente como faria se estivesse numa aplicativo baseado em navegador.

If you find continuously running `tns run` from the terminal to be tedious, you may be interested in trying one of the following workflows:

Se você achar tedioso executar `tns run` no console muitas vezes, você pode se interessar por um dos seguintes fluxos de trabalho:


* The `tns livesync` command instantly transfers XML, CSS, and JavaScript files to a running NativeScript app. If you set the command's `--watch` flag (`tns livesync ios --emulator --watch` or `tns livesync android --emulator --watch`), the NativeScript CLI will watch your app for changes, and apply those changes automatically after you save files. Be warned, however, that the `livesync` command currently does not show `console.log()` output or stack traces. So during debugging you may want to switch back to `tns run`.
* For Sublime Text users, [this build script](http://developer.telerik.com/featured/a-nativescript-development-workflow-for-sublime-text/) lets you type `Cmd`/`Ctrl` + `B` to start a build without returning to the terminal.
* Emil Öberg's [nativescript-emulator-reload npm module](https://github.com/emiloberg/nativescript-emulator-reload) adds a Gulp watcher that relaunches the emulator after every change you make.

* O comando `tns livesync` transfere instantanemante arquivos XML, CSS e JavaScript para um app NativeScript que esteja rodando. Se você usar o modificador `--watch` (`tns livesync ios --emulator --watch` ou `tns livesync android --emulator --watch`), o CLI NativeScript observará as mudanças em seu app e irá aplicá-las automaticamente depois de você salvar os aqruivos. Saiba, no entanto, que o comando `livesync` atualmente não exibe a saída de `console.log()` ou as descrições de erro detalhadas. Assim, durante o debug, você talvez queira voltar a usar `tns run`.
* Pra usuários do Sublime Text [esse script](http://developer.telerik.com/featured/a-nativescript-development-workflow-for-sublime-text/) lhe permite digitar `Cmd`/`Ctrl` + `B` para iniciar o build sem usar o console.
*[o módulo npm nativescript-emulator-reload](https://github.com/emiloberg/nativescript-emulator-reload) de  Emil Öberg adiciona um observador Gulp que re-executa o emulador após cada alteração feita.

Now that you've created an app, configured your environment, and set up your app to run on iOS and Android, you're ready to start digging into the files that make up a NativeScript app.

Agora que você criou um app, configurou seu ambiente de produção, e pôs seu app pra rodar no iOS e Android, você está pronto pra ir mais a fundo nos arquivos que compõem um app NativeScript.  
