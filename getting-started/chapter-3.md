## Application logic
## Lógica do Aplicativo

In this chapter, you'll learn how to add JavaScript logic to your NativeScript app, and you'll be doing so using the base pattern on which the NativeScript framework is built, MVVM, or "model view view model". Here's what those words mean:
Nesse capítulo você aprenderá a adicionar lógica a seu app NativeScript em JavaScript e fará isso usando o padrão no qual NativeScipt é construído, MVVM, ou "model view view model". Essas palavras significam:

- **Model**: The model defines and represents the data. Separating the model from the various views that might use it allows for code reuse.
- **Model**: O <i>model</i> define e representa os dados. Separar o model das várias <i>views</i> que podem utilizá-lo permite reuso de código.

- **View**: The view represents the UI, which in NativeScript is written in XML. The view is often data-bound to the view model so that changes made to the view model in JavaScript instantly trigger visual changes to UI components.
- **View**: A <i>view</i> representa a UI, que em NativeScript é escrita em XML. A view é normalmente linkada dinâmicamente ao <i>view model</i>. Assim, as mudanças feitas no view model em JavaScript instantaneamente dispara alterações visuais nos componentes da UI.

- **View Model**: The view model contains the application logic (often including the model), and exposes the data to the view. NativeScript provides a module called 'Observable', which facilitates creating a view model object that can be bound to the view.
- **View Model**: O <i>view model</i> contém a lógica do aplicativo (muitas vezes incluindo o model), e expõe os dados para a view. NativeScript fornece um módulo chamado 'Observable', que facilita a criação de um objeto view model que pode ser linkado à view.

The biggest benefit of separating models, views, and view models, is that you are able to use two-way data binding; that is, changes to data in the model get instantly reflected on the view, and vice versa. The other big benefit is code reuse, as you're often able to reuse models and view models across views.
O grande benefício de separar models, views e view models é que você pode linkar os dados em "mão dupla", isso é, mudanças nos dados feitas no model se refletem instantaneamente nas views e vice versa. Outra grande vantagem é o reuso do código, visto que você poderá reusar models e view models em suas views. 

In Groceries, so far you've only touched the view (`login.xml`), and in this chapter you'll be creating a view model. To do so, we first need to introduce one other type of file: the code-behind.
No Groceries, você ainda só editou a view (`login.xml`), e nesse capítulo você criará o view model. Pra isso, primeiro precisamos introduzir um outro tipo de arquivo: o code-behind (algo como: código base)

### O code-behind

In NativeScript a code-behind file is a JavaScript file that shares the same name as the view. For example, the login page's view is named `login.xml`, so its code-behind file is named `login.js`. The code-behind file is where you put all code that interacts with the view itself.
Em NativeScript um code-behind é um JavaScript nomeado `login.js`. O arquivo code-behind é onde você põe todo o código que interage com a view em si.

Let's look at what you can do in a code-behind file with a simple example.
Vamos ver o que você pode fazer em um arquivo code-behind com um exemplo simples.

<h4 class="exercise-start">
    <b>Exercício</b>: Contrua o view model do login
</h4>

Open `login.xml` and add a `loaded` attribute to the `<Page>` UI component at the top. It should look like this:
Abra `login.xml` e adicione um atributi `loaded` ao componente UI `<Page>` no topo. Ele deve ficar como:

``` XML
<Page loaded="loaded">
```

Next, paste the code below in `app/views/login/login.js` to define a `loaded()` function:
Depois, cole o código abaixo em `app/views/login/login.js` pra definir a funcção `loaded`:

``` JavaScript
exports.loaded = function() {
    console.log("hello");
};
```
<div class="exercise-end"></div>

> **NOTE**: The keyword `exports` is part of [CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1), the standard on which both NativeScript and Node.js' implementations of modules are based. In CommonJS-based JavaScript modules, a free variable called `exports` is an object to which a module might add properties and methods to configure its external API. Using `exports` in a code-behind file exposes the function for use in the view, or XML file. That is, the `exports.loaded` assignment in the code-behind file is what makes `loaded="loaded"` in the view work.
> **NOTA**: A palavra reservada `exports` faz parte do [CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1), o padrão em que se baseiam as implementações de módulos NativeScript e Node.js. Em módulos baseados em Common-JS, uma váriável livre chamada `exports` é um objeto ao qual um módulo pode adicionar propriedades para configurar sua API externa. Usar `exports` em um arquivo code-behind é o que faz `loaded="loaded"` funcionar na view.


When you run the app with this change, NativeScript triggers the `loaded()` function you created in the code-behind file, and you should see the word “hello” logged in your terminal.
Quando você rodar seu app com essa alteração, NativeScript vai disparar a função `loaded` que você criou no arquivo de código e você deverá ver a palavra "hello" escrita no console.

![](../img/cli-getting-started/chapter3/terminal-1.png)

This simple example shows you how you can append attributes to UI components to run functions in the view's accompanying JavaScript file. Let's use another one of these attributes: `tap`.
Esse exemplo simples mostra como você pode acrescentar atributos a componentes UI para chamar funções na view presentes  no arquivo JavaScript.


<h4 class="exercise-start">
    <b>Exercício</b>: Habilite os botões
</h4>

You can add a `tap` attribute that will fire when the user taps or touches a button. In `app/views/login/login.xml`, switch the two buttons at the bottom of the screen to use this markup:
Você pode adicionar um atributo `tap` que vai disparar quando o usuário tocar no botão. Em `app/views/login/login.xml`, altere os dois botões na parte de baixo da tela para usar essa marcação:


``` XML
<Button text="Sign in" tap="signIn" />
<Button text="Sign up for Groceries" cssClass="link" tap="register" />
```


Then, at the bottom of the `app/views/login/login.js` file, paste in the following `signIn()` and `register()` functions:
Depois, no final do arquivo `app/views/login/login.js`, cole as segunintes funções `singIn()`e `register()`:

``` JavaScript
exports.signIn = function() {
    alert("Signing in");
};

exports.register = function() {
    alert("Registering");
};
```
<div class="exercise-end"></div>

At this point, if you run your app and tap either of the buttons, you will see the appropriate alerts pop up. 
Nesse ponto, se você rodar seu app e tocar qualquer dos dois botões, você verá os alertas aparecerem:

![login 5](../img/cli-getting-started/chapter3/ios/1.png)
![login 5](../img/cli-getting-started/chapter3/android/1.png)

Now that you can see tap gestures working, let's make them do something more interesting than open alerts.
Agora que você pode ver como os gestos de toque funcionam, vamos fazê-los fazer algo mais interessante do quê só abrir alertas.

### Navigating screens
### Navegagando entre Telas

When you tap the “Sign up for Groceries” button, you would expect a navigational change to a registration screen. This is very easy to do in NativeScript.
Quando você toca o botão "Sign up gor Groceries", você, naturalmente, espera uma mudança para a tela de cadastro. Isso é muito fácil em NativeScript. 

<h4 class="exercise-start">
    <b>Exercise</b>: Enable the “Sign up” button on the login screen with a navigational change
</h4>
<h4 class="exercise-start">
    <b>Exercício</b>: Habilite o botão "Sign up" na tela de login a fazer uma mudança de tela.
</h4>

In `app/views/login/login.js`, add this line to the top of the file:
Em `app/views/login/login.js`, adicione essa linha ao topo do arquivo:

``` JavaScript
var frameModule = require("ui/frame");
```

Then, replace the current `register()` function with the version shown below:
Depois, substitua a função ``register()` com a versão mostrada abaixo:

``` JavaScript
exports.register = function() {
    var topmost = frameModule.topmost();
    topmost.navigate("views/register/register");
};
```
<div class="exercise-end"></div>

This function uses the [frame module](/ApiReference/ui/frame/README.html), which is the NativeScript module responsible for navigation in your app. Here, you tell the topmost frame, or the frame the user actually sees, to navigate to the register view. 
Essa função usa o [frame module](/ApiReference/ui/frame/README.html), que o módulo responsável pela navegação em seu app NativeScript. Aqui, você diz ao frame topmost, que é o que o usuário está vendo atualmente, para navegar para a view register.

If you run your app and click the “Sign up for Groceries” button, you will be sent to the registration screen, which we have pre-built for you.
Se você rodar seu app e clicar no botão "Sign up for Groceries", você será redirecionado à tela de cadastro, que nós pré-construimos pra você.

![navigate](../img/cli-getting-started/chapter3/ios/2.gif)
![navigate](../img/cli-getting-started/chapter3/android/2.gif)

Now that you can access the registration page, go ahead and sign up for an account to use for the rest of this tutorial.
Agora que você pode acessar a página de cadastro, vá em frente e cadastre-se em uma conta para completar esse tutorial.

<h4 class="exercise-start">
    <b>Exercise</b>: Register for an account
</h4>
<h4 class="exercise-start">
    <b>Exercício</b>: Cadastre uma conta
</h4>

Open Groceries and tap “Sign up for Groceries” to access the registration page. From there, provide an email address and password, and click the “Sign up” button to create an account.
Abra o app Groceries e clique em "Sing up for Groceries" para acessar a página de cadastro. Na página de cadastro, forneça seu email e senha e clique no botão "Sign up" para criar uma conta.


You can use a fake email address and password, just remember your credentials as you'll need them later.
Você pode usar um email e senha falsos, apenas lembre-se deles para usar depois.
<div class="exercise-end"></div>

> **TIP**: Although our Groceries app doesn't use complex navigation strategies, you have several available to you out of the box, such as the [TabView](/ui-views#tabview) and the [SegmentedBar](/ui-views#segmentedbar). A SideDrawer component is also available for free via Telerik's [UI for NativeScript](https://www.nativescript.org/blog/welcome-to-telerik-ui-for-nativescript) product.
> **DICA**: Embora nosso app atualmente não use estratégias complexas de navegação, existem várias disponíveis pra você, como a [TabView](/ui-views#tabview) e a [SegmentedBar](/ui-views#segmentedbar). Um componente SideDrawer também está disponível de graça via [Telerik's UI for NativeScript](https://www.nativescript.org/blog/welcome-to-telerik-ui-for-nativescript).

### Accessing UI components
### Acessando componentes UI

It's time to see how data flows back and forth between the front end and back end in forms.
É hora de ver como os dados fluem em "pra frente" e "pra trás" entre o front end e o backend em formulários:

<h4 class="exercise-start">
    <b>Exercise</b>: Send data from the front end to the view model
</h4>
<h4 class="exercise-start">
    <b>Exercício</b>: Envie dados do front end para o view model
</h4>

Open `login.xml` and add an `id="email_address"` attribute to the email text field. Its markup should look like this:
Abra `login.xml` e adicione um atributo `id="email_address"` ao campo de texto do email. Sua marcação ficará assim:

``` XML
<TextField id="email_address" hint="Email Address" keyboardType="email" />
```

With an `id` attribute in place, you can access this text field in your code-behind file. To do that, start by opening `app/views/login/login.js` and adding the code below at the top, underneath the `frameModule` variable.
Com um atributo `id` no lugar, você pode acessar esse campo de texto em seu arquivo de código. Para isso, abra `app/views/login/login.js`e adicione o código abaixo ao topo, abaixo da variável `frameModule`.

``` JavaScript
var viewModule = require("ui/core/view");
var email;
```

> **NOTE**: This line of code imports the [view module](/ApiReference/ui/core/view/View.html), which is the base class for all UI components. The module provides a lot of functionality, including the ability to control properties of a view and its children. You're going to use it to get access to the email text field.
> **NOTA**: Essa linha de código importa o [view module](/ApiReference/ui/core/view/View.html), que é a classe base de todos os componentes UI. O módulo provê uma série de funcionalidades, como a habilidade de controlar propriedades da view e seus filhos. Você o usará para acessar o campo de texto do email.

Next, edit the `loaded()` function in `login.js` to get a reference to the email address text field:
Depois, edite a função `loaded()` em `login.js` para obeter uma referência ao campo de texto de email.

``` JavaScript
exports.loaded = function(args) {
    var page = args.object;
    email = viewModule.getViewById(page, "email_address");
};
```

There are two things to note here. First, NativeScript passes `loaded` event handlers a reference to the `<Page>` in the function's argument, which is named `args` by convention. Second, you use the view module's [`getViewById()`](/ApiReference/ui/core/view/View.html) function to get a reference to the text field component.
Há duas coisas para observar aqui. Primeiro, NativeScript passa para aos manipuladores do evento `loaded` uma referência a `<Page>` no argumento da função, que, por convenção, é chamado de `args`. Segundo, você usa a função do view model [`getViewById()`](/ApiReference/ui/core/view/View.html) para obter uma referência ao componente campo de texto.

Finally, edit the `signIn()` function to log the contents of the text field:
Finalmente, edite a função `signIn()` para escrever o conteúdo do campo de texto no console:

``` JavaScript
exports.signIn = function() {
    console.log(email.text);
};
```
<div class="exercise-end"></div>

To see how this works in action, run the app, type some text in the email address text field, and tap the “Sign in” button. If all went well, you should see the text you typed logged in your terminal.
Para ver o funcionamento disso, rode o app, digite algum texto no campo de email e clique no botão "Sign in". Se tudo der certo, você deve ver o texto que você digitou escrito na tela do console.

![](../img/cli-getting-started/chapter3/terminal-2.png)

By accessing UI elements in JavaScript, you can control how those elements look and behave on the front end. However, accessing these UI components individually is a very manual process, and it makes it hard to track the state of the UI. This is where view models come in.
Ao usar JavaScript para acessar elementos da UI, você pode controlar como eles elementos são exibidos e se comportamento no front end. Contudo, acessar componentes UI individualmente é um processo muito manual, e isso torna difícil acompanhar o estado da UI. Aqui entram em cena os view model.

### Adding a view model
### Adicionando um view model

NativeScript provides view model functionality in the form of a module called 'Observable'.
NativeScrip provê a funcionalidade de view model através de um módulo chamado `Observable`.

The Observable is the view model in the MVVM design pattern. It provides a mechanism used for two-way data binding, to enable direct communication between the UI and code-behind file. This means that if the user updates the data in the UI, the change will be automatically reflected in the view model, and vice versa. 
O Observable é o view model no padrão de projeto MVVM. Ele provê um mecanismo usado para "conexão" de dados em "mão dupla", para habilitar a comunicação direta entre a UI e o arquivo <i>code-behind<i/>

<h4 class="exercise-start">
    <b>Exercise</b>: Create a view model and bind it to the view
</h4>
<h4 class="exercise-start">
    <b>Exercício</b>: Crie um view model e ligue-o à view.
</h4>


To allow for two-way data binding using an Observable, open `login.xml`, and replace the two existing TextField UI components with the two shown below, each including a new `text` attribute:
Para permitir conexão de dados em mão dupla usando um Observable, abra `login.xml`, e substitua os dois componentes de UI TextField existentes com os dois mostrados abaixo, cada um incluindo um novo atributo `text`:

``` XML
<TextField id="email_address" text="{% raw %}{{ email }}{% endraw %}" hint="Email Address" keyboardType="email" />
<TextField secure="true" text="{% raw %}{{ password }}{% endraw %}" hint="Password" />
```

> **NOTE**: The use of two curly brackets surrounding the `text` attribute's value delineates a data-bound value. You will be setting corresponding properties with the same name in the view model.
> **NOTA**: U uso de duas chaves no valor do atributo `text` configura-o como um valor <i>data-bound</i> (conectado ao view model). Você definirá propriedades correspondentes com o mesmo nome no view model.

Add the following code to the top of `app/views/login/login.js`, which includes the observable module, and defines a new `user` object, which you'll be using as this page's view model:
Adicione o seguinte código no topo do arquivo `app/views/login/login.js`, que inclui o módulo Observable, e define
um novo objeto `user, que você usará como o view model dessa página:

``` JavaScript
var observableModule = require("data/observable");

var user = new observableModule.Observable({
    email: "user@domain.com",
    password: "password"
});
```

Now, replace the existing `loaded()` function with the one below, which sets `user` as the binding context for the page.
Agora, substitua a função `loaded()` existente com código abaixo, que define `user` como o contexto de ligação de dados para a página.

``` JavaScript
exports.loaded = function(args) {
    var page = args.object;
    page.bindingContext = user;
};
```

<div class="exercise-end"></div>

What's going on here?

1. You're creating a `user` view model that is based on the NativeScript Observable module. You create the view model with two properties, `email` and `password`, that are pre-populated with some dummy values.
2. You bind the page to the `user` view model by setting it as the page's `bindingContext` property. This is specifically what makes the curly bracket syntax work.

O que está acontecendo aqui?

1. Você está criando o view model `user` que é baseado no modulo Observable do NativeScript. Você cria o view model com duas prorpiedades, `email` e `password`, que estão preenchidas com valores quaisquer
2. Você conecta a página ao view model `user` ao definí-lo como a propriedade `bindingContext` da página. É isso, específicamente, que faz a sintaxe das chaves funcionar na view.

Simply put, properties placed on a page's binding context are available to XML elements using the `{% raw %}{{ propertyName }}{% endraw %}` syntax. Because JavaScript sets the view model's `email` to `"user@domain.com"`, and because you bound the email address text field to that property using `<TextField text="{% raw %}{{ email }}{% endraw %}">`, when you run this app you'll see "user@domain.com" appear on the front end.
Em poucas palvaras, proprieadades adicionadas ao contexto de ligação de uma página (`bindindContext`) são disponibilizadas aos elementos XML usando a sintaxe `{% raw %}{{ propertyName }}{% endraw %}`. Visto que você definiu em JavaScript o campo `email` do view model para `"user@domain.com"` e "capturou" no campo de texto do email usando `<TextField text="{% raw %}{{ email }}{% endraw %}">`, quando você rodar o app você verá "user@domain.com" aparecer no front end.


![](../img/cli-getting-started/chapter3/ios/3.png)
![](../img/cli-getting-started/chapter3/android/3.png)

What's really cool is that the binding is two-way. Meaning, when the user types text in these text fields, those changes are immediately applied to your view model.
O mais legal de tudo é que a ligação de dados se dá em "mão dupla". Quer dizer, quando o usuário digita algo nos campos de texto, essas mudanças são aplicadas ao view model também.

To use these values, and to make this login functional by tying your app into a backend service, you're going to need the ability to make HTTP calls. And to make HTTP calls in NativeScript you use the NativeScript fetch module. Let's look at how NativeScript modules work.
Para usar esses valores, e para tornar esse login funcional conectando seu app num serviço de back end, você precisará da funcionalidade de requisições HTTP. E para fazer tais requisições em NativeScript cocê usa o módulo fetch. Vamos ver como móduos NativeScript funcionam.
