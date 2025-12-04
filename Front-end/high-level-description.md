# Front-end high level description

In this articles you'll find a review of the architectural approach of the frontend of the project.

## Stack
We are using the following technologies:

- HTML
- CSS 
- Tailwind: css classes framework
- Flowbite: Tailwind based components library
- HMTX: JS library to implment hypermedia-based webapps
- Alpine.js
- Unfold

## Technological discussion

A review of the current architectural choices have been given in the [index](). In this section we'll dig deeper in the intertwins of the current libraries and approach for the app design.

### Creating a customized Django admin interface

We are using [Django admin](https://docs.djangoproject.com/en/5.2/ref/contrib/admin/) to ease the backend development but we also want a customized UX for the admin site so that it provides more consistency for users. Therefore we need an architectural approach to [overriding Django admin](https://docs.djangoproject.com/en/4.1/ref/contrib/admin/#overriding-the-default-admin-site). In this section we'll be reviewing strategies and justifying our decisions.

**Overriding Django admin panel templates**: we can override blocks of the admin templates, in order to do that we can inspect [Django admin templates](https://github.com/django/django/tree/main/django/contrib/admin/templates/admin) and apply our changes in a block-based basis.

**Creating multiple admin sites**: other possibilty would be to [create multiple admin sites](https://dev.to/rammyblog/how-to-create-multiple-independent-admin-sites-in-django-1klh) ([oficial docs](https://docs.djangoproject.com/en/5.2/ref/contrib/admin/#multiple-admin-sites-in-the-same-urlconf), [implementation using unfold](https://github.com/unfoldadmin/django-unfold/issues/768) ) in order to fully control non-superusers admin site but keep a fully featured superadmin site for developers. We can [add custom templates to one of the admin sites in the app](https://stackoverflow.com/questions/5420990/django-admin-using-different-templates-for-two-admin-site).
We have created a [custom decorator to register models in our custom admin site](https://stackoverflow.com/questions/36985937/django-admin-register-decorator-for-custom-admin-site-class).

**Mandatory use of Tailwind4 with Unfold 0.57 or higher for custom interfaces**: as the Unfold team explains in this post ["Loading Tailwind stylesheet in Django project"](https://unfoldadmin.com/docs/styles-scripts/customizing-tailwind/), tailwind 4 is needed to properly load styles and avoid overwriting exisitng classes.