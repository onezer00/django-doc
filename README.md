# Documentação Django
Repositório para documentar passo a passo de como configurar o django.

As ferramentas que utilizo para desenvolvimento estarão listadas abaixo:
- Windows 11 / Ubuntu 20.04
- Python 3.10.8
- Django 3.x
- Virtualenv
- Poetry
- Vscode

# Primeiros passos

## Criação do ambiente local para desenvolvimento

### Preparando ambiente com virtualenv

- Linux
```bash
# Certifique-se de que o python3 e o pip3 estão instalados
$ sudo apt-get install python3-pip
$ sudo pip3 install virtualenv
$ virtualenv -p python3 venv
$ source venv/bin/activate
```
- Windows
```bash	
# Certifique-se de que o python3 e o pip3 estão instalados
$ pip3 install virtualenv
$ virtualenv -p python3 venv
$ venv\Scripts\activate
```
### Preparando ambiente com poetry
```bash	
# Por praticidade irei seguir daqui para frente utilizando poetry, mas nada impede de você utilizar o virtualenv
# Certifique-se de que o python3 e o pip3 estão instalados
$ pip3 install poetry
$ poetry new nome_do_projeto
$ cd nome_do_projeto

# Agora já dentro da pasta do projeto no navegador, iniciaremos o Vscode
$ code .

# A fim de praticidade iremos configurar o Vscode para criar nossa virtualenv na pasta do projeto
# Para isso, abra o arquivo settings.json pressionando Ctrl + Shift + P e digite "settings.json".
# Dentro do arquivo settings.json, adicione a seguinte linha:
# "python.venvPath": "${workspaceFolder}/.venv"

# Agora já com o Vscode devidamente configurado, abra o terminal e execute o comando abaixo, isso fará que o Vscode crie a virtualenv e instale as dependências do projeto
$ poetry add django djangorestframework uritemplate PyYAML pytz sqlparse asgiref tzdata

```

### Criando projeto Django
```bash
# Como utilizamos o poetry apenas para gerar a estrutura base do projeto, agora iremos excluir a pasta do projeto e criar novamente utilizando o django-admin
$ rm -rf nome_do_projeto

# Dentro da pasta do projeto, execute o comando abaixo para criar o projeto Django
$ django-admin startproject nome_do_projeto .

# Para fins didáticos chamaremos nosso projeto de "core", mas você pode nomear como quiser.

# Neste ponto iremos passar as nossas dependências para um arquivo de configuração, para que possamos futuramente utilizar em outros ambientes
# E como temos o nosso Vscode configurado para criar a virtualenv na pasta do projeto, não precisamos nos preocupar com isso, basta se certificar que o ambiente virtual está ativado e executar o seguinte comando.
$ pip freeze > requirements.txt
```
### Executando o primeiro migrate e executando o servidor
```bash
# Antes de tudo iremos configurar o Vscode para que possamos executar o servidor em modo debug, isso será muito útil para o desenvolvimento.
# Para isso, no menu lateral esquerdo, clique em "Run and Debug", depois clique em "Create a launch.json file", selecione "Python: Django" e clique em "Create".
# Agora já com o arquivo de configuração criado, abra o arquivo e deixe-o como o exemplo abaixo:
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Django",
            "type": "python",
            "request": "launch",
            "program": "${workspaceFolder}\\manage.py",
            "args": [
                "runserver",
            ],
            "env": {
                "DJANGO_SETTINGS_MODULE": "core.settings"
            },
            "django": true,
            "justMyCode": true
        }
    ]
}

# Agora vamos fazer nossa primeira migração do banco de dados com o seguinte comando
$ python manage.py migrate

# E por fim, vamos executar o servidor, você pode executar de duas formas diferentes:
# 1 - Clicando no botão "Run and Debug" no menu lateral esquerdo do Vscode e selecionando a opção "Python: Django"
# 2 - Executando o comando abaixo no terminal do Vscode
$ python manage.py runserver --settings=core.settings

# Se tudo ocorreu bem, você verá uma mensagem parecida com a abaixo no terminal do Vscode
# Lembrando que ao executar da primeira forma o servidor será executado em modo debug, ou seja, você poderá fazer breakpoints e debugar o código. E que a variável do DJANGO_SETTINGS_MODULE já está configurada no arquivo de configuração do Vscode.
```

`Deixa o like e aguarde o próximo commit!`
