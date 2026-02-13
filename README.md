# 📦 Release Auto Documentation

Automatize a geração e envio de documentação de release diretamente pelo
**GitHub**, utilizando **GitHub Actions** para capturar informações da
release, gerar HTML formatado e enviar por e-mail automaticamente.

Repositório:\
https://github.com/n4w-solutions/release-auto-documentation

------------------------------------------------------------------------

## 🚀 Objetivo

Este projeto automatiza o processo de:

-   📌 Capturar dados da Release publicada
-   📝 Gerar documentação em HTML
-   📧 Enviar e-mail automático com notas de versão
-   🔄 Padronizar comunicação de deploy

Ideal para times que desejam:

-   Governança de versões
-   Comunicação automática com stakeholders
-   Rastreabilidade de mudanças
-   Padronização enterprise de release notes

------------------------------------------------------------------------

## ⚙️ Como Funciona

1.  Uma **Release** é publicada no repositório.
2.  O workflow do GitHub Actions é acionado.
3.  O sistema:
    -   Lê o `tag_name`
    -   Captura o corpo da release
    -   Gera HTML estruturado
    -   Envia e-mail via SMTP

------------------------------------------------------------------------

## 🧩 Estrutura do Workflow

Exemplo simplificado do envio de e-mail:

``` yaml
- name: Send email with release notes
  uses: dawidd6/action-send-mail@v3
  with:
    server_address: ${{ env.SMTP_HOST }}
    server_port: ${{ env.SMTP_PORT }}
    username: ${{ env.SMTP_USER }}
    password: ${{ env.SMTP_PASS }}
    subject: "🚀 Release ${{ github.event.release.tag_name }} publicada"
    to: ${{ env.MAIL_TO }}
    from: GitHub Actions <${{ env.SMTP_USER }}>
    html_body: ${{ steps.html.outputs.result }}
```

------------------------------------------------------------------------

## 📧 Envio de E-mails com SMTP do Google (App Password)

Para utilizar o SMTP do Google com autenticação segura, é necessário gerar uma **Senha de App (App Password)**.  
Essa senha substitui sua senha principal e é obrigatória quando a conta possui **Verificação em Duas Etapas (2FA)** ativada.

---

### ✅ Pré-requisitos

Antes de começar, confirme que:

- ✔️ Sua conta Google possui **Verificação em duas etapas (2FA)** ativada
- ✔️ Você tem acesso ao painel de segurança da conta
- ✔️ O envio será feito via SMTP autenticado

---

### 🔐 Passo-a-passo para gerar a Senha de App

1. Acesse sua conta Google em  
   👉 https://myaccount.google.com/

2. No menu lateral, clique em **Segurança**

3. Ative a **Verificação em duas etapas**, caso ainda não esteja ativa

4. Após ativar o 2FA, acesse a opção  
   👉 **Senhas de app**  
   Link direto: https://myaccount.google.com/apppasswords

5. Em **Selecionar app**, escolha:
   - 📧 **E-mail**

6. Em **Selecionar dispositivo**, escolha:
   - 💻 **Outro (nome personalizado)**  
   - Informe um nome como: `Sistema Backend`, `API SMTP`, `App Produção`, etc.

7. Clique em **Gerar**

8. O Google exibirá uma senha no formato:

---

## 🔐 Configuração Necessária

No repositório, acesse:

    Settings → Secrets and variables → Actions

### 🔒 Secrets obrigatórios

  Nome                   | Descrição
  -----------------------|---------------
  AUTO_RELEASE_SMTP_HOST | Servidor SMTP
  AUTO_RELEASE_SMTP_PORT | Porta SMTP
  AUTO_RELEASE_SMTP_USER | Usuário SMTP
  AUTO_RELEASE_SMTP_PASS | Senha SMTP

### 🌎 Variables obrigatórias

  Nome                  | Descrição
  ----------------------|------------------------------------------------
  AUTO_RELEASE_MAIL_TO  | Lista de e-mails destinatários
  ENVIRONMENT           | Ambiente que a aplicação está sendo executada

------------------------------------------------------------------------

## 📧 Exemplo de E-mail Gerado

-   Assunto:

        🚀 Release v1.2.0 publicada

-   Corpo:

    -   Versão
    -   Data
    -   Autor
    -   Notas da Release
    -   Link direto para o GitHub

------------------------------------------------------------------------

## 🏗️ Arquitetura Recomendada

Para ambientes corporativos:

-   Utilize **Environments** no GitHub
-   Separe:
    -   staging
    -   production
-   Configure approval manual para production
-   Centralize SMTP via domínio corporativo

------------------------------------------------------------------------

## 🛠️ Personalização

Você pode facilmente:

-   Alterar layout HTML
-   Incluir changelog automático via API
-   Adicionar geração de PDF
-   Integrar com:
    -   Slack
    -   Microsoft Teams
    -   Jira
    -   Freshdesk

------------------------------------------------------------------------

## 🧪 Como Testar

1.  Crie uma nova tag:

    ``` bash
    git tag v1.0.1
    git push origin v1.0.1
    ```

2.  Publique a release no GitHub.

3.  O workflow será disparado automaticamente.

------------------------------------------------------------------------

## 📈 Benefícios

-   Elimina envio manual de release notes
-   Reduz erro humano
-   Padroniza comunicação
-   Melhora governança de deploy
-   Histórico auditável

------------------------------------------------------------------------

## 🔄 Roadmap (Sugestão)

-   [ ] Template dinâmico configurável
-   [ ] Multi-destinatários por ambiente
-   [ ] Geração automática de changelog por commit
-   [ ] Integração com Jira
-   [ ] Webhook externo

------------------------------------------------------------------------

## 👨‍💻 Autor

Desenvolvido por **N4W Solutions**

Especialistas em:

-   Arquitetura Web
-   Automação DevOps
-   Governança de Dados
-   Integrações Enterprise

------------------------------------------------------------------------

## 📄 Licença

Este projeto pode ser adaptado para uso interno corporativo.
