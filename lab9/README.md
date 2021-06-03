# Отчет по лабораторной работе № 9

### Цель работы

Данная лабораторная работа посвещена изучению процесса создания артефактов на примере **Github Release**

### Задания

- [x] 1. Создать публичный репозиторий с названием **lab9timp** на сервисе **GitHub**
- [x] 2. Ознакомиться со ссылками учебного материала
- [x] 3. Получить токен для доступа к репозиториям сервиса **GitHub**
- [x] 4. Выполнить инструкцию учебного материала
- [x] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

### Выполненные команды

Результат см. в текущем репозитории

```sh
$ export GITHUB_TOKEN=<token>
```

```sh
$ git clone https://github.com/lozchkavarene/lab8 projects/lab9
$ cd timp/lab9
$ git remote remove origin
$ gh repo create
```

```sh
$ gpg --full-generate-key

	gpg (GnuPG) 2.2.27; Copyright (C) 2021 Free Software Foundation, Inc.
	This is free software: you are free to change and redistribute it.
	There is NO WARRANTY, to the extent permitted by law.
	
	Please select what kind of key you want:
	   (1) RSA and RSA (default)
    ...

$ gpg --list-secret-keys 

	/home/orm/.gnupg/pubring.kbx
	----------------------------
	sec   rsa4096/B0BC6E20E5BA714F 2021-05-06 [SC]
	      B1F<...>14F
	uid                 [ultimate] gpg_for_github (Nope) <lozchkavarene@gmail.ru>
	ssb   rsa4096/25B<...>5FD 2021-05-06 [E]

$ GPG_KEY_ID=$(gpg --list-secret-keys --keyid-format LONG | grep ssb | tail -1 | awk '{print $2}' | awk -F'/' '{print $2}')

$ GPG_SEC_KEY_ID=$(gpg --list-secret-keys --keyid-format LONG | grep sec | tail -1 | awk '{print $2}' | awk -F'/' '{print $2}')

$ gpg --armor --export ${GPG_KEY_ID}

# Добавление gpg ключа на github
$ open https://github.com/settings/keys 

$ git config user.signingkey ${GPG_SEC_KEY_ID}
$ git config gpg.program gpg
```

```sh
$ cmake -H. -B_build -DCPACK_GENERATOR="TGZ"
$ cmake --build _build --target package
```

```sh
'Подписанный git tag'
$ git tag -s v0.1.0.0
$ git tag -v v0.1.0.0
$ git show v0.1.0.0
$ git push origin master --tags
```

```sh
$ gh release create v0.1.0.1
	? Title (optional) Print_app
	? Release notes Write my own
	? Is this a prerelease? No
	? Submit? Publish release
	https://github.com/lozchkavarene/lab9/releases/tag/v0.1.0.1

$ gh release upload v0.1.0.1 ./build/cpack/*.tar.gz
    Successfully uploaded 1 asset to v0.1.0.1
```

```sh
$ wget https://github.com/lozchkavarene/lab9/releases/download/v0.1.0.1/print-0.1.0.0-Linux.tar.gz
$ tar -ztf solver-0.1.0.0-Linux.tar.gz
```

### Ссылки

- [Create Release](https://help.github.com/articles/creating-releases/)
- [Get GitHub Token](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)
- [Signing Commits](https://help.github.com/articles/signing-commits-with-gpg/)
- [Go Setup](http://www.golangbootcamp.com/book/get_setup)
- [github-release](https://github.com/aktau/github-release)
