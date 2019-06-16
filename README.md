### General notes!

1. The editing of views can be confusing sometimes, would be easier if you just had the full code for the `before` and `after`
2. importing stuff is schetchy as well and can be confusing
3. sometimes urls are done using paths and other times they are used via the `url` tag
   example :
   ```html
   <a href="/drafts/{{ draft.slug }}/">
     vs
     <form action="{% url 'draft-edit' draft.slug %}" method="POST"></form
   ></a>
   ```
4. need better styling in general its very ugly sorry bro

### github repo

there is no starter just a solution (just a note)

### creating-a-django-project

1. Windows portion should be

```bash
$ superblog_env\Scripts\activate
```

2. When installing django we might need to pick a specific version to match the tutorial

```bash
pip install django==2.1
```

for example

3. in the soluation branch the main project name is `project` when in the tutorial its `superblog`

### hello world page

1. the import for `from articles import views` is there but isn't very clear that we should add it, maybe seperate it from the list of urlpatterns

2. Same issue with the `views.py` portion I think the imports should be seperated or paste the whole file

### detail page

1. the picture has a different url than the one we should visit

### form classes

1. whats a PasswordInput() widget that wasn't explained

### create page

1. it was confusing adding the `Write!` button in `list.html` because I almost copy/pasted it without noticing the triple dots, maybe an indication would be nice remember we are dealing with nubs

### automatically assign author

changing `article = form.save()` to `article = form.save(commit=False)` but you did not add article.save() at the end so it never saved any new articles after that

### draft list page

1. Where in the page do i write

```html
{% if request.user.is_authenticated %} ...
<a href="{% url 'draft-list' %}">
  <button>
    Drafts
  </button>
</a>
{% else %}
```

?

same issue with the `...` not being visiable and ruinning my day

### draft edit

1. `Change your draft_edit() view to:` this part will break the edit page
   should have

```python
    context = {
       'form': form,
       'draft': article
   }
   return render(request, "draft_edit.html", context)
```

at the end of it

2. `path('articles/<int:article_id>/', views.detail),` is wrong it should've been `views.article_detail`

### slugs

1. should mention to set slugfield as unique
2. should mention that we need to delete the older articles because we added a new field that isn't nullable
3. we can make create_slug into a method instead of creating a utils.py file
4. editing the draft_edit view was confusing for a moment because of all the triple dots `...`
5. `def create_slug(instance, new_slug=None):` wasn't obvious or explained and caused an error because I didnt replace the start of the function with the rest(was my mistake but could be more obvious)

### profile page

1. if the user doesn't have a first name or a last name

`<p>Published by: <a href="/profiles/{{ article.author.username }}/">{{ article.author.first_name }} {{ article.author.last_name }}</a></p>`

wont show the link to the profile, consider adding a `-` inbetween first name and last name

### about

1. consider changing the imports of
   `from .models import Profile` to be
   `from .models import Profile, Article`
   so they won't be in a seperate line

2) Previous users won't have a profile so it will give you an error, you have to re-create a superuser or go to the shell and create your own profile

### implementing-markdown

1. security note, when doing this `<p>{{ article.body|makemarkdown|safe }}</p>` you allow a security exploit called `xss` to happen in the page, if you go and create a new articale and it had something like this for example

```html
"><script>
  alert(document.cookie);
</script>
```

it will trigger this script which is unsafe

### share-link

1. won't work because we don't have jquery it will pop up an error
