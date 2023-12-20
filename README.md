A Django starter project with Tailwind, Alpine.js and HTMX. Based on [DjangoX](https://github.com/wsvincent/djangox) by Will Vincent.

## New features
- Styling with [Tailwind](http://tailwindcss.com).
- Interactivity with [Alpine.js](https://alpinejs.dev).
- Modern front-end experience via [HTMX](https://htmx.org/).
- Environment variables with python-dotenv.
- Media file support via Cloudinary.

### DjangoX features

- Django 4.2 & Python 3.11
- Install via [Pip](https://pypi.org/project/pip/) or [Docker](https://www.docker.com/)
- User log in/out, sign up, password reset via [django-allauth](https://github.com/pennersr/django-allauth)
- Static files configured with [Whitenoise](http://whitenoise.evans.io/en/stable/index.html)
- Debugging with [django-debug-toolbar](https://github.com/jazzband/django-debug-toolbar)
- DRY forms with [django-crispy-forms](https://github.com/django-crispy-forms/django-crispy-forms)
- Custom 404, 500, and 403 error pages

## Getting started

Follow the installation instructions below, then follow these steps to configure the extra bits.

### Environments

Create a .env file in your project root and add your secret key and debug settings.

### Tailwind

Forms are styled with crispy-tailwind, but it doesn't support dark mode so I've had to override a bunch of templates. These are in templates/tailwind.

#### Development mode

```
python manage.py tailwind start
```

To run tailwind in development mode. This will watch for changes and use browsersync to auto-reload the browser.

#### Production mode

```
python manage.py tailwind build
```

This will create a build optimised for production.

### HTMX

#### Browsing between pages
Add the following code to your a tags:

```
 hx-get="{% url 'home' %}" hx-target="body" hx-push-url="true" hx-indicator=".progress"
```

- `hx-get="{% url 'home' %}` - The target page if a link, should be the same as the href
- `hx-target="body"` – The element to switch out content from. Can be set to any element, but body is useful for switching between pages.
- `hx-push-url="true"` – Adds the link to the browser history/back button. 
- `hx-indicator=".progress"` – Shows the progress indicator at the top of the page when loading.

### Cloudinary

Uncomment the Cloudinary config in settings.py and add your cloud name, API key and secret to your environment variables.

Import Cloudinary in models.py:

```
from cloudinary.models import CloudinaryField
from cloudinary.uploader import upload
```

Add Cloudinary fields to your model:

```
image = CloudinaryField('image')
```

---

## DjangoX

> A batteries-included Django starter project. To learn more try the books [Django for Beginners](https://djangoforbeginners.com), [Django for APIs](https://djangoforapis.com), and [Django for Professionals](https://djangoforprofessionals.com).

### 🚀 Features

- Django 4.2 & Python 3.11
- Install via [Pip](https://pypi.org/project/pip/) or [Docker](https://www.docker.com/)
- User log in/out, sign up, password reset via [django-allauth](https://github.com/pennersr/django-allauth)
- Static files configured with [Whitenoise](http://whitenoise.evans.io/en/stable/index.html)
- Styling with [Bootstrap v5](https://getbootstrap.com/)
- Debugging with [django-debug-toolbar](https://github.com/jazzband/django-debug-toolbar)
- DRY forms with [django-crispy-forms](https://github.com/django-crispy-forms/django-crispy-forms)
- Custom 404, 500, and 403 error pages
----

### Table of Contents
* **[Installation](#installation)**
  * [Pip](#pip)
  * [Docker](#docker)
* [Next Steps](#next-steps)
* [Contributing](#contributing)
* [Support](#support)
* [License](#license)

----

## 📖 Installation
DjangoX can be installed via Pip or Docker. To start, clone the repo to your local computer and change into the proper directory.

```
$ git clone https://github.com/MattKevan/djangox-tailwind.git
$ cd djangox-tailwind
```

### Pip

```
$ python -m venv .venv

# Windows
$ Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
$ .venv\Scripts\Activate.ps1

# macOS
$ source .venv/bin/activate

(.venv) $ pip install -r requirements.txt
(.venv) $ python manage.py migrate
(.venv) $ python manage.py createsuperuser
(.venv) $ python manage.py runserver
# Load the site at http://127.0.0.1:8000
```

### Docker

To use Docker with PostgreSQL as the database update the `DATABASES` section of `django_project/settings.py` to reflect the following:

```python
# django_project/settings.py
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": "postgres",
        "USER": "postgres",
        "PASSWORD": "postgres",
        "HOST": "db",  # set in docker-compose.yml
        "PORT": 5432,  # default postgres port
    }
}
```

The `INTERNAL_IPS` configuration in `django_project/settings.py` must be also be updated:

```python
# config/settings.py
# django-debug-toolbar
import socket
hostname, _, ips = socket.gethostbyname_ex(socket.gethostname())
INTERNAL_IPS = [ip[:-1] + "1" for ip in ips]
```

And then proceed to build the Docker image, run the container, and execute the standard commands within Docker.

```
$ docker-compose up -d --build
$ docker-compose exec web python manage.py migrate
$ docker-compose exec web python manage.py createsuperuser
# Load the site at http://127.0.0.1:8000
```

## Next Steps

- Add environment variables. There are multiple packages but I personally prefer [environs](https://pypi.org/project/environs/).
- Add [gunicorn](https://pypi.org/project/gunicorn/) as the production web server.
- Update the [EMAIL_BACKEND](https://docs.djangoproject.com/en/4.0/topics/email/#module-django.core.mail) and connect with a mail provider.
- Make the [admin more secure](https://opensource.com/article/18/1/10-tips-making-django-admin-more-secure).
- `django-allauth` supports [social authentication](https://django-allauth.readthedocs.io/en/latest/providers.html) if you need that.

I cover all of these steps in my three books: [Django for Beginners](https://djangoforbeginners.com), [Django for APIs](https://djangoforapis.com), and [Django for Professionals](https://djangoforprofessionals.com).

----

## 🤝 Contributing

Contributions, issues and feature requests are welcome! See [CONTRIBUTING.md](https://github.com/wsvincent/djangox/blob/master/CONTRIBUTING.md).

## ⭐️ Support

Give a ⭐️  if this project helped you!

## License

[The MIT License](LICENSE)
