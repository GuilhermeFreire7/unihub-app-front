# UniHub

Aplicativo mobile (Expo / React Native) para estudantes organizarem sua vida acadêmica: montar a grade horária, acompanhar disciplinas e faltas, e gerenciar atividades em um quadro estilo kanban com calendário integrado.

## Funcionalidades

- **Autenticação** — login e cadastro de usuário (nome, matrícula, e-mail e senha), com token JWT persistido localmente.
- **Montagem de grade horária** — lista as disciplinas ofertadas, permite adicionar/remover disciplinas da grade do usuário.
- **Grade do aluno** — edição de professor, sala e faltas por disciplina, com cálculo automático do percentual de faltas (alerta visual acima de 25%) e opção de compartilhar a grade via WhatsApp ou e-mail.
- **Quadro de atividades (Kanban)** — atividades organizadas em colunas (Pendente, Em Progresso, Concluído) com drag-and-drop, filtro por disciplina, criação/edição/exclusão via modal.
- **Calendário** — visualização de prazos de atividades por data, em português.
- **Tema claro/escuro** — com persistência da preferência do usuário.

## Stack

- [Expo](https://expo.dev/) 53 + [Expo Router](https://docs.expo.dev/router/introduction/) (roteamento baseado em arquivos)
- React Native 0.79 / React 19
- TypeScript
- Axios para comunicação com a API
- AsyncStorage para persistência local (token, usuário, tema)
- react-native-calendars, react-native-gesture-handler, react-native-reanimated
- react-native-toast-message para feedback ao usuário

## Pré-requisitos

- [Node.js](https://nodejs.org/) 18+
- npm
- App [Expo Go](https://expo.dev/go) no celular (para testar em dispositivo físico) ou emulador Android/iOS configurado
- Uma instância da [API do UniHub](./services/api.ts) rodando (backend próprio, não incluso neste repositório)

## Instalação

```bash
npm install
```

## Configuração da API

A URL base da API está definida em [services/api.ts](./services/api.ts):

```ts
export const API_URL = "http://localhost:8000";
```

Ajuste esse valor conforme o ambiente:
- **Emulador Android**: use `http://10.0.2.2:8000` no lugar de `localhost`.
- **Dispositivo físico via Expo Go**: use o IP local da máquina que roda o backend (ex.: `http://192.168.1.2:8000`), garantindo que o dispositivo esteja na mesma rede.

> Nota: o hook [hooks/useDisciplinas.ts](./hooks/useDisciplinas.ts) atualmente define sua própria constante `API_URL` com um IP fixo — ajuste-a também caso utilize esse hook.

## Executando o projeto

```bash
npm start        # abre o Expo Dev Tools / Metro Bundler
npm run android  # abre no emulador/dispositivo Android
npm run ios      # abre no simulador/dispositivo iOS
npm run web      # abre a versão web
```

## Scripts disponíveis

| Script | Descrição |
| --- | --- |
| `npm start` | Inicia o servidor de desenvolvimento do Expo |
| `npm run android` | Executa o app em um dispositivo/emulador Android |
| `npm run ios` | Executa o app em um dispositivo/simulador iOS |
| `npm run web` | Executa o app no navegador |
| `npm run enviarDisciplinas` | Script utilitário (TypeScript) para envio/carga de disciplinas |

## Estrutura do projeto

```
app/                # Telas (Expo Router)
  index.tsx           # Login
  signup.tsx          # Cadastro
  home.tsx            # Início (menu, calendário)
  gradeBuilder.tsx     # Montagem da grade horária
  studentGrade.tsx     # Grade do aluno (faltas, professor, sala)
  board.tsx            # Quadro de atividades (kanban)
  _layout.tsx           # Layout raiz (providers, stack de navegação)
components/          # Componentes reutilizáveis (Drawer, cards, modais, etc.)
contexts/            # Contextos React (tema)
hooks/               # Hooks customizados
services/            # Configuração de acesso à API
theme/               # Paleta de cores (claro/escuro)
```

## Licença

Projeto privado, sem licença definida.
