# Pipeline CI/CD

## 
Boa noite seres humanos dessa realidade distopica e pandemica
hoje vamos falar o que é Continuous Integration (CI) e Continuous Deployment (CD). Ou Integração contínua ou Entrega Continua

Essas tecnicas aplicam o monitoramento e automação de uma parte do ciclo de vida de um software, juntas, essas práticas são chamadas de “pipeline de CI/CD”.


##
O que é Integração contínua ?

nada mais é do que automações na nossa pipeline, da nossa linha de produção de software 

É  um conjunto de práticas que leva a nossa equipe a implementar pequenas mudanças e fazer check-in do código toda vez que for dado um push pro repositorio

Por exemplo: Sempre ao gerar um Pull Request (PR) para um determinado
branch, vai rodar diversas rotinas para validar as mudanças, linting, testes unitários, testes de integração, teste de regressão, teste de componentes. 


##
Entrega contínua

Ou Continuous Deployment, Delivery é um mecanismo que nos ajudam a fazer entregas contínuas, essas duas técnicas vem dos princípios ágil e do manifesto ágil, para quem não conhece eu indico muito essa leitura.

O CD automatiza a entrega de aplicativos para diversos ambientes. Com bem sabemos, a maioria das equipes trabalha com vários ambientes diferentes de produção, como ambientes de desenvolvimento e teste, e o CD garante que haja uma maneira automatizada de enviar as nossas releases a esses ambientes.


##

(TDD) Desenvolvimento Orientado a Testes 

Test Driven Development (TDD), ou Test-first development, é um conjunto de técnicas orientado a testes associadas com Extreme Programming (XP) e metodologia ágil. Com TDD temos um desenvolvimento incremental do código, iniciado pelos testes (Miller,2004).


## 
o que é TDD?
Resumindo, 
Escreva os testes primeiro! 

Escreva testes para testar sua feature.
Execute testes (somente os novos testes podem falhar).
Escreva seu código para implementar o recurso.
Execute os testes (repita os passos 3 e 4 até passarem todos os testes).
Refatore o código (se necessário).

##
Porque devemos considerar o uso de CI/CD

##

1. Isolamentos de falhas

Conseguimos garantir mais velocidade em encontrar
e isolar o problema antes que ele possa causar mais queda de cabelo


##

2. Mais confiabilidade do teste

Mais confiabilidade pois estam os usando teste unitarios que ira cobrir parte dos cenários de testes da aplicação.

##

3. Menor lista de pendências

Menos bugs e logo menos defeitos não críticos em nosso backlog. 
Pois conseguimos encontrar esses pequenos defeitos antes de serem liberados para os usuarios finais.


##

4. Reduzir custos

Maior qualidade nas entregas, com menor indice de erro e retrabalho.


##
Show me de code

Para facilitar e agilizar eu criei uma app em django e disponibilizei ela no meu github

python3 manage.py startapp question


# organização dos testes unitários no Django

A estrutura em árvore do projeto criado é semelhante à seguinte.

 
├── manage.py
├── core
└── question
   ├── migrations
   ├── admin.py
   ├── apps.py
   ├── models.py
   ├── tests.py
   └── views.py


O diretório ‘core’ é onde está o projeto Django e já o diretório ‘question’ onde encontra se a nossa aplicação que vamos trabalhar.

Geralmente os testes de cada aplicação devem estar dentro do arquivo question/teste.py, não existe problema em colocar os seus testes aqui.
Entretanto dentro de uma aplicação podemos realizar vários tipos de testes, como por exemplo, testes unitários para models, views e formulários.

Para organiuzarmpos nossos testes unitarios todos deste models ira ficar confuso, confoirme o projeto cresce aumenta o nivel de complexidade. Pensando nisso eu realizei uma pesquisa e atravez de outras expeiencias de projetos eu cheguei na seguinte estrutura


├── manage.py
├── core
└── question
   ├── migrations
   ├── admin.py
   ├── apps.py
   ├── models.py
   ├── tests
       └── unittest
        ├── tests_models.py
        ├── tests_views.py
           └── tests_forms.py
   └── views.py
 

Como nossa aplicação pode ter vários tipos de testes, como unitários, integração, eu sugiro criar um diretório para cada tipo de testes e posteriormente dividir as rotinas com as suas respectivas responsabilidades.

Essa estrutura é sugerida para cada aplicação, caso tenhamos 10 aplicações no projeto devemos seguir essa estrutura. Obviamente não é uma regra e sim apenas uma sugestão de padronização e organização.

# vamos agora criar o nosso arquivo __init__.py

2 -  Criando nossos testes

Antes de criar os nossos testes devemos iniciar criando nossos modelos, abaixo segue o exemplo criado para o nosso caso de estudo:

from django.db import models
 
class Question(models.Model):
   name = models.CharField('Name', max_length=100)
   amount = models.PositiveIntegerField('Amount')
 
   def __str__(self):
       return self.name
 
 
Com o modelo criado devemos criar nossas migrations:

python3 manage.py makemigrations
python3 manage.py migrate


Enfim vamos criar nosso primeiro teste, dentro do arquivo question/tests/tests_models.py

vamos criar a seguinte classe:


from django.test import TestCase
from ..models import Question
    
class QuestionTestCase(TestCase):
    def setUp(self):
        Question.objects.create(
            name="You are you?",
            amount=12
        )
    
    def test_return_str(self):
        q = Question.objects.get(name="You are you?")
        self.assertEquals(q.__str__(), "You are you?")


Agora vamos no terminal e vamos rodar os testes da nossa aplicação question:

python3 manage.py test question


# CI com Django usando Github Actions

Agora vamos no github para criar a nossa pipeline.
Primeiro acesse o repositório do github onde esta o seu projeto e depois acesse a aba actions

Agora selecione a opção “Python application” e vamos realizar o setup do nosso workflow

git init
git flow init
git config user.name "f0rmig4"
git config user.email f0rmig4@protonmail.com

git flow feature start requirement 
touch requirements.txt
echo "django" >> requirements.txt

Vamos agora dar um push na nossa branch e criar um PR no github

git add requirements.txt
git commit -m 'Create requirements' .
git push origin feature/requirement
