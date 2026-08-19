# Lidi Natura — Catálogo Online

Catálogo web com 417 produtos extraídos do PowerPoint `catalogo 548`. O cliente navega,
seleciona os produtos, e finaliza o pedido direto no seu WhatsApp.

## 1. Configuração (já preenchida)

No `index.html`, perto do fim do arquivo, fica o bloco **CONFIGURAÇÃO**:

```js
const CONFIG = {
  whatsapp: "5584986751867",        // 55 + DDD + número, só dígitos
  loja: "Lidi Natura",              // nome exibido no topo e no rodapé
  parcelasMax: 12,                  // até quantas vezes o cliente pode parcelar
  taxaParcelado: 5.59,              // % fixo cobrado pela maquineta no parcelado
  taxaPorParcela: 2.99,             // % adicional por parcela
  brindeMin: 200                    // valor do pedido que dá direito ao brinde surpresa
};
```

Para mudar a taxa do cartão ou o número de parcelas, altere só esses valores — o site
recalcula tudo sozinho (preço parcelado nos produtos, total do carrinho e mensagem do WhatsApp).

## Formas de pagamento

- **À vista (Pix, débito ou crédito 1x)** — sem acréscimo. É o preço em destaque no produto.
- **Parcelado no cartão, até 12x** — acréscimo de 5,59% + 2,99% por parcela.
  Ex: 3x → 14,56%; 6x → 23,53%; 12x → 41,47%.
  O cliente escolhe as parcelas no carrinho. Por decisão sua, **no parcelado o site mostra
  apenas "3x de R$ 87,83"** — sem exibir o valor total nem a porcentagem.

## Brinde surpresa

Pedidos com **R$ 200 ou mais em produtos** (valor à vista, sem o acréscimo do cartão)
dão direito a um brinde surpresa. O carrinho mostra quanto falta para atingir, e o aviso
vai junto na mensagem do WhatsApp. Para mudar o valor, altere `brindeMin` no `CONFIG`.

As artes da promoção estão em `marca/banner-brinde.png` (quadrado) e
`marca/banner-brinde-story.png` (story).

## 2. Testar no computador

Dê dois cliques em `index.html` — abre no navegador e funciona 100% offline.

## 3. Colocar no ar (link para mandar aos clientes)

**Opção mais fácil — Netlify Drop (grátis, 1 minuto, sem cadastro para testar):**
1. Acesse https://app.netlify.com/drop
2. Arraste a pasta `catalogo-online` inteira para a página
3. Pronto: você recebe um link tipo `https://seunome.netlify.app` — é esse link que
   você manda no WhatsApp, no status e na bio do Instagram

Outras opções: GitHub Pages, Vercel, Cloudflare Pages — todas grátis, mesmo princípio
(subir a pasta inteira, com a subpasta `img`).

## 4. Como o cliente usa

1. Busca ou filtra por categoria/marca (Natura ou Avon)
2. Toca em **Adicionar** e ajusta a quantidade (limitada ao seu estoque)
3. Toca em **Ver pedido**, escolhe **Pix à vista** ou **Cartão até 3x**, informa nome e observação
4. Toca em **Finalizar no WhatsApp** → abre seu WhatsApp com o pedido já escrito:

```
Olá! Quero fazer um pedido do catálogo:

1. ÁGUAS FLOR DE LARANJEIRA — NATURA 170 ML
   2x R$ 64,90 = R$ 129,80

Itens: 2
Subtotal: R$ 129,80
Pagamento: Cartão (acréscimo de 7% = R$ 9,09)
*Total: R$ 138,89* — em até 3x de R$ 46,30
(economia de R$ 104,00)

Nome: Maria
```

O carrinho fica salvo no celular do cliente mesmo se ele fechar a página.

## 5. Atualizar preços e estoque

Todos os dados estão em `produtos.js`, um produto por linha:

```js
{"id":1,"nome":"ÁGUAS FLOR DE LARANJEIRA","marca":"NATURA","categoria":"Perfumaria Feminina",
 "tamanho":"170 ML","de":116.9,"preco":64.9,"desconto":48,"estoque":2,"img":"001-....jpg"}
```

- `preco` = seu preço de venda à vista (Pix)
- `de` = preço de mercado riscado
- `estoque` = quantidade disponível (o cliente não consegue pedir mais que isso)
- Para tirar um produto do ar, apague a linha dele ou coloque `"estoque":0`

Depois de editar, salve o arquivo e suba a pasta de novo (no Netlify: arraste outra vez).

## Observações sobre os dados

- **417 produtos** (145 perfumaria feminina, 86 masculina, 98 corpo, 41 cabelos,
  6 infantil, 41 rosto) — os 7 slides de capa/seção do PPT não viraram produto.
- **3 produtos sem foto** no PPT original (Renew Sabonete Gel, Renew Sérum Vitamina C,
  Renew Tônico Vitamina C) — aparecem com ícone no lugar da imagem.
- **1 produto sem preço** no PPT original (Chronos Protetor Multiclareador 70 FPS) —
  aparece como "Sob consulta" e vai para o WhatsApp como "preço a combinar".
  Se quiser, defina o preço dele em `produtos.js`.
- Imagens redimensionadas para 700px e comprimidas: 53 MB → 9 MB (carrega rápido no 4G).
