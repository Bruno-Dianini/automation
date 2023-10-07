
# Docker CI

Descrição curta do seu projeto.

## Visão Geral

Este repositório contém um pipeline de integração contínua (CI) configurado com o GitHub Actions para automatizar o processo de construção, teste e implantação de um aplicativo ou serviço. O pipeline consiste em vários "jobs" que são executados automaticamente em resposta a eventos específicos, como push para o branch principal ou pull requests.

## Jobs do Pipeline

O pipeline é composto por vários jobs, cada um com uma tarefa específica:

1. **Build e Publicação da Imagem de Teste**
   - Nome: `build-test-image`
   - Descrição: Este job constrói uma imagem Docker para fins de teste e a publica no GitHub Container Registry (ghcr.io). Ele utiliza as ações do Docker para configurar o ambiente de construção e fazer o push da imagem.

2. **Testes de Unidade em Docker**
   - Nome: `test-unit`
   - Descrição: Este job executa testes de unidade dentro de um contêiner Docker usando a imagem construída anteriormente. Ele usa a imagem publicada no GitHub Container Registry.

3. **Testes de Integração em Compose**
   - Nome: `test-integration`
   - Descrição: Este job realiza testes de integração usando Docker Compose. Ele verifica a integração de vários componentes do aplicativo em um ambiente Dockerizado.

4. **Teste de Implantação em Kubernetes (k3d)**
   - Nome: `test-k3d`
   - Descrição: Este job testa a implantação do aplicativo em um cluster Kubernetes local (k3d). Ele cria um cluster k3d, implanta o aplicativo e executa testes de saúde.

5. **Verificação de Vulnerabilidades de Imagem (Trivy)**
   - Nome: `scan-image`
   - Descrição: Este job verifica a imagem Docker criada em busca de vulnerabilidades de segurança usando Trivy. Ele puxa a imagem e executa a verificação.

6. **Construção da Imagem Final**
   - Nome: `build-final-image`
   - Descrição: Este é o último job no pipeline. Ele constrói a imagem final do aplicativo, que pode incluir correções de segurança após a verificação de vulnerabilidades. A imagem final é publicada no GitHub Container Registry e no Docker Hub.

## Dependências entre Jobs

Os jobs têm dependências configuradas usando a seção "needs". Isso garante que os jobs sejam executados em ordem e dependam do sucesso dos jobs anteriores.

## Permissões e Segurança

Cada job pode ter diferentes permissões, como permissões para ler ou gravar pacotes, conteúdo ou eventos de segurança. Essas permissões são configuradas para cada job, dependendo das ações que eles executam.

## Configuração

Todas as configurações do pipeline estão definidas no arquivo `.github/workflows/nome-do-arquivo.yml`. Você pode personalizar esse arquivo conforme necessário para atender aos requisitos específicos do seu projeto.

## Contribuição

Sinta-se à vontade para contribuir com melhorias ou correções para este pipeline. Abra um pull request e terei prazer em revisá-lo.
