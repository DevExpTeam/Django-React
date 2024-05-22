# Full Stack Django and React

**Get hands-on experience in full-stack web development with Python, React, and AWS**

## What is this book about?
Django developers often need to rely on front-end developers to build client-side solution for their web apps. By combining the capabilities of React with Django, this book creates a complete learning path to go from being a backend developer to a full stack developer in no time. This book will help you use React to build state-of-the-art UI layouts and Django to create an immaculate backend.

This book covers the following exciting features:
* Explore how things work differently under the hood in the frontend as well as backend
* Discover how to build an API with Django
* Start from scratch to build an intuitive user interface using React capabilities
* Dockerize and prepare projects for deployment
* Deploy API and UI on various platforms like AWS and Vercel

## Instructions and Navigations
All of the code is organized into folders. For example, Chapter03.

The code will look like the following:
```
from rest_framework import viewsets
from rest_framework import filters
class AbstractViewSet(viewsets.ModelViewSet):
  filter_backends = [filters.OrderingFilter]
  ordering_fields = ['updated', 'created']
  ordering = ['-updated']

```

**Following is what you need for this book:**
This book is for Django web developers who want to get started with full-stack development and learn a frontend framework that can be quickly bootstrapped with the backend to build full-stack applications. Familiarity to React and JavaScript would be an added advantage.

With the following software and hardware list you can run all code files present in the book (Chapter 1-16).

### Software and Hardware List
| Chapter | Software/Hardware required | OS required |
| -------- | ------------------------------------ | ----------------------------------- |
| 1-16 | Python | Windows, Mac OS X, and Linux |
| 1-16 | JavaScript  | Windows, Mac OS X, and Linux |
| 1-16 | PostgreSQL  | Windows, Mac OS X, and Linux |
| 1-16 | Django  | Windows, Mac OS X, and Linux |
| 1-16 | React  | Windows, Mac OS X, and Linux |
| 1-16 | Docker | Windows, Mac OS X, and Linux |

We also provide a PDF file that has color images of the screenshots/diagrams used in this book. [Click here to download it](https://packt.link/jdEHp).

## Issue - Initial User Migration Failed with Admin.0001 Dependency
After creating the `UserManager` and `User` models, if the migration fails with the following error:<br>
`Migration admin.0001_initial is applied before its dependency core_user.0001_initial on database 'default'.`

Please try running these commands:<br> 
`$ sudo su postgres`<br>
`$  psql`<br>
`postgres=# DROP DATABASE coredb;`<br>
`postgres=# CREATE DATABASE coredb;`<br>
`postgres=# ALTER ROLE core SET client_encoding TO 'utf8';`<br>
`postgres=# ALTER ROLE core SET default_transaction_isolation TO 'read committed';`<br>
`postgres=# ALTER ROLE core SET timezone TO 'UTC';`<br>
`postgres=# ALTER DATABASE coredb OWNER TO core;`<br>
`postgres=# GRANT ALL PRIVILEGES ON DATABASE coredb TO core;`<br>

If you already  ran the "makemigrations" for core_user, simply  run `python manage.py migrate`


## Errata
* Page 81 (line 19): 
```
post = serializers.SlugRelatedField(queryset=Post.objects.all(), slug_field='public_id')

  def to_representation(self, instance):
        rep = super().to_representation(instance)
        
```
_should be_
```
post = serializers.SlugRelatedField(queryset=Post.objects.all(), slug_field='public_id')

        def validate_author(self, value):
          if self.context["request"].user != value:
            raise ValidationError("You can't create a post for another user.")
        return value
        
        def to_representation(self, instance):
          rep = super().to_representation(instance)
```

