# Reproduce [#33115](https://github.com/quarkusio/quarkus/issues/33115)

## 1. Start an artifact repository

Start a local "repository" which requires authorization. We simulate the behaviour of gitlab
or azure with a webserver only returning artifacts, when a  certain authorization header is present. See `nginx.conf` for details.


```
> docker-compose up -d
```

Artifacts are served from `repo`. Authorization configuration via header is configured in `settings.xml`

## 2. Verify everything works without quarkus

```
> mvnw install --settings settings.xml
```

## 3. Reproduce error with quarkus 3


```
> rm -rf ~/.m2/repository/example
> mvnw install --settings settings.xml -Pwith-quarkus3
```