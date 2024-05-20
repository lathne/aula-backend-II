# Ambiente Python para desenvolvimento introdução ao django 

1. ________________________________________________________________
"vvvv cria a imagem docker vvvv"

```
docker-compose up -d --build
```
A partir de agora todos os comandos que vamos utilizar são executados a partir do docker

2. ________________________________________________________________
Abrir no vs code a extensão do docker, um ícone que fica do lado esquerdo
Clicar com o botão direito no '> aula-4-dev-backend' e clicar no Atach Shell. Isso vai abrir o terminal do docker onde vamos rodar os comandos. Dessa forma acessamos o ambiente ja configurado com as versões do python e pip corretas (*pip é o gerenciador de pacotes do python*).
Nesse terminal, ao rodar o ls, vão aparecer diversas paginas diferentes
nesse local vamos acessar a pasta src 
```
cd src
```
ao rodar o ls, vai aparecer o arquivo desafios.txt

3. ________________________________________________________________
Criando o vEnv - módulo que suporta a criação de "ambientes virtuais" leves para o python. cada um com seu conjunto independente de pacotes
python.

```
mkdir django-produtos
```

```
cd django-produtos
```

"vvvv crie um ambiente individualizado de python chamado venv e coloca todas as dependencias desse ambiente em uma pasta chamada venv vvvv"

```
python -m venv ./venv
```
após executar ele vai criar diversas pastas no local

rodar comando para ativar o ambiente virtual

```
source venv/bin/activate
```
 ==tive um erro ao rodar esse comando: 'source not found'. A solução foi matar o terminal > clicar novamente em Atach Shell > dar o comando /bin/bash > depois entrar na pasta src novamente e repetir os passos==

```
# /bin/bash
root@64c6e9d05233:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  src  srv  sys  tmp  usr  var
root@64c6e9d05233:/# cd src
root@64c6e9d05233:/src# ls
desafios.txt  django-produtos
root@64c6e9d05233:/src# cd django-produtos
root@64c6e9d05233:/src/django-produtos# ls
venv
root@64c6e9d05233:/src/django-produtos# python -m venv ./venv
```

após a execução correta o terminal fica assim

```
# /bin/bash
root@64c6e9d05233:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  src  srv  sys  tmp  usr  var
root@64c6e9d05233:/# cd src
root@64c6e9d05233:/src# ls
desafios.txt  django-produtos
root@64c6e9d05233:/src# cd django-produtos
root@64c6e9d05233:/src/django-produtos# ls
venv
root@64c6e9d05233:/src/django-produtos# python -m venv ./venv
root@64c6e9d05233:/src/django-produtos# source venv/bin/activate
(venv) root@64c6e9d05233:/src/django-produtos#
```

para desativar a venv >```deactivate``` 
para reativar > ```source venv/bin/activate ```

```
(venv) root@64c6e9d05233:/src/django-produtos# deactivate
root@64c6e9d05233:/src/django-produtos# source venv/bin/activate
(venv) root@64c6e9d05233:/src/django-produtos# 
```



Com o ambiente virtualizado/ configurado, o que preciso agora é instalar o django com o comando

```
 pip install django
```

```
(venv) root@64c6e9d05233:/src/django-produtos# pip --version
pip 24.0 from /src/django-produtos/venv/lib/python3.12/site-packages/pip (python 3.12)
(venv) root@64c6e9d05233:/src/django-produtos# pip install django
Collecting django
  Downloading Django-5.0.6-py3-none-any.whl.metadata (4.1 kB)
Collecting asgiref<4,>=3.7.0 (from django)
  Downloading asgiref-3.8.1-py3-none-any.whl.metadata (9.3 kB)
Collecting sqlparse>=0.3.1 (from django)
  Downloading sqlparse-0.5.0-py3-none-any.whl.metadata (3.9 kB)
Downloading Django-5.0.6-py3-none-any.whl (8.2 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 8.2/8.2 MB 4.2 MB/s eta 0:00:00
Downloading asgiref-3.8.1-py3-none-any.whl (23 kB)
Downloading sqlparse-0.5.0-py3-none-any.whl (43 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 44.0/44.0 kB 669.8 kB/s eta 0:00:00
Installing collected packages: sqlparse, asgiref, django
Successfully installed asgiref-3.8.1 django-5.0.6 sqlparse-0.5.0
```

4. ________________________________________________________________

```
pip freeze

(venv) root@64c6e9d05233:/src/django-produtos# pip freeze
asgiref==3.8.1
Django==5.0.6
sqlparse==0.5.0
(venv) root@64c6e9d05233:/src/django-produtos# 
```
^ vai listar todas as dependencias

```
pip freeze > requirements.txt
```
^ cria o arquivo com a listagem de requirements do ambiente

esse comando é util quando ja tenho um projeto em andamento e preciso verificar e instalar as dependencias do projeto, nesses casos devo rodar o ``` pip install -r requirements.txt```. Esse comando vai carregar todas as configurações necessarias para meu projeto

5. ________________________________________________________________

o que foi feito até agora > inicializado o sistema com o docker e o ambiente virtual com todas as dependecias isoladas do projeto django dentro de um ambiente virtual

A partir de agora vamos criar um projeto django

```
django-admin startproject setup .
```
^cria uma nova pasta chamada setup com diversos arquivos de configuração do projeto

a partir de agora tudo que vamos fazer no django vamos pedir para o arquivo manage.py ``` python manage.py runserver 0.0.0.0:8000 ```. O comando anterior var gerar um erro. Pois o host não é valido até adicionarmos 
 adiciondo o 0.0.0.0 na linha de código dessa forma > ```ALLOWED_HOSTS = ['0.0.0.0']  ```

================================================================

==esse comando deveria carregar o servidor django após a configuração do settings.py. Para mim, mesmo com o ajuste não carregou o host, pois quando abro o browser tem o erro de pagina invalida, solução foi deixar o ```ALLOWED_HOSTS = ['*'] ``` e entrar manualmente no browser com a URL http://localhost:8000/

================================================================

6. ________________________________________________________________

Modificações apos a inicialização do projeto django:

Modificar o settings.py linha 108 para trazer o horario local.

as ``` TIME_ZONE = 'UTC' ``` to be ``` TIME_ZONE = 'America/Sao_Paulo' ```

Modificar o settings.py linha 106 para trazer as mensagens do server django em portugues.

as ``` LANGUAGE_CODE = 'en-us' ``` to be ``` LANGUAGE_CODE = 'pt-br' ```

Em seguida entrar com o seguinte comando

```python manage.py startapp produto```

^ vai criar uma nova pasta 'produto' 

Na pasta produto, aquivo *models.py* criar o modelo abaixo da linha 3

``` 
# Create your models here.
class Produto(models.Model):

    name = models.CharField(max_lenght=100)
    description = models.TextField()
    price = models.DecimalField(max_digits=10,decimal_places=2)
    category = models.CharField(max_lenght=100)
```

No terminal, rodar o seguinte codigo para 'fazer uma estrutura das migrações pro banco de dados'

```python manage.py makemigrations```


================================================================

==
esse comando deveria fazer as migrações e criar o modelo do 'Produto' mas para mim não criou
```
(venv) root@64c6e9d05233:/src/django-produtos# python manage.py makemigrations
No changes detected 
```

solução???

==
================================================================

Com a estrutura do banco de dados montada executar o seguinte comando

```python manage.py migrate```

Com esse comando vão ser carregadas todas as migrações necessárias para um banco de dados com o django

Para visualizar todas essas informações, rodar novamente o comando:

``` python manage.py runserver 0.0.0.0:8000 ```

abrir o http://localhost:8000/ no browser para verificar se a aplicação está rodando

Após executado, no proprio browser incluir um /admin na url

*http://localhost:8000/admin*

Essa url leva para uma pagina de login para administração do django

Para criar um usuario capaz de fazer o login, paramos o servidor no terminal com um *ctrl c* e rodamos o comando

``` python manage.py createsuperuser ```

abre um input para o nome do usuario, endereço de email (pode deixar em branco), senha e repetir senha (pode deixar em branco... mas em projetos reais deve ser senha forte)

após o superuser criado com sucesso, iniciar novamente o servidor com o comando

``` python manage.py runserver 0.0.0.0:8000 ```

abrir o http://localhost:8000/admin no browser e entrar com o superuser criado. Deve entrar na pagina de admin do django.

Como nessa pagina precisamos visualizar os produtos criados no banco de dados retornamos ao vs code para registrar a aplicação de produtos.

Acessar a pasta produto arquivo admin.py e inserir o codigo

``` 
from django.contrib import admin
from produto.models import Produto


admin.site.register(Produto)
```

Após salvar e atualizar o browser, aparece na pagina a classe de produto. Clicando em adicionar, aparece um formulario onde é possível incluir novos produtos com as propriedades criadas no modelo models.py

Gerar produtos aleatorios

Ao criar esses produtos, o título deles na pagina ficam como:
Produto object (1)
Produto object (2)

Isso não pode acontecer para ficar mais facil de dar manutenção futuramente. Dessa forma voltamos ao vs code e alterando o modelo.

Após a criação da classe, criar função para renomear o titulo do produto ao ser criado no admin do django

```
    def __str__(self):
        return self.name
 ```

 Quando salvamos e atualizamos o browser na pagina de admin, os títulos dos produtos aparecem com o proprio nome do produto.

 Com isso finalizamos o desenvolvimento de um crud com o django.


 ## Desenvolvimento da API que lista esses produtos com fastAPI


[FastApi](https://fastapi.tiangolo.com/)


1. Sair da pasta do django com os comandos no terminal:*ls* + *mkdir fastapi-produtos* + *cd fastapi-produtos*
2. Desativar o ambiente virtual do django pelo terminal : *deactivate*
3. Dentro da pasta fastapi-produtos criar o ambiente  virtual do fastapi *python -m venv ./venv*
4. Ativar o v-env pelo terminal *source venv/bin/activate*
5. Instalação de duas bibliotecas pelo terminal: *pip fastapi uvicorn*. Uvicorn é um servidor que permite requisições assíncronas.
6. *pip freeze > requirements.txt* para criar o arquivo com a listagem de requirements do ambiente
7. criar um arquivo pelo terminal *touch app.py*  e começar a trabalhar nesse arquivo
8. 
```
from fastapi import FastApi

app = FastAPI()

#pega uma informação do endereço principal da aplicação.
@app.get('/')

```


Na aula desenvolvimento backend II parei em 02:42:30