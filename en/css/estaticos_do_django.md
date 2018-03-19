## Static files in Django

Finally we will take a closer look at these things we've been calling __static files__. Static files are all your CSS and images -- files that are not dynamic, therefore their content doesn't depend on the request context and will be the same for every user.

### Where to put static files for Django

Django already knows where to find the static files for the built-in "admin" app. Now we just need to add some static files for our own app, `blog`.

We do that by creating a folder called `static` inside the blog app:

```
    afropython
    ├── blog
    │   ├── migrations
    │   ├── static
    │   └── templates
    └── mysite
```

Django will automatically find any folders called "static" inside any of your apps' folders, and it will be able to use their contents as static files.