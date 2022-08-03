# django custom user table

1. database에 table을 생성한다.
2. 상황에 맞게 models.py 설정 ( python manage.py inspectdb ) 

> example models.py file 
```python
from django.db import models
from django.contrib.auth.models import (BaseUserManager, AbstractBaseUser)

class TbUserManager(BaseUserManager):
    def create_user(self, user_id, password=None):
        if not user_id:
            raise ValueError("Users must have an user_id address")

        user = self.model(
            user_id=user_id,
        )

        user.set_password(password)
        user.save(using=self._db)
        return user

    def create_superuser(self, user_id, password):
        user = self.create_user(
            user_id,
            password=password
        )
        user.is_admin = True
        user.save(using=self._db)
        return user


class TbUser(AbstractBaseUser):
    user_seq = models.AutoField(
        primary_key=True
    )
    user_id = models.CharField(unique=True, max_length=20, blank=True, null=True)
    password = models.CharField(max_length=500, blank=True, null=True)
    user_nm = models.CharField(max_length=500, blank=True, null=True)
    email = models.CharField(max_length=500, blank=True, null=True)
    phone = models.CharField(max_length=500, blank=True, null=True)
    user_type = models.CharField(max_length=20, blank=True, null=True)
    last_login_dts = models.DateTimeField(blank=True, null=True)
    connect_ip = models.CharField(max_length=20, blank=True, null=True)
    login_fail_cnt = models.PositiveIntegerField(blank=True, null=True)
    password_chg_dts = models.DateTimeField(blank=True, null=True)
    del_yn = models.CharField(max_length=1, blank=True, null=True)
    reg_dts = models.DateTimeField(blank=True, null=True)
    reg_user = models.PositiveIntegerField(blank=True, null=True)
    upd_dts = models.DateTimeField(blank=True, null=True)
    upd_user = models.PositiveIntegerField(blank=True, null=True)

    objects = TbUserManager()

    USERNAME_FIELD = "user_id"
    # REQUIRED_FIELDS = ['date_of_birth']

    class Meta:
        db_table = "tb_user"

    def __str__(self):
        return self.user_id

    def username(self):
        print('user_nm called', self.user_nm)
        return self.user_nm

    def has_perm(self, perm, obj=None):
        "Does the user have a specific permission?"
        # Simplest possible answer: Yes, always
        return True

    def has_module_perms(self, app_label):
        "Does the user have permissions to view the app `app_label`?"
        # Simplest possible answer: Yes, always
        return True
```

3. settings.py 에 custom model 지정
```python
AUTH_USER_MODEL = "member.TbUser"
```

4. migration file 생성

```bash
python manage.py makemigrations member ( app name )
```

> 그 외 Django migrate 관련 명령어

```bash
python manage.py showmigrations
python manage.py migrate member ( app name )
```

