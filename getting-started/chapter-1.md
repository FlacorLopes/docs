## Preparando a Instalação
Nesse capítulo você começará com o básico, incluindo a instalação do CLI NativeScript, como começar  um novo projeto e fazer seu primeiro app executar.

### Instale NativeScript e configure seu ambiente de produção

O CLI NativeScript tem alguns requisitos de sistema que você precisa ajustar antes de construir apps com NativeScript. Como primeiro passo, siga as instruções para o seu sistema operacional:

- [Windows](/setup/ns-cli-setup/ns-setup-win.html)
- [OS X](/setup/ns-cli-setup/ns-setup-os-x.html)
- [Linux](/setup/ns-cli-setup/ns-setup-linux.html)

> **DICA**: Se você estiver um pouco preocupado com esses requisitos, ou quiser desenvolver apps iOS no Windows, você poderá se interessar em [usar o AppBuilder NativeScript da Telerik](/setup/quick-setup.md#the-appbuilder-tool-set).
O Telerik AppBuilder provê ferramentas pra aplicativos NativeScript, incluindo o recurso de criar apps iOS e Android na nuvem, o que elimina a necessidade de satisfazer esses requisitos de sistema.

Após completar o setup você deve ter poder rodar dois comandos no console: `tns`-uma sigla para <b>T</b>elerik <b>N</b>ative<b>S</b>cript-e `nativescript`. Os dois comandos são equivalentes, por isso usaremos a versão mais curta: `tns`.

Você pode verificar se a instalação deu certo rodando `tns` no console. Você deve ver algo como:

```
$ tns
# NativeScript
┌─────────┬─────────────────────────────────────────────────────────────────────┐
│ Usage   │ Synopsis                                                            │
│ General │ $ tns <Command> [Command Parameters] [--command <Options>]          │
│ Alias   │ $ nativescript <Command> [Command Parameters] [--command <Options>] │
└─────────┴─────────────────────────────────────────────────────────────────────┘
```

### Comece a desenvolver seu app

Com o NativeScript CLI instalado, é hora de começar a desenvolver seu app. Normalmente, você [usa o comando `tns create` para criar uma aplicação vazia](https://github.com/NativeScript/NativeScript-cli#create-project). Pra esse tutorial, nós já estruturamos um projeto padronizado pra servir como ponto de partida para o app [Groceries](https://github.com/NativeScript/sample-Groceries).

<h4 class="exercise-start">
    <b>Exercício</b>: Vá até o ponto de partida do app Groceries
</h4>

Navegue até a pasta onde você quer manter seu código:

<div class="no-copy-button"></div>

```
cd nome-da-pasta-que-guardará-os-arquvivos-do-app
```

Depois, assumindo que você tenha o [git installado](http://www.git-scm.com/), clone o repositório do app Groceries do GitHub.

```
git clone https://github.com/NativeScript/sample-Groceries.git
```

Depois disso, abra a pasta do repositório recém-criado. 

```
cd sample-Groceries
```

O branch master tem o estado final do app Grocieries. Sinta-se livre para [trabalhar nele](https://github.com/NativeScript/sample-Groceries) a qualquer momento, mas, por enquanto, mude para o branch "start" iniciar no objetivo deste guia.

```
git checkout start
```

<div class="exercise-end"></div>

### Adicione as plataformas alvo

Seu app já está configurado, mas antes de executá-lo, você precisa inicializar um projeto nativo específico para cada plataforma alvo.

<h4 class="exercise-start">
    <b>Exercício</b>: Adicione a plataforma iOS e Android.
</h4>

Se você estiver num Mac, comece adicionando a plataforma iOS:

```
tns platform add ios
```

Depois, adicone a plataforma Android com o mesmo comando `platform add`:

```
tns platform add android
```

<div class="exercise-end"></div>

>**IMPORTANTE:** Você pode adicionar apenas plataformas para as quais você já instalou o SDK em sua máquina de desenvolvimento. Se você receber erros ao rodar `tns platform add`, consulte a seção [configurando sua máquina de desenvolvimento](#install-nativescript-and-configure-your-environment).

O comando `platform add` adiciona uma pasta chamada `platforms` ao seu projeto, e copia para ela todos os arquivos dos SDKs nativos necessários. Quando você faz um <i>build</i> (uma espécie de compilação) o CLI NativeScript copia todo o código de seu app para a pasta `platforms`, assim um arquivo binário nativo pode ser criado. 

### Executando seu app

Com a inicialização de plataforma completa, você pode rodar seu app em um emulador ou nos dispositivos.

<h4 class="exercise-start">
    <b>Exercício</b>: Execute seu app
</h4>

Se estiver num Mac, comece rodando o app num simulador de iOS com o seguinte comando:

```
tns run ios --emulator
```

Se tudo correr bem, você deve ver algo como:

![iOS login](../img/cli-getting-started/chapter1/ios/1.png)

Depois, rode seu app num emulador de Android com o seguinte comando:

```
tns run android --emulator
```

>**ATENÇÃO**:
> * Você precisa ter ao menos um Android AVD (Android Virtual Device) configurado pra esse comando funcionar. Se você obter um erro, consulte [configurando um AVD](https://www.genymotion.com/#!/) e rode o comando de novo.
> * Se você estiver usando Genymotion, abra seu dispositivo virtual e então execute `tns run android`.

Se tudo correu bem, você deve ver seu app rodando num emulador de Android.

![Android login](../img/cli-getting-started/chapter1/android/1.png)

<div class="exercise-end"></div>

Aqui estão algumas outras dicas para executar apps NativeScript.

> **DICA**:
> * Para executar num Android ou iOS conectados via USB, use o mesmo comando `run` sem a flag `--emulator`- Por exemplo: `tns run android` e `tns run ios`.
> * O comando `tns device` lista todos os dispositivos (iOS e Android) conectados via USB e dispositivos virtuais Genymotion com os quais `tns run` está habilitado pra trabalhar. Note que `tns device` não lista simuladores de iOS.

### Fluxo de Trabalho

Nesse ponto, você já tem o CLI NativeScript baixado e instalado, bem como as dependências do Android e iOS que você precisa pra rodar seu app. Agora você precisa de um bom fluxo de trabalho que lhe permita fazer alterações e ver os resultados rapidamente.

Um bom jeito de ver suas mudanças é executar `tns run ios` ou `tns run android` depois de salvar os arquivos. Pra ver isso em ação, vamos fazer uma pequena mudança em seu app.

<h4 class="exercise-start">
    <b>Exercício</b>: Sua primeira alteração num app NativeScript
</h4>

Se o comando `tns run ios` ou `tns run android` ainda estiver rodando, digite `Ctrl+C` na linha de comando para finalizá-lo.

Abra o arquivo `app/views/login/login.xml` num editor de texto de sua escolha e altere `<Label text="hello world" />` para `<Label text="hello NativeScript" />`.

Retorne ao console e execute `tns run ios --emulator` (Se estiver num Mac), ou `tns run android --emulator`. Você deve ver o app reabrir e a mudança no texto ser exibida. 

<div class="exercise-end"></div>

Como talvez tenha notado, o comando `tns run` bloqueia o console enquanto seu app está executando (é pra isso que você deve usar `Ctrl` + `C` pra finalizar). A tarefa mostra a saída do comando `console.log()` à medida que seu app executa, e também log de erros quando as coisas dão errado. Assim, se seu app travar durante esse tutorial, veja no console a descrição detalhada do problema. 

Os logs do iOS e Andoroid podem ser meio esquisitos, por isso você talvez precise navegar pelo log pra encontrar o problema real. Por exemplo, se tentar chamar o método `foo.bar()` sendo que `foo` não existe, aqui está a informação obtida no iOS:

```
/app/path/to/file.js:14:8: JS ERROR ReferenceError: Can't find variable: foo
1   0xe3dc0 NativeScript::FFICallback<NativeScript::ObjCMethodCallback>::ffiClosureCallback(ffi_cif*, void*, void**, void*)
```

E aqui a mesma informação nos logs do Android:

```
E/TNS.Native( 2063): ReferenceError: foo is not defined
E/TNS.Native( 2063): File: "/data/data/org.nativescript.groceries/files/app/./views/login/login.js, line: 13, column: 4
```

> **DICA**: Quando estiver tentando debugar um problema, você pode também chamar o método  `console.log()` em seu código JavaScript - Exatamente como faria se estivesse numa aplicativo baseado em navegador.

Se você achar tedioso executar `tns run` no console muitas vezes, você pode se interessar por um dos seguintes fluxos de trabalho:


* O comando `tns livesync` transfere instantanemante arquivos XML, CSS e JavaScript para um app NativeScript que esteja rodando. Se você usar o modificador `--watch` (`tns livesync ios --emulator --watch` ou `tns livesync android --emulator --watch`), o CLI NativeScript observará as mudanças em seu app e irá aplicá-las automaticamente depois de você salvar os aqruivos. Saiba, no entanto, que o comando `livesync` atualmente não exibe a saída de `console.log()` ou as descrições de erro detalhadas. Assim, durante o debug, você talvez queira voltar a usar `tns run`.
* Pra usuários do Sublime Text [esse script](http://developer.telerik.com/featured/a-nativescript-development-workflow-for-sublime-text/) lhe permite digitar `Cmd`/`Ctrl` + `B` para iniciar o build sem usar o console.
*[o módulo npm nativescript-emulator-reload](https://github.com/emiloberg/nativescript-emulator-reload) de  Emil Öberg adiciona um observador Gulp que re-executa o emulador após cada alteração feita.

Agora que você criou um app, configurou seu ambiente de produção, e pôs seu app pra rodar no iOS e Android, você está pronto pra ir mais a fundo nos arquivos que compõem um app NativeScript.  
