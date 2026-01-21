# 🛒 Carrinho – WPP (Recuperação de Abandono via WhatsApp)

Este workflow do n8n automatiza a recuperação de carrinhos abandonados da Hotmart, enviando mensagens automáticas via WhatsApp (Z-API) para o comprador finalizar a compra.

 Como funciona
Hotmart (Postback)
        ↓
Webhook (n8n)
        ↓
Validação de Token (If)
        ↓
Identificação do Evento (Switch)
        ↓
Montagem da Mensagem
        ↓
Envio via Z-API (WhatsApp)

 Entrada (Hotmart Postback)

O fluxo recebe eventos da Hotmart, como:

PURCHASE_OUT_OF_SHOPPING_CART → Abandono de carrinho

PURCHASE_EXPIRED → Compra expirada

O Webhook valida o header:

x-hotmart-hottok


Somente requisições com o token correto são processadas.

 Tratamento dos Dados

Do payload da Hotmart, o fluxo extrai:

Campo	Origem
LeadName	buyer.name
Phone	buyer.phone
produtoURL	Link fixo do produto
 Roteamento por Evento

Node Switch:

Evento	Saída
PURCHASE_OUT_OF_SHOPPING_CART	Abandono de carrinho
PURCHASE_EXPIRED	Compra expirada
 Mensagem Enviada
Ei! Percebemos que você deixou alguns produtos no carrinho.
Eles ainda estão te esperando!

Finalize sua compra agora antes que acabe o estoque.

 https://pay.hotmart.com/O102059941V?bid=1759967035641

Se tiver qualquer dúvida, é só me chamar — posso te ajudar a concluir rapidinho.

 Envio via WhatsApp (Z-API)

A mensagem é enviada usando:

Endpoint: send-text

Header: client-token

Corpo:

{
  "phone": "telefone do comprador",
  "message": "mensagem de recuperação"
}

 Memória (Opcional)

Após o envio, a mensagem é salva no node:

Chat Memory Manager

Para histórico e rastreio.

 Tecnologias

n8n

Hotmart Postback

Z-API (WhatsApp)

LangChain Memory Manager

 Como usar

Importe Carrinho - WPP.json no n8n

Configure:

Token da Hotmart

Token da Z-API

Troque o link do produto

Ative o workflow

Cadastre o Webhook na Hotmart 🚀

 Benefícios

Recupera vendas perdidas

Automatiza follow-up

Comunicação direta no WhatsApp

Funciona 24/7
