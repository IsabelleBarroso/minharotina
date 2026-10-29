# Minha Rotina

App de rotina da Isabelle: rotina do dia, da semana e do mês, hábitos, água, estudos (com a trilha de Política), leitura, desenvolvimento pessoal e mercado. Funciona no celular e no computador, com o mesmo link e os mesmos dados.

- **Dados:** salvos no Firebase, no mesmo projeto dos outros apps (`isabelle-financas`), numa gaveta só do Minha Rotina. Os outros apps não são alterados.
- **Google Agenda:** o app cria uma agenda chamada "Minha Rotina" com os blocos da rotina, as revisões de estudo e os lembretes de água, com aviso antes de cada bloco.

## 1. Publicar no GitHub Pages

1. No GitHub, crie um repositório novo chamado **minharotina** (público).
2. Clique em **Add file → Upload files** e envie tudo desta pasta: `index.html`, `manifest.json`, `sw.js`, `README.md` e a pasta `icons`.
3. Vá em **Settings → Pages**, escolha a branch **main** e a pasta **/ (root)** e salve.
4. Em alguns minutos o app fica no ar em: **https://isabellebarroso.github.io/minharotina/**
5. No iPhone, abra o link no Safari, toque em **Compartilhar → Adicionar à Tela de Início**.

## 2. Ligar o Google Agenda (uma vez só)

Tudo é feito no projeto do Firebase que você já usa, no Google Cloud.

1. Abra **console.cloud.google.com** e, no topo, escolha o projeto **isabelle-financas**.
2. Vá em **APIs e serviços → Biblioteca**, procure **Google Calendar API** e clique em **Ativar**.
3. Vá em **Google Auth Platform** (ou "Tela de permissão OAuth"):
   - Tipo de público: **Externo**. Nome do app: **Minha Rotina**. Coloque o seu e-mail.
   - Em **Público → Usuários de teste**, adicione o seu Gmail.
   - O app fica em **modo de teste**, só para você. Não precisa publicar.
4. Vá em **Clientes** (ou "Credenciais") → **Criar cliente** → tipo **Aplicativo da Web**.
   - Em **Origens JavaScript autorizadas**, adicione: `https://isabellebarroso.github.io`
   - Clique em **Criar** e copie o **ID do cliente** (termina em `.apps.googleusercontent.com`).
5. No app, abra a aba **Google**, cole o ID no quadro **Configuração** e toque em **Salvar ID**.
6. Toque em **Entrar com Google**. O Google vai avisar que o app não foi verificado: toque em **Continuar** (é o seu próprio app).
7. O app cria a agenda **Minha Rotina** e envia a rotina. Pronto: os avisos chegam pelo Google Agenda.

## Como funciona a sincronização

- **Enviar rotina ao Google:** apaga os eventos antigos do app na agenda "Minha Rotina" e cria de novo, com os horários atuais e o aviso escolhido (padrão: 4 minutos antes).
- **Trazer mudanças do Google:** se você mudar o horário ou o nome de um bloco direto no Google Agenda, o app atualiza a rotina.
- **Revisões:** ao concluir um livro ou uma parte da trilha, o app marca revisões em 1, 3, 7 e 30 dias, às 7h20.
- **Hoje no Google Agenda:** a tela Hoje mostra os seus compromissos da agenda principal do dia.
- A permissão do Google dura cerca de 1 hora. Depois disso, ao tocar num botão do Google, ele pede para entrar de novo.

## Se algo der errado

- **"Falha ao salvar na nuvem":** as regras do Realtime Database precisam liberar o caminho `financas/minharotina-…` (o mesmo jeito dos outros apps).
- **Janela do Google não abre:** libere pop-ups para o site do app.
- **Erro de origem (origin_mismatch):** confira se a origem autorizada é exatamente `https://isabellebarroso.github.io`, sem barra no fim.

## Atualizar o app

A cada versão nova, troque o número em `sw.js` (`minharotina-v1.0` → `v1.1`) e envie os arquivos de novo pelo GitHub.
