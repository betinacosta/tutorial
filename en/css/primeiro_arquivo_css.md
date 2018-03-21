## Your first CSS file!

Let's create a CSS file now, to add your own style to your web page. Create a new directory called `css` inside your `static` directory. Then create a new file called `blog.css` inside this `css` directory. Ready?

```
    afropython
    └─── blog
         └─── static
              └─── css
                   └─── blog.css
```

Time to write some CSS! Open up the `static/css/blog.css` file in your code editor.

We won't be going too deep into customizing and learning about CSS here. There is a recommendation for a free CSS course at the end of this page if you would like to learn more. 

But let's do at least a little. Maybe we could change the color of our header?
To understand colors, computers use special codes. These codes start with `#` followed by 6 letters (A–F) and numbers (0–9). For example, the code for blue is `#0000FF`. You can find the color codes for many colors here: http://www.colorpicker.com/. You may also use [predefined colors](http://www.w3schools.com/colors/colors_names.asp), such as `red` and `green`.

In your `blog/static/css/blog.css` file you should add the following code:

blog/static/css/blog.css
```css
h1 a {
    color: #DA691A;
}
```

`h1 a` is a CSS Selector. This means we're applying our styles to any `a` element inside of an `h1` element. So when we have something like `<h1><a href="">link</a></h1>`, the `h1 a` style will apply. In this case, we're telling it to change its color to `#FCA205`, which is orange. Of course, you can put your own color here!

In a CSS file we determine styles for elements in the HTML file. The first way we identify elements is with the element name. You might remember these as tags from the HTML section. Things like `a`, `h1`, and `body` are all examples of element names.
We also identify elements by the attribute `class` or the attribute `id`. Class and id are names you give the element by yourself. Classes define groups of elements, and ids point to specific elements. For example, you could identify the following tag by using the tag name `a`, the class `external_link`, or the id `link_to_django_wiki`:

```html
<a href="https://en.wikipedia.org/wiki/Django" class="link_externo" id="link_wikipedia_do_django">
```

You can read more about [CSS Selectors at w3schools](http://www.w3schools.com/cssref/css_selectors.asp).

We also need to tell our HTML template that we added some CSS. Open the `blog/templates/blog/post_list.html` file and add this line at the very beginning of it:

blog/templates/blog/post_list.html
```html
{% load staticfiles %}
```

We're just loading static files here. :) Between the `<head>` and `</head>` tags, after the links to the Bootstrap CSS files, add this line:

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