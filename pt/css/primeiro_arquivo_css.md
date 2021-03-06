## Seu primeiro arquivo CSS!

Vamos criar um arquivo CSS agora, para adicionar seu próprio estilo para sua página da web. Crie um novo diretório chamado `css` dentro de seu diretório `static`. Em seguida, crie um novo arquivo chamado `blog.css` dentro do diretório `css`. Pronto?

    afropython
    └─── blog
         └─── static
              └─── css
                   └─── blog.css


Hora de escrever CSS! Abra o arquivo `static/css/blog.css` no seu editor de código.

Não vamos nos aprofundar muito em customizar e aprender sobre CSS aqui, porque você pode aprender sozinho(a) após esta oficina. Tem uma recomendação de um curso gratuito para aprender mais no final da página.

Mas vamos fazer pelo menos um pouco. Talvez possamos mudar a cor do nosso cabeçalho? Para entender sobre cores, computadores usam códigos especiais. Eles começam com `#` e são seguidos por 6 letras (A-F) e números (0-9). Por exemplo, o código para azul é `#0000FF`. Você pode encontrar vários exemplos de códigos de cores aqui: http://www.colorpicker.com/. Você pode também usar [cores predefinidas](http://www.w3schools.com/colors/colors_names.asp), como `vermelho - red` e `verde - green`.

Em seu arquivo `blog/static/css/blog.css` você deve adicionar o seguinte código:

blog/static/css/blog.css
```css
h1 a {
    color: #DA691A;
}
```

`h1 a` é um seletor de CSS. Isso significa que nós estamos aplicando nossos estilos para qualquer elemento `a` dentro de um elemento `h1`. Então quando tivermos no código algo como `<h1><a href="">link</a></h1>`, o estilo `h1 a` será aplicado. Neste caso nós estamos dizendo para mudar a cor para `#DA691A`, que é laranja. Claro, você pode colocar a cor que você quiser aqui!

Em um arquivo CSS podemos determinar estilos para elementos no arquivo HTML. A primeira maneira de identificar elementos é pelo nome do elemento. Você deve lembrar dessas tags na seção de HTML. Coisas como `a`, `h1` e  `body` são todas exemplos de nomes de elementos. Nós também identificamos elementos pelo atributo `class` ou o atributo `id`. Classe e identificador(id) são nomes que você mesmo dá ao elemento. Classes definem grupos de elementos, e ids apontam para elementos específicos. Por exemplo, você poderia identificar a seguinte tag usando a tag `a`, a classe `link_externo`, ou o id `link_wikipedia_do_django`.

```html
<a href="https://en.wikipedia.org/wiki/Django" class="link_externo" id="link_wikipedia_do_django">
```

Você pode ler mais sobre [Seletores CSS em w3schools](http://www.w3schools.com/cssref/css_selectors.asp).

Então, precisamos também contar ao nosso template HTML que nós adicionamos um CSS. Abra o arquivo `blog/templates/blog/post_list.html` e adicione essa linha bem no início do mesmo:

blog/templates/blog/post_list.html
```html
{% load staticfiles %}
```

Estamos apenas carregando arquivos estáticos aqui :). Agora, entre as tags `<head>` e `</head>`, depois dos links para os arquivos de CSS do Bootstrap, adicione esta linha:

blog/templates/blog/post_list.html
```html
<link rel="stylesheet" href="{% static 'css/blog.css' %}">
```

O navegador lê os arquivos na ordem que eles são informados, então nós temos que nos certificar que esse é o lugar certo. Senão, o código em nosso arquivo pode sobrescrever o código nos arquivos do Bootstrap. Só dissemos ao nosso template onde se encontra nosso arquivo CSS.

Agora, seu arquivo deve ficar assim:

blog/templates/blog/post_list.html
```html
{% load staticfiles %}
<html>
    <head>
        <title>Blog do AfroPython</title>
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
        <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
        <link rel="stylesheet" href="{% static 'css/blog.css' %}">
    </head>
    <body>
        <div>
            <h1><a href="/">Blog do AfroPython</a></h1>
        </div>

        {% for post in posts %}
            <div>
                <p>publicado em: {{ post.published_date }}</p>
                <h1><a href="">{{ post.title }}</a></h1>
                <p>{{ post.text|linebreaksbr }}</p>
            </div>
        {% endfor %}
    </body>
</html>
```

OK, salve o arquivo e atualize o site!

![Blog com as cores do AfroPython](images/blog-com-cores-afropython.png)

Bom trabalho! Talvez a gente também queira dar um pouco de ar ao nosso site e aumentar a margem do lado esquerdo? Vamos tentar!

blog/static/css/blog.css
```css
body {
    padding-left: 15px;
}
```

Adicione isto ao seu arquivo CSS, salve e veja como ele funciona!

![Blog com padding](images/blog-com-padding.png)

Talvez a gente possa customizar a fonte no nosso cabeçalho? Cole na seção `<head>` do arquivo `blog/templates/blog/post_list.html` o seguinte:

blog/templates/blog/post_list.html
```html
<link href="https://fonts.googleapis.com/css?family=Roboto:400,700" rel="stylesheet">
```

Como antes, confira a ordem e coloque antes do link para `blog/static/css/blog.css`. Essa linha irá importar uma fonte chamada *Roboto* do Google Fonts (https://www.google.com/fonts).

Encontre o bloco com a declaração `h1 a` (o código entre chaves `{` and `}`) dentro do arquivo CSS `blog/static/css/blog.css`.  Agora adicione a linha `font-family: 'Roboto';` entre as chaves, e atualize a página:


Agora adicione a linha `font-family: 'Roboto';` no CSS do arquivo `static/css/blog.css` dentro do bloco de declaração `h1 a` (o código entre as chaves `{` e `}`) e atualize a página:

blog/static/css/blog.css
```css
h1 a {
    color: #DA691A;
    font-family: 'Roboto';
}
```

![Blog com a fonte alterada](images/fonte-roboto.png)

Incrível!

Como mencionado acima, CSS usa o conceito de classes, que basicamente permite que você nomeie parte do código HTML e aplique estilos apenas à esta parte, sem afetar as outras. É super útil se você tiver duas `divs`, mas eles estão fazendo algo muito diferente (como o seu cabeçalho e seu post). Uma classe pode ajudar você a fazer com que eles tenham um visual diferente.

Vá em frente e o nomeie algumas partes do código HTML. Adicione uma classe chamada de `cabecalho-pagina` para a `div` que contém o cabeçalho, assim:


blog/templates/blog/post_list.html
```html
<div class="cabecalho-pagina">
    <h1><a href="/">Blog do AfroPython</a></h1>
</div>
```

E agora, adicione uma classe `post` em sua `div` que contém um post de blog.

blog/templates/blog/post_list.html
```html
<div class="post">
    <p>publicado em: {{ post.published_date }}</p>
    <h1><a href="">{{ post.title }}</a></h1>
    <p>{{ post.text|linebreaksbr }}</p>
</div>
```

Agora adicionaremos blocos de declaração para seletores diferentes. Seletores começando com `.` se referem às classes. Existem muitos tutoriais e explicações sobre CSS na Web para ajudar você a entender o código a seguir. Por enquanto, basta copiar e colá-lo em seu arquivo `blog/static/css/blog.css` :

blog/static/css/blog.css
```css
.cabecalho-pagina {
    background-color: #ff9400;
    margin-top: 0;
    padding: 20px 20px 20px 40px;
}

.cabecalho-pagina h1, .cabecalho-pagina h1 a, .cabecalho-pagina h1 a:visited, .cabecalho-pagina h1 a:active {
    color: #ffffff;
    font-size: 36pt;
    text-decoration: none;
}

.content {
    margin-left: 40px;
}

h1, h2, h3, h4 {
    font-family: 'Roboto', cursive;
}

.date {
    color: #828282;
}

.save {
    float: right;
}

.post-form textarea, .post-form input {
    width: 100%;
}

.top-menu, .top-menu:hover, .top-menu:visited {
    color: #ffffff;
    float: right;
    font-size: 26pt;
    margin-right: 20px;
}

.post {
    margin-bottom: 70px;
}

.post h1 a, .post h1 a:visited {
    color: #000000;
}
```

Então envolva o código HTML que exibe as mensagens com declarações de classes. Substitua isto:

blog/templates/blog/post_list.html
```html
{% for post in posts %}
    <div class="post">
        <p>publicado em: {{ post.published_date }}</p>
        <h1><a href="">{{ post.title }}</a></h1>
        <p>{{ post.text|linebreaksbr }}</p>
    </div>
{% endfor %}
```

no arquivo `blog/templates/blog/post_list.html` por isto:

blog/templates/blog/post_list.html
```html
<div class="content container">
    <div class="row">
        <div class="col-md-8">
            {% for post in posts %}
                <div class="post">
                    <div class="date">
                        <p>publicado em: {{ post.published_date }}</p>
                    </div>
                    <h1><a href="">{{ post.title }}</a></h1>
                    <p>{{ post.text|linebreaksbr }}</p>
                </div>
            {% endfor %}
        </div>
    </div>
</div>
```

Salve esses arquivos e atualize seu site.

![Blog com CSS completo](images/blog-com-css-completo.png)

Uhuu! Ficou incrível, né? Olhe para o código que nós acabamos de colar para encontrar os lugares aonde nós adicionamos classes no HTML e as usamos no CSS. Aonde você faria a mudança para que a data ficasse com a cor turquesa ?

Não tenha medo de brincar com esse CSS um pouco e tente mudar algumas coisas. Brincar com o CSS pode ajudar você a entender as
diferentes coisas que estão sendo feitas. Se você bagunçar tudo, não se preocupe - você sempre pode voltar atrás!

Nós realmente recomendamos que faça esse curso on-line [Curso de HTML & CSS do Code Academy](https://www.codecademy.com/pt-BR/tracks/web). Ele pode ajudar você a aprender tudo sobre como tornar seus sites mais bonitos com CSS.

Pronto para o próximo capítulo?! :)