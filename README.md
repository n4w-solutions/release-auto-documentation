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
    server_address: ${{ secrets.GEN_RELEASE_SMTP_HOST }}
    server_port: ${{ secrets.GEN_RELEASE_SMTP_PORT }}
    username: ${{ secrets.GEN_RELEASE_SMTP_USER }}
    password: ${{ secrets.GEN_RELEASE_SMTP_PASS }}
    subject: "🚀 Release ${{ github.event.release.tag_name }} publicada"
    to: ${{ vars.GEN_RELEASE_MAIL_TO }}
    from: GitHub Actions <${{ secrets.GEN_RELEASE_SMTP_USER }}>
    html_body: ${{ steps.html.outputs.result }}
```

------------------------------------------------------------------------

## 🔐 Configuração Necessária

No repositório, acesse:

    Settings → Secrets and variables → Actions

### 🔒 Secrets obrigatórios

  Nome                   | Descrição
  -----------------------|---------------
  GEN_RELEASE_SMTP_HOST  | Servidor SMTP
  GEN_RELEASE_SMTP_PORT  | Porta SMTP
  GEN_RELEASE_SMTP_USER  | Usuário SMTP
  GEN_RELEASE_SMTP_PASS  | Senha SMTP

### 🌎 Variables obrigatórias

  Nome                  | Descrição
  ----------------------|--------------------------------
  GEN_RELEASE_MAIL_TO   | Lista de e-mails destinatários

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
