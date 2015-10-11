## Criando a UI (Interface de Usuário)

Antes de começar a programar seu app Groceries, é importante entender a organização da estrutura de pastas do NativeScript. Isso o ajudará a entender onde criar novos arquivos, bem como um pouco do que acontece no NativeScript "por baixo dos panos".

Vá em frente e abra a pasta `sampla-Groceries` de seu app e seu editor de textos e vamos mais a fundo.

### Estrutura do Diretório

Para manter as coisas simples, vamos começar olhando o rascunho da estrutura  do app Groceries:

```
.
└── sample-Groceries
    ├── app
    │   └── ...
    ├── node_modules
    │   └── tns-core-modules
    ├── package.json
    └── platforms
        ├── android
        └── ios
```

Isso é o que essas várias pastas e arquivos fazem:

- **app**: Essa pasta contém todos os recursos que você precisa pra construir seu app. Você passará a maior parte do tempo editando arquivos nela. 

- **node_modules**: Essa pasta contém as dependências do módulo npm de seu app. Todos os novos projetos começam com uma única depencência em tns-core-modules.
 
- **node_modules/tns-core-modules**: Essa pasta contém os módulos de seu aplicativo, que são uma série de módulos JavaScript providos pelo NativeScript que você vai usar pra construir seu app. Cada módulo contém o código específico a plataforma necessário pra implementar alguma funcionalidade- a câmera, requisições http, o sistema de arquivos, e muitos outros -exposta através de uma API independente de plataforma (ex.: `camera.takePicture()`). Veremeos alguns exemplos brevemente.

- **package.json**: Esse arquivo contém os detalhes de configuração de seu app, como o id do app, a versão do NativeScript que você está usando, e também quais módulos npm seu app usa. Vamos ver mais aprofundadamente como usar esse arquivo quando falarmos sobre como usar módulos npm no [capítulo 5](#plugins-and-npm-modules).
 
- **platforms**: Essa pasta contém código específico de plataforma que NativeScript precisa para construir apps iOS e Android nativos. Por exemplo na pasta `android` você encontra coisas como o `AndroidManifest.xml` de seu projeto e arquívos executáveis .apk.
Similarmente, a pasta `ios` contém o projeto Xcode do app  e arquivos executáveis .ipa. Note que usuários do Windows não terão uma pasta `ios`.

O CLI NativeScript gerencia a pasta `platforms` pra você conforme você desenvolve e roda seu app; portanto, é uma boa prática tratar a pasta `platforms`como código gerado. O app Groceries inclui a pasta `platforms`em [seu `.gitignore`](https://github.com/NativeScript/sample-Groceries/blob/master/.gitignore) para deixar seus arquivos fora do controle de versionamento (Nota de tradução: pra serem ignorados pelo git).

Agora, vamos entender a estrutura da pasta `app`, já que é nela que você passará a maior parte do tempo.

```
.
└── sample-Groceries
    ├── app
    │   ├── App_Resources
    │   │   ├── Android
    │   │   └── iOS
    │   ├── shared
    │   │   └── ...
    │   ├── views
    │   │   └── login
    │   │       ├── login.js
    │   │       └── login.xml
    │   ├── app.css
    │   ├── app.js
    │   └── ...
    └── ...
```
Isso é o que esses vários arquivos e pastas fazem:

- **App_Resources**: Essa pasta contém recuros esecíficos a plataforma, como icones, telas de abertura e arquivos de configuração. O CLI NativeScript cuida de injetar esses recursos nos lugares apropriados na pasta `platforms`quando você executa `tns run`.

- **shared**: Essa pasta, exclusiva do app Groceries, guarda qualquer arquivo que você precise compartlihar entre várias <i>views</i> no app. No Groceries você encontrará alguns objetos <i>view model</i> e um arquivo `config.js` usado pra compartilhar variáveis de configurações como chaves de API.

- **views**: Essa pasta contém o código pra contruir as telas do app, cada uma contendo uma subpasta dentro de `views`. Cada view e composta de um arquivo XML, um arquivo JavaScritp e um arquivo opcional de CSS. O app Groceries contém três pastas pra suas três views.

- **app.css**: Esse arquivo contém regras de estilo globais do seu app. Estudaremos ele outra na [seção 2.3](#css).

- **app.js**: Esse arquivo configura o módulo de inicialização de seu aplicativo.

Vamos começar com `app/app.js`, porque ele é o ponsto de partida dos aplicativos NativeScript. Seu `apps.js` contém as três linhas abaixo:

``` JavaScript
var applicationModule = require("application");
applicationModule.mainModule = "views/login/login";
applicationModule.start();
```
No código, você está solicitando, ou importando (require()), o [módulo application do NativeScript](/ApiReference/application/HOW-TO.md). Depois você  define seu `mainModule`, ou a tela inicial de seu app, como a tela de login; que está localizada na pasta `views/login` de seu app.

> **DICA**: Módulos NativeScript em JavaScript seguem a  [CommonJS specification](http://wiki.commonjs.org/wiki/CommonJS). Isso significa que você pode usar o [método `require()`](http://wiki.commonjs.org/wiki/Modules/1.1#Module_Context) para importar módulos, como feito acima, bem como usar a palavra-reservada `exports` pra expor as propiedades e métodos de um módulo, que trataremos depois neste capítulo. Esses são os mesmos construtores que Node.js usa pra módulos JavaScript, assim, se você sabe como usar módulos do Node.js, você já sabe como usar os módulos NativeScript.

Agora que seu app está pronto pro desenvolvimento, vamos adicionar alguns componentes de UI pra fazer nossa tela de login mais atraente do quê somente texto.

### Adicionando compontentes UI

Vamos "cavar" mais fundo nos arquivos usados para criar a UI de seu app, que estão armazenados em`apps/views`. Cada pasta em `app/views` contém o código de uma das três páginas no Groceries: `list`, `login`, e `register`. Se você olhar na pasta `app/view/login`, você verá três arquivos: `login.css`, `login.js` e `login.xml`, este último foi modificado por nós no capítulo anterior. Quando você abre `login.xml` novamente você vê o seguinte código:

``` XML
<Page>
    <Label text="hello NativeScript" />
</Page>
```

Essa página atualmente contém dois componentes UI: um `<Page>` e um `<Label>`. Pra deixar essa página mais parecida com uma página de login, vamos adicionar alguns componentes extra, que serão dois elementos `<TextField>` e dois `<Button>`. 

<h4 class="exercise-start">
    <b>Exercício</b>: Adicione componentes UI no arquivo <code>login.xml</code>
</h4>

Abra `app/views/login/login.xml` e substitua o `<Label>` existente com o seguinte código:

``` XML
<TextField hint="Email Address" keyboardType="email" />
<TextField hint="Password" secure="true" />

<Button text="Sign in" />
<Button text="Sign up for Groceries" />
```

<div class="exercise-end"></div>

Os componetntes UI do NativeScript lhe permitem configurar seu comportamentoe aparência através de alguns atributos. O código que você adicionou usa os seguintes atributos: 

- `<TextField>` (Campo de Texto)
    - `hint`: Usado para exibir um texto padrão(placeholder) no TextField para informar ao usuário o quê digitar. 
    - `secure`: Um atributo booleano (true, false) que determina se o texto no TextField deve ser mascarado, comumente feito em campos de senha.
    - `keyboardType`: O tipo de teclado a ser apresentado ao usuário para digitação. `keyboardType="email"` exibe um teclado otimizado para a entrada de endereços de email. NativeScript atualmente suporta [cinco tipos de teclado](/ApiReference/ui/enums/KeyboardType/README.md) para campos de texto.
- `<Button>`
    - `text`: Controla o texto mostrado dentro do botão

Após você  [rodar seu app](#development-workflow) com essa alteração, você verá um único componente `<Button>` na tela.

![login 1](../img/cli-getting-started/chapter2/ios/1.png)
![login 1](../img/cli-getting-started/chapter2/android/1.png)

Você precisa informar ao NativeScript como formatar o layout dos componentes UI em sua página. Vamos ver como usar os layouts do NativeScript para organizar esses componentes na tela.

> **DICA**: A documentação do NativeScript inclui a  [lista completa de componentes UI e seus atributos](/ui-with-xml.md) que você pode utilizar para construir seu app. Você pode até [construir seu próprio componente UI](https://docs.nativescript.org/ui-with-xml#custom-components).

### Layouts 

NativeScript oferece vários containers de layout que lhe permitem posicionar componentes UI precisamente onde cocê quer que eles apareçam.

- O  [Absolute Layout](https://docs.nativescript.org/ApiReference/ui/layouts/absolute-layout/HOW-TO.md) lhe permite posicionar elementos usando coordenadas x, y explicitamente. Isso é últil quando você precisa por elementos em posições exatas, por exemplo exibir um widget indicador de atividade na esquerda superior de seu app. 

- O  [Dock Layout](https://docs.nativescript.org/ApiReference/ui/layouts/dock-layout/HOW-TO.md) é últil para posicionar elementos UI nas bordas extremas de seu app. Por exemplo, um container <i>dockado</i> na parte de baixo de seu app seria um bom lugar pra um anúncio.

-  O [Grid Layout](https://docs.nativescript.org/ApiReference/ui/layouts/grid-layout/HOW-TO.md) permite-lhe dividir a interface em uma série de linhas e colunas, bem parecido com a `<table>` em HTML.

- O [Stack Layout](https://docs.nativescript.org/ApiReference/ui/layouts/stack-layout/HOW-TO.md) lhe permite empilhar componentes-filhos vertical ou horizontalmente.

- O  [Wrap Layout](https://docs.nativescript.org/ApiReference/ui/layouts/wrap-layout/HOW-TO.md) permite componentes-filhos  <i>fluírem</i> de uma linha ou coluna para a próxima quando o espaço vazio é preenchido.

> **DICA**:
> * Para uma introdução a outros elementos de layout do NativeScript, veja o artigo de Jen Looper em [desmistificando layouts NativeScript](https://www.nativescript.org/blog/demystifying-nativescript-layouts).
> * Consulte a documentação do NativeScript para uma [visão mais detalhada sobre o funcionamento dos layouts NativeScript](/layouts) e as várias coisas que você pode fazer para configurá-los.

Para sua tela de login, tudo que você precisa é um simples `<StackLayout>` para empilhar componentes UI no topo uns dos outros. Em seções mais a frente você usará alguns layouts mais avançados.

<h4 class="exercise-start">
    <b>Exercício</b>: Adicione um stack layout para a tela de login
</h4>

Em `login.xml`, adicione o componente `<StackLayout>` dentro do componente `<Page>`. `login.xml`agora deve se parecer com isso:

``` XML
<Page>
    <StackLayout orientation="vertical">

        <TextField hint="Email Address" keyboardType="email" />
        <TextField hint="Password" secure="true" />

        <Button text="Sign in" />
        <Button text="Sign up for Groceries" />

    </StackLayout>
</Page>
```

<div class="exercise-end"></div>

O stcak layout é um componente UI, e como tal, ele possui atributos, assim, como os componentes `<TextField>` e `<Button>` que você usou na seção anterior. Aqui, o atributo `orientation="vertical"` diz ao stack layout para organizar seus componentes verticalmente.

Após rodar seu app com essa alteração, você verá que os componentes do login de sua página empilharam-se.

![login 2](../img/cli-getting-started/chapter2/ios/2.png)
![login 2](../img/cli-getting-started/chapter2/android/2.png)

Embora os componentes UI estejam na ordem correta, eles poderiam ter algum espaçamento e cores diferentes para tornar o app um pouco mais bonito. Para fazer isso vamos ver outra funcionalidade do NativeScript: CSS.

### CSS

NativeScript usa um [subconjunto do CSS](/styling) para alterar a aparência visual de seu app. Você pode usar três mecanismos para adicionar propriedades CSS para os componentes UI: [CSS global](/styling#application-wide-css) (`app.css`), [CSS específico para uma página](/styling#page-specific-css), e um[atributo `style` inline](/styling#inline-css).

> **DICA**:
> * Ponha as regras CSS que devem se aplicar a todas as páginas em seu `app.css` e as regras CSS que apliquem-se a uma única página em um arquivo CSS específico àquela página. (ex.: `login.css`).
> * Embora estilo inline seja útil para testes rápidos - ex.:  `<Page style="background-color: green;">` , você deve evitar usá-lo no geral, porque os atributos `<style>` tendem a sobrecarregar visualmente os arquivos XML, especialmente se você precisa aplicar multiplas regras.

Vamos começar adicionando algumas regras CSS globais.

<h4 class="exercise-start">
    <b>Exercício</b>: Crie regras globais
</h4>

Cole o seguinte código no arquivo `app.css`:

``` CSS
Page {
    background-color: white;
    font-size: 17;
}
TextField {
    margin: 10;
    padding: 10;
}
Image {
    margin-top: 20;
    margin-left: 0;
    margin-right: 0;
    margin-bottom: 80;
}
Button {
    margin: 10;
    padding: 10;
}
```

<div class="exercise-end"></div>

Se você já desenvolveu para a web antes, a sintaxe deve soar bem familiar aqui. Você selecionou quatro componentes UI  (Page, TextField, Image e Button) pelas suas tags, então aplicou algumas regras CSS úteis como pares de nome:valor. NativeScript não suporta todas as propriedades CSS porque não é possível implementá-las em apps nativos sem causar problemas de performance. Uma [lista completa de propriedades CSS que NativeScript suporta](/styling#supported-properties) está em sua documentação.

Vamos fazer mais uma mudança. Embora muitas vezes se queira que regras CSS se apliquem igualmente no seu app iOS e Android, às vezes faz sentido aplicar uma regra CSS em somente uma plataforma. Por exemplo, campos de texto do iOS normalmente tem bordas ao seu redor, mas os campos de texto do Android não tem. Vamos ver como fazer mudanças de estilo direcionadas à plataformas específicas em NativeScript. 

<h4 class="exercise-start">
    <b>Exercício</b>: Adicione CSS específico a plataforma
</h4>

Adicione o seguinte como a primeira linha  do arquivo `app.css` de seu aplicativo:

``` CSS
@import { url('~/platform.css') };
```

> **IMPORTANTE**: NativeScript é consistente com implementações de navegador, assim declarações `@import` devem preceder todas as outras regras CSS em um arquivo.

Agora, adicione um atributo `cssClass="link"` ao botão de registrar em `login.xml`. A marcação do botão deve se parecer com isso: 

``` XML
<Button text="Sign up for Groceries" cssClass="link" />
```

<div class="exercise-end"></div>

Vamos esmiuçar o que aconteceu. Primeiro, NativeScript suporta a declaração CSS `@import` para importação de um arquivo CSS dentro de outro. Assim essa nova linha de código importa as regras CSS de `platform.css` para `app.css`. Mas, você deve ter notado que oapp não tem um arquivo chamado `platform.css` - Apenas `app/platform.android.css` `app/platform.ios.css` existem. O que aconteceu aqui?

<a id="platform-specific-files"></a>Quando você executa `tns run`ou `tns livesync`, o CLI NativeScript pega seu código da pasta `app` e o põe nos projetos nativos localizados na pasta `platforms/ios` e `platforms/android`. Aqui as convenções de nomeação  entram em cena: quando move os arquivos, o CLI inteligentemente seleciona arquivos `.android.*` e `.ios.*`. Pra dar um exemplo específico, o CLI move `platform.ios.css` em `platforms/ios` e renomeia-o para `platform.css`; similarmente o CLI move  `platform.android.css` para`platforms/android` e novamente renomeia-o para `platform.css`. Essa convenção provê uma maneira conveniente de ramificar seu código para tratar iOS e Android separadamente, e é suportada pra qualquer tipo de arquivoem NativeScript - não apenas arquivos CSS. Você verá um pouco mais dessa convenção depois nesse tutorial.

Há uma outra mudança aqui que precisamos discutir. É o atributo `cssClass` que você adicionou ao botão:

``` XML
<Button text="Sign up for Groceries" cssClass="link" />
```

NativeScript usa o atributo `cssClass` para adicioar classes CSS a componentes UI. O nome da classe é usado para dar ao botão de registro uma aparência ligeiramente diferente da do botão de login. Você as regras CSS associadas à essa classe em `platform.ios.css` e `platform.android.css`:


``` CSS
/* From platform.android.css */
.link {
    background-color: transparent;
}

/* From platform.ios.css */
.link {
    border-width: 0;
}
```

> **DICA**: NativeScript suporta também selecionar elementos pelos seu atributo `id`. Consulte a documentação para ver  a [lista completa de seletores suportados](/styling#supported-selectors).

Com essas alterações no lugar, você notará que o app se parece um pouco melhor agora, e também tem aparencias diferenciadas no iOS e Android.

![login 1](../img/cli-getting-started/chapter2/ios/3.png)
![login 1](../img/cli-getting-started/chapter2/android/3.png)

Sinta-se a vontade para passar algum tempo brincando com a aparencia desse app antes de prosseguir.Você pode tentar adicionar alguns classes CSS, ou adicionar algum outro estilo em `login.css`. Quando estiver pronto, vamos seguir em frente adicionar uma imagem a essa tela de login.

### Imagens

Em NativeScript você usa o componente UI `<Image>` e seu atributo `src`para adicionar imagens em suas páginas. O atributp `src` permite-lhe apontar pra sua imagem de três formas. A primeira (e mais simples) é apontar para a URL de uma imagem:

``` XML
<Image src="https://www.nativescript.org/images/default-source/landingpages/logo.png" />
```
A segunda forma é apontar para uma imagem que esteja na pasta `app` de seu aplicativo. Por exemplo se você tem uma imagem em `app/images/logo.png`, você pode usá-la com:

``` XML
<Image src="~/images/logo.png" />
```
A terceira forma, e a forma que o app Groceries usa, é usar recursos específicos a plataforma. Vamos adicionar uma imagem à tela de login e discutir exatamenre o que acontece.

<h4 class="exercise-start">
    <b>Exercício</b>: Adicione um logo
</h4>

Em `login.xml`, adicione o componente `<Image>` abaixo como o primeiro elemento-filho da tag `<StackLayout>`:

``` XML
<Image src="res://logo" stretch="none" horizontalAlignment="center" />
```

<div class="exercise-end"></div>

A sintaxe `res://` diz ao NativeScript para usar um recurso específico a plataforma, nesse caso uma imagem. Recursos direcionados a plataforma ficam na pasta `app/App_Resources` de seu aplicativo. Se você olhar lá, encontrará alguns arquivos de imagens diferentes, vários deles denominados `logo.png`. 

Embora mais complexa do quê inserir uma imagem diretamente na pasta `app`, usar imagens para cada plataforma dá a você mais controle sobre a exinição de imagens em dispositivos com dimensões diferentes. Por exemplo iOS o deixa fornecer três imagens diferentes para dispositivos com diferentes densidades de pixel. Por isso você encontrará logos nomeadoscomo `logo.png`, `logo@2x.png`, e `logo@3x.png` na pasta `App_Resources/iOS`. Para Android você vai encontrar arquivos similares em `App_Resources/Android/drawable-hdpi` (para "high" dpi, ou high pontos-per-inch (pontos-por-polegada)) e  `App_Resources/Android/drawable-ldpi` (para low-dpi).

Tendo esses arquivos no lugar, o framework NativeScript sabe como pegar o correto; tudo que você tem de fazer é referenciar a imagem usando `res://` e a base do nome do arquivo - ex.: `res://logo`. É assim que sua tela de login deve parecer no iOS e no Android.

![login 4](../img/cli-getting-started/chapter2/ios/4.png)
![login 4](../img/cli-getting-started/chapter2/android/4.png)

Nesse ponto sua UI parece mais bonita, mas o app ainda não faz nada. Vamos ver como podemos usar JavaScript para adicionar algumas funcionalidades.
