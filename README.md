# NexChat — versão inicial para compilar

Interface mobile-first com tema escuro, Firebase Authentication e Firestore.

## O que funciona nesta versão
- Cadastro por e-mail/senha com verificação de e-mail.
- Login por e-mail/senha e Google.
- Perfil com @usuário único, nome, bio e avatar em emoji/cor.
- Busca por @usuário, solicitações de amizade, aceitar/recusar.
- Conversas privadas 1:1 em tempo real entre amigos.
- Edição de perfil, recuperação de senha e logout.
- Interface responsiva para celular e desktop.

## Ainda não está ativo
Comunidades/canais, anexos, envio de imagens, chamadas de áudio/vídeo, notificações push e presença online. A tela Comunidades deixa isso explícito. Isso é intencional: primeiro é importante testar as regras de segurança e o fluxo de chat.

## Requisitos do Firebase
Projeto configurado no código: `nexchat-58d82`.
1. Em Authentication > Sign-in method, habilite Email/Password e Google.
2. Em Authentication > Settings > Authorized domains, inclua o domínio onde o app vai rodar (ex.: domínio do GitHub Pages).
3. Publique `firestore.rules` e `firestore.indexes.json` no projeto correto.
4. O cadastro exige verificação de e-mail, conforme as regras.
5. A Realtime Database não é usada por esta versão. O arquivo `database.rules.json` incluído remove o caminho de chamadas que tinha permissões amplas; só publique depois de revisar/testar no Emulator Suite.

## Testar como site
Por ser um módulo JavaScript, não abra `index.html` por `file://`. Hospede em HTTPS (GitHub Pages, por exemplo) ou use um servidor local.
No GitHub Pages: envie o conteúdo de `www/` para a raiz do repositório/site e confirme o domínio autorizado no Firebase.

## Preparar projeto Android com Capacitor
É necessário Node.js/npm em um computador ou ambiente de build. O pacote inclui os arquivos básicos para iniciar:
```bash
npm install
npm run android:add
npm run android:sync
npm run android:open
```
Esses comandos exigem Android Studio para abrir/compilar localmente. Para compilar só pelo celular, será preciso usar um serviço de build compatível ou GitHub Actions; não coloque senhas nem arquivos de service account no repositório.

## Importante
- `apiKey` no Firebase Web config identifica o projeto e não é uma senha de administrador. A segurança depende das regras publicadas.
- Não publique regras sem testes. As regras originais foram fornecidas pelo usuário e precisam ser executadas no Firebase Emulator antes de confiar nelas.
- Não foi feita implantação no Firebase nem compilação de APK nesta etapa.

## Compilar o APK pelo GitHub (sem Android Studio no celular)
O repositório inclui `.github/workflows/build-apk.yml`. Depois de enviar TODO o conteúdo do ZIP a um repositório GitHub:
1. Abra o repositório e entre em **Settings > Actions > General**. Confirme que Actions está habilitado.
2. Na aba **Actions**, selecione **Build NexChat APK** e toque em **Run workflow** (ou envie um commit na branch `main`).
3. Espere o trabalho terminar com marca verde.
4. Abra a execução concluída; na seção **Artifacts**, baixe `NexChat-debug-apk`.
5. Extraia o ZIP baixado e instale `app-debug.apk` no Android. Se o Android pedir, autorize a instalação para o navegador/gerenciador de arquivos usado.

Esse é um APK de depuração para teste, não uma versão assinada para publicação na Play Store. O build em nuvem pode falhar se as dependências ou a configuração do projeto precisarem de ajustes; abra os logs da execução para ver o erro.
