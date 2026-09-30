# Desafio DevSecOps — Gerenciador de Tarefas

## Sobre o Projeto
Este repositório faz parte do desafio prático do módulo de DevSecOps da ADA Tech.
Você receberá este projeto com vulnerabilidades propositais e uma pipeline incompleta.
Seu objetivo é **implementar a pipeline de segurança** e **corrigir as vulnerabilidades**.

## Estado atual
A pipeline está **completa**, com os steps de segurança implementados e o deploy automatizado configurado.

## Sua missão
1. Implementar os steps de segurança no `pipeline.yml`
2. Fazer a pipeline **quebrar** ao detectar os problemas
3. Corrigir as vulnerabilidades encontradas
4. Fazer a pipeline **passar** com tudo verde ✅
5. Documentar o funcionamento da pipeline neste README

## O que implementar
- [x ] Secrets Scanning com **Gitleaks**
- [x] SAST com **Semgrep**
- [x] SCA com **Grype**
- [x] Assinatura do artefato com cosign
- [x] Deploy com **GitHub Pages**

## Como a pipeline funciona
A pipeline DevSecOps funciona como uma sequência automática de etapas que o código precisa passar antes de chegar à produção. Quando uma alteração é enviada para o repositório, o GitHub Actions executa essas etapas e verifica se o projeto está seguro para ser publicado.

### Step 1 — Checkout do código
Essa etapa baixa o código do repositório para o ambiente onde a pipeline será executada.

Ela é necessária porque as próximas etapas precisam ter acesso aos arquivos do projeto para realizar as verificações.

### Step 2 — Build
O build prepara o projeto e os arquivos necessários para as próximas etapas da pipeline.

Essa etapa é importante para garantir que o projeto esteja preparado corretamente antes das verificações de segurança e do deploy.

### Step 3 — Secrets Scanning com Gitleaks
O Gitleaks verifica se existem informações sensíveis expostas no código, como senhas, tokens e chaves de API.

Essa ferramenta é importante porque segredos publicados no código podem ser utilizados por pessoas não autorizadas. Se o Gitleaks encontrar um segredo exposto, a pipeline é interrompida.

### Step 4 — SAST com Semgrep
O Semgrep faz uma análise estática do código para procurar padrões inseguros e possíveis vulnerabilidades.

Essa ferramenta é importante porque permite encontrar problemas de segurança no próprio código antes que a aplicação seja publicada em produção. Se uma vulnerabilidade for detectada, ela deve ser corrigida antes de continuar.

### Step 5 — SCA com Grype
O Grype analisa as dependências utilizadas pelo projeto e verifica se existem vulnerabilidades conhecidas.

Essa ferramenta é importante porque uma aplicação também pode ficar vulnerável por utilizar bibliotecas ou dependências com falhas de segurança. A pipeline foi configurada para interromper o processo caso sejam encontradas vulnerabilidades de severidade média ou superior.

### Step 6 — Preparação e assinatura do artefato
Depois que as verificações de segurança são aprovadas, os arquivos da aplicação são preparados para publicação. A pipeline também gera um hash SHA-256 e utiliza o Cosign para a assinatura do artefato.

Essa etapa é importante para ajudar a garantir a integridade do artefato que será utilizado no deploy.

### Step 7 — Verificação e Deploy
Antes da publicação, o artefato é verificado. Depois disso, a aplicação é publicada automaticamente no GitHub Pages.

O deploy só acontece se todas as etapas anteriores forem concluídas com sucesso. Se alguma verificação de segurança falhar, a pipeline é interrompida e a aplicação não chega à produção. Esse processo é conhecido como **break the build**.


## URL de Produção
https://lupassos79.github.io/projeto-devsecop-desafio/