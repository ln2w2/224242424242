# INSTRUÇÕES DEFINITIVAS DE DEPLOY

Este arquivo ZIP contém a versão final e corrigida do seu projeto, pronta para ser implantada em qualquer plataforma de hospedagem.

## 1. Passos Iniciais

1.  **Baixe o arquivo `portfolio-final-definitivo.zip`**.
2.  **Extraia o conteúdo** em uma pasta no seu computador.
3.  **Crie um NOVO repositório** no GitHub.
4.  **Suba TODOS os arquivos** dessa pasta para o novo repositório.

## 2. Deploy no Render (Recomendado)

O Render é a melhor opção para este projeto, pois suporta o servidor Node.js e o banco de dados SQLite.

### A. Configuração do Serviço

1.  Crie um novo **Web Service** no Render e conecte-o ao seu novo repositório.
2.  Vá para as **`Environment Variables`** (Variáveis de Ambiente).
    *   **Key:** `NIXPACKS_PKGMGR`
    *   **Value:** `pnpm`
3.  Vá para **`Settings`** (Configurações).
    *   **Build Command:** `pnpm install && pnpm build`
    *   **Start Command:** `pnpm start`

### B. Configuração de Persistência (CRUCIAL para o Contador)

1.  No Render, vá para a seção **`Disks`** (Discos).
2.  Crie um novo disco (Persistent Disk).
    *   **Name:** `sqlite-data` (ou qualquer nome)
    *   **Mount Path:** `/opt/render/project/src/dist`
    *   Isso garante que o arquivo `visitors.db` (que está em `dist/visitors.db`) seja salvo permanentemente.

## 3. Deploy no Railway

O Railway também é uma ótima opção.

1.  Crie um novo projeto e conecte-o ao seu novo repositório.
2.  Vá para a aba **`Settings`**.
    *   **Build Command:** `pnpm install && pnpm build`
    *   **Start Command:** `pnpm start`
3.  Vá para a seção **`Volumes`** (Persistência).
    *   Crie um volume persistente com o **Path:** `/app/dist`

## 4. Deploy no Netlify (Apenas Frontend)

Se você usar o Netlify, o contador **NÃO VAI FUNCIONAR**.

1.  **Build Command:** `pnpm install && pnpm run build`
2.  **Publish Directory:** `dist/public`

---

**Se você seguir as instruções do Render ou Railway, seu site estará online com o contador funcionando corretamente!**
