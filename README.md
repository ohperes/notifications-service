![Wallpaper- 2560x1600](https://user-images.githubusercontent.com/28010081/207477511-998f2136-58a2-42fa-88c6-243306ba27a0.png)

<p align="center">
   Uma API de entrega de notificações
</p>

## :atom: Projeto

O projeto desenvolvido durante o bootcamp IgniteLab da <a href="https://www.rocketseat.com.br/"> Rocketseat </a>, tem as funcionalidades:
- Criar notificação
- Retornar todas as notificações de um recipiente
- Contar todas as notificações de um recipiente
- Marcar uma notificação como lida
- Marcar uma notificação como não lida
- Cancelar a notificação

## 🔧 Tecnologias
- NodeJS
- NestJS
- Kafka
- Jest

## :octocat: Rodando o projeto

Instalar as dependências

```sh
npm install
```

Iniciar o ambiente

```sh
npm run start:dev
```

Para criar um producer você pode iniciar um projeto node:
```bash
npm init
```

Instalar o kafka:
```
npm i kafkajs
```
Criar um cluster no <a href='https://console.upstash.com/'>Upstash</a>.

E configurar o producer: 
```js
import { Kafka } from 'kafkajs'
import { randomUUID } from 'node:crypto'

async function bootstrap() {
  const kafka = new Kafka({
    clientId: 'test-producer',
    brokers: ['paste_your_broker'],
  sasl: {
    mechanism: 'scram-sha-256',
    username: 'paste_your_username',
    password: 'paste_your_password',
  },
  ssl: true,
  })

  const producer = kafka.producer()

  await producer.connect()

  await producer.send({
    topic: 'notifications.send-notification',
    messages: [
      {
        value: JSON.stringify({
          content: 'Nova solicitação de amizade!',
          category: 'social',
          recipientId: randomUUID(),
        })
      }
    ]
  })

  await producer.disconnect()
}

bootstrap()
```

<p align="right">
  <a href="https://github.com/ohperes">
    <img src="https://img.shields.io/badge/Made%20by-ohperes-green">
  </a>
</p>
