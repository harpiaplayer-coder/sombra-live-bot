# Sombra - Avatar de IA para live no TikTok

Um personagem encapuzado (original) que le os comentarios da sua live, responde por voz
usando IA e reage de forma engracada quando alguem manda **rosas**.

## Como funciona

TikTok Live --> server.js (le chat e presentes) --> IA (Claude) escreve a resposta
--> pagina do avatar (voz + boca animada + chuva de rosas) --> voce captura na live.

## Requisitos

- Node.js 18 ou mais novo (https://nodejs.org)
- Chave da API da Anthropic (https://console.anthropic.com) para as respostas inteligentes
- Um computador para transmitir (TikTok LIVE Studio ou OBS)

## Instalacao

```bash
npm install
```

## Rodando

Windows (PowerShell):
```powershell
$env:TIKTOK_USER="seu_usuario"; $env:ANTHROPIC_API_KEY="sua_chave"; npm start
```

Mac / Linux:
```bash
TIKTOK_USER=seu_usuario ANTHROPIC_API_KEY=sua_chave npm start
```

1. Abra http://localhost:3000 no Chrome e clique em **Iniciar** (libera o audio).
2. Teste sem estar ao vivo: deixe `TIKTOK_USER` vazio, digite comentarios e clique em **Mandar Rosa**.
3. Quando for ao vivo, abra a pagina com `http://localhost:3000/?clean` (esconde os botoes de teste).
4. No TikTok LIVE Studio ou no OBS, adicione a janela do Chrome como fonte e transmita.
   Para o publico ouvir a voz, capture tambem o audio do computador.

## Personalizando

- **Personalidade / humor**: edite `SYSTEM_PROMPT` e `ROSE_PROMPT` no `server.js`.
- **Voz**: ajuste `u.pitch` e `u.rate` no `public/index.html`.
- **Visual**: o personagem e um SVG no `index.html`. Voce pode trocar pelo seu proprio desenho.
- **Modelo**: `MODEL=claude-sonnet-5-5` deixa as respostas mais espertas (um pouco mais lento).
  O padrao e `claude-haiku-5-5`, mais rapido.

## Observacoes importantes

- A leitura do chat usa a biblioteca nao oficial `tiktok-live-connector`. Ela pode quebrar se o TikTok
  mudar algo, e voce precisa estar **ao vivo** para conectar.
- A voz usa o sintetizador do navegador. A qualidade depende das vozes pt-BR do seu sistema
  (Chrome/Edge costumam ter boas opcoes).
- O bot ignora spam (1 resposta por pessoa a cada 8s) e trata comentarios como texto, nao como
  ordem. Mesmo assim, fique de olho nas regras da comunidade do TikTok.
- Presentes furam a fila: a reacao as rosas acontece logo, com chuva de rosas e voz derretida.
