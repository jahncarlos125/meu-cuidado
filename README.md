<p align="center"><img src="docs/icone.png" width="96" alt="Ícone do Meu Cuidado"></p>

<h1 align="center">Meu Cuidado</h1>

<p align="center">App de lembretes de remédio para você e para as pessoas de quem você cuida.</p>

<p align="center">
  <a href="https://play.google.com/store/apps/details?id=com.my.little"><img src="https://img.shields.io/badge/Google_Play-dispon%C3%ADvel-0B0E14?style=for-the-badge&logo=googleplay&logoColor=C05B1E" alt="Disponível no Google Play"></a>
  <img src="https://img.shields.io/badge/App_Store-em_revis%C3%A3o-0B0E14?style=for-the-badge&logo=apple&logoColor=EEEDE9" alt="App Store: em revisão">
</p>

<p align="center"><img src="docs/capa.jpg" width="720" alt="Arte de destaque do Meu Cuidado"></p>

## Sobre

Você cadastra os seus remédios e os dos seus dependentes (filhos, pais, avós), e o app avisa no horário de cada dose. A notificação tem os botões Tomei, Adiar e Pular, então dá para registrar a dose sem abrir o app.

Outra pessoa pode cuidar junto: ela recebe um convite por link e passa a acompanhar o mesmo dependente. Para cadastrar um remédio, você aponta a câmera para o código de barras ou fotografa o rótulo, e o app busca o produto na base de medicamentos da Anvisa (CMED).

## Telas

| | | | | |
|:-:|:-:|:-:|:-:|:-:|
| <img src="docs/01-hero.jpg" width="160"> | <img src="docs/02-temas.jpg" width="160"> | <img src="docs/03-familia.jpg" width="160"> | <img src="docs/04-organizado.jpg" width="160"> | <img src="docs/05-cadastro.jpg" width="160"> |

## Como foi feito

- O app confere as notificações que o sistema operacional realmente tem agendadas antes de cancelar ou reagendar, porque um cache local pode ficar desatualizado. Ele também respeita o limite de agendamentos do Android e usa o canal de prioridade máxima.
- Adiar roda em segundo plano. Tomei e Pular abrem o app para gravar a dose com o usuário autenticado.
- A leitura de código de barras e o OCR do rótulo rodam no aparelho com ML Kit e funcionam offline. A foto não é enviada a nenhum servidor.
- Convites e vínculos entre cuidadores passam por funções no Postgres com RLS, e cada pessoa só enxerga os dependentes que cuida.
- A telemetria não recebe dados de saúde nem o texto lido nos rótulos.
- Há testes com Jest e Testing Library, fluxos E2E em Maestro e atualizações OTA pelo EAS Update.

## Arquitetura

```mermaid
flowchart LR
  subgraph Celular["App (Expo / React Native)"]
    UI["Expo Router + Paper"] --> Store["Zustand"]
    Store --> Notif["Agendador de notificações locais"]
    UI --> ML["ML Kit: código de barras e OCR"]
  end
  Store <--> SB["Supabase: Postgres, Auth, Storage, RLS"]
  ML --> CMED["Base CMED / Anvisa"]
  Celular --> FB["Firebase: Crashlytics e Analytics"]
  EAS["EAS Build / Update"] -.-> Celular
```

## Stack

Expo SDK 55 · React Native 0.83 · React 19 · TypeScript · Expo Router · React Native Paper · Reanimated 4 · Zustand · Supabase · expo-notifications · ML Kit · Firebase · Jest · Maestro · EAS

## Meu papel

Fiz o produto, o design, o app, o backend e a publicação nas lojas.

<sub>O código-fonte é privado. Para ver uma demo ou conversar sobre o projeto, fale comigo em <a href="https://abisay.tech">abisay.tech</a> ou no <a href="https://www.linkedin.com/in/jahncarlos">LinkedIn</a>.</sub>
