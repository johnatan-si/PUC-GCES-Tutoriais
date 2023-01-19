# Tutorial GitLab-CI

## 1. Como funciona?

O [GitLab-CI](https://docs.gitlab.com/ee/ci/) é uma ferramenta de Integração Contínua (CI) e Entrega/Deploy Contínuo (CD) utilizada nos repositórios hospedados no GitLab. 

Ele funciona através de [_runners_](https://docs.gitlab.com/ee/ci/runners/index.html), que são processos que acessam e executam o seu _pipeline_ de CI/CD. O GitLab já disponibiliza _runners_ públicos, mas se desejar é possível especificar os seus proprios _runners_ (como por exemplo na sua máquina ou em uma _cloud_ específica).

Você também pode utilizar o GitLab-CI mesmo tendo o reposítorio hospedado no GitHub. Para isto é necessário somente espelhar os repositórios. É possível encontrar as informações necessárias e os passos nesse [guia](https://docs.gitlab.com/ee/ci/ci_cd_for_external_repos/github_integration.html).

Para configurar e definir o seu _pipeline_ de CI/CD, você tem que criar um arquivo na raiz com o nome `.gitlab-ci.yml`, o funcionamento do yaml será explicado no próximo tópico. Obs.: é possível utilizar outro nome, mas para isso é necessário alterar as configurações do repositório.

## 2. O YAML

O YAML (ou YML) é uma linguagem de serialização de dados [[1]](https://circleci.com/blog/what-is-yaml-a-beginner-s-guide/?utm_medium=SEM&utm_source=gnb&utm_campaign=SEM-gnb-DSA-Eng-ni&utm_content=&utm_term=dynamicSearch-&gclid=Cj0KCQjwg7KJBhDyARIsAHrAXaF1Jr_TpoPt0du-qsfsvqVs7rOEXlF6_ogTI24eSx4uxWYcb0-M4b0aAuQIEALw_wcB) fortemente identada e utilizada, principalmente, para arquivos de configuração.

A estrutura básica de uma yml é um _map_:

``` yaml
key: value
```

Já para definir uma _collection_:

``` yaml
key: 
    - key: value
    - key: value
    - key: value
```

### 2.1 .gitlab-ci.yml

O GitLab-CI trabalha com _jobs_, ou seja, tarefas a serem executadas para garantir a integridade da versão. Um exemplo de _job_ pod ser para executar os testes unitários da versão.

O arquivo yaml de configuração do GitLab-CI, tem algumas `keys` [[2]](https://docs.gitlab.com/ee/ci/yaml/) já definidas para configurar as etapas do CI/CD. O GitLab disponibiliza alguns [exemplos](https://docs.gitlab.com/ee/ci/examples/index.html) como material de apoio, além do proprio [yml](https://gitlab.com/gitlab-org/gitlab/-/blob/master/.gitlab-ci.yml) utilizado no projeto do GitLab.

Algumas das `keys` mais utilizadas são:

- [before_script](#211-before_script)
- [after_script](#212-after_script)
- [coverage](#213-coverage)
- [image](#214-image)
- [rules](#215-rules)
- [script](#216-script)
- [stage](#217-stage)

Com essas `keys` você consegue configurar uma _pipeline_ completa. A seguir, iremos passar uma por uma.

#### 2.1.1 `before_script`

Essa key aceita uma _collection_ e é utilizada para rodar alguns comandos antes de cada _job_. Ela pode ser definida tanto dentro de cada _job_ como para todos os _jobs_.

Exemplos:

`before_script` para um _job_
``` yaml
job:
  before_script:
    - echo "Execute this command before any `script:` commands."
  script:
    - echo "This command executes after the job's `before_script` commands."
```

`before_script` para todos os _jobs_
```yaml
before_script:
  - echo "Execute this command before any `job`."

job1:
  ...
job2:
  ...
```

#### 2.1.2 `after_script`

Essa key aceita uma _collection_ e é utilizada para rodar alguns comandos depois de cada _job_. Ela pode ser definida tanto dentro de cada _job_ como para todos os _jobs_.

Exemplos:

`after_script` para um _job_
``` yaml
job:
  after_script:
    - echo "Execute this command after any `script:` commands."
  script:
    - echo "This command executes after the job's `after_script` commands."
```

`after_script` para todos os _jobs_
```yaml
after_script:
  - echo "Execute this command after any `job`."

job1:
  ...
job2:
  ...
```

#### 2.1.3 `coverage`

Essa key aceita um valor somente e é utilizada para definir como extrair a cobertura do código a partir da saída do _job_.

Exemplo:

``` yaml
job1:
  script: rspec
  coverage: '/Code coverage: \d+\.\d+/'
```

#### 2.1.4 `image`

Essa key aceita um valor somente e é utilizada para definir a imagem do docker. Ela pode ser definida tanto dentro de cada _job_ como para todos os _jobs_.

Exemplos:

`image` para todos os _jobs_
``` yaml
image: node:latest

job1:
  ...
job2:
  ...
```

`image` para um _job_
``` yaml
job1:
  image: node:latest
job2:
  image: docker:latest
```

#### 2.1.5 `rules`

Essa _key_ aceita uma _collection_ e é utilizada para definir as regras em que aquele _job_ irá executar ou não. [Mais informações dessa _key_](https://docs.gitlab.com/ee/ci/yaml/#rules).

Examplo:

```yaml
job:
  script: echo "Hello, Rules!"
  rules:
    - if: '$CI_MERGE_REQUEST_SOURCE_BRANCH_NAME =~ /^feature/'
      when: manual
      allow_failure: true
    - if: '$CI_PIPELINE_SOURCE == "merge_request_event"'
      changes:
        - Dockerfile
      when: manual
    - exists:
      - Dockerfile
```

#### 2.1.6 `script`

Essa key aceita uma _collection_ e é utilizada para definir os commandos que o _runner_ tem que executar.

Exemplo:

``` yaml
job1:
  script: "bundle exec rspec"

job2:
  script:
    - uname -a
    - bundle exec rspec
```

#### 2.1.7 `stage`

Essa key aceita uma _collection_ e é utilizada para definir os estágio da sua _pipeline_ e define também em qual estágio cada _job_ se encontra.

PS: Se um `stage` não for definido em um _job_, ele utiliza o `test` por padrão.

Exemplo:

``` yaml
stages:
  - build
  - test
  - deploy

job1:
  stage: build
  script:
    - echo "This job compiles code."

job2:
  stage: test
  script:
    - echo "This job tests the compiled code. It runs when the build stage completes."

job3:
  script:
    - echo "This job also runs in the test stage".

job4:
  stage: deploy
  script:
    - echo "This job deploys the code. It runs when the test stage completes."
```

## Outros Materiais

Principais:
  - [Documentação GitLab-CI](https://docs.gitlab.com/ee/ci/)
  - [Referências do .gitlab-ci.yml](https://docs.gitlab.com/ee/ci/yaml/)

Complementares:
- [DESCOMPLICANDO O YAML - APRENDA YAML DE UMA VEZ POR TODAS!](https://www.youtube.com/watch?v=JOtIVGy1SgE)
- [PRIMEIRA AULA PARA A CERTIFICAÇÃO OFICIAL DO GITLAB](https://www.youtube.com/watch?v=SMzaAP09BD4)

Alguns projeto de EPS/MDS que utilizaram o GitLab-CI:

- [2018.2-Lino](https://github.com/BotLino)
- [2019.1-Gaia](https://github.com/BotGaia)
- [2019.1-ADA](https://github.com/fga-eps-mds/2019.1-ADA)
