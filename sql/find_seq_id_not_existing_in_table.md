```
select id+1 from users_user where (id+1) not in (select id from users_user);
```

이런 방법이,,,