---
layout: single
title: Depósito de fiança
permalink: /docs/pt/escrow/
toc: true
toc_sticky: true
sidebar:
  title: '<img id="side-icon-verybig" src="/assets/vector/money-bill-transfer.svg"/>Depósito de fiança'
  nav: docs
src: "_pages/docs/pt/03-understand/05-trade-escrow.md"
---

Quando se vende bitcoin, uma garantia de segurança é utilizada na forma de uma garantia de comércio. O RoboSats aproveita as [faturas de retenção](https://github.com/lightningnetwork/lnd/pull/2022) da Lightning no sistema de garantia para proteger o comprador contra fraudes ou falta de pagamento por parte de seu par comercial.

O tempo designado para pagar (travar) uma garantia de comércio é determinado pelo criador do pedido. O temporizador de expiração da garantia padrão é de {{site.robosats.hours_submit_escrow}} horas; no entanto, isso pode ser personalizado para variar de 1 a 8 horas.

Se o vendedor não trancar sua garantia de comércio dentro do limite de tempo dado, então o vendedor perde sua fiança de fidelidade. Consulte [Entender > Bonds](/docs/pt/bonds/) para obter informações adicionais sobre fianças de fidelidade. Além disso, se uma disputa for aberta, os Satoshis em garantia são liberados para o vencedor da disputa.

Certifique-se de usar uma carteira Lightning que funcione bem com o RoboSats, consulte [Entender > Carteiras](/docs/pt/wallets/) para obter informações adicionais.

_Nota: O termo "vendedor" refere-se à venda de bitcoin, enquanto "comprador" refere-se à compra de bitcoin._

## **O que é uma fatura de retenção?**

As faturas de retenção do Lightning, também conhecidas como faturas "hodl", são um tipo de fatura que "trava" fundos em sua carteira e então "desbloqueia" esses fundos dependendo do status da fatura, conforme determinado pelo receptor. Em algumas carteiras, a interface do usuário descreve esse tipo de pagamento como um pagamento "em trânsito" ou "congelado".

Ao contrário dos pagamentos típicos da Lightning que imediatamente são confirmados e liquidados quando o pagamento é recebido, uma fatura de retenção apenas confirma o pagamento, mas ainda não o liquida. A partir desse momento, o remetente não pode revogar seu pagamento e os fundos ficam assim bloqueados em sua carteira, mas ainda não saíram dela. O receptor escolhe se vai liquidar (completar) ou desbloquear (cancelar) o pagamento e a fatura.

Na prática, a fatura de retenção da garantia é bloqueada para o nó coordenador experimental do RoboSats. Isso significa que a fatura é cobrada exatamente quando o vendedor clica em "Confirmar Recebimento da Fiat" e então a fatura do comprador é paga. Durante o tempo necessário para liquidar o pagamento da Lightning para o comprador, o RoboSats tem os fundos enquanto tenta pagar repetidamente o comprador.

Este método é, no momento, a abordagem mais segura para garantir que os pares cumpram sua parte do acordo, uma vez que uma fatura de retenção direta entre vendedor e comprador ainda não foi demonstrada na prática com carteiras convencionais.

## **Como enviar um depósito de fiança**

Primeiro, consulte [Entender > Carteiras](/docs/pt/wallets/) para encontrar carteiras Lightning compatíveis que ajudarão a tornar o uso do RoboSats uma experiência mais tranquila. Dependendo da carteira, os fundos bloqueados podem ser exibidos como um pagamento em trânsito, congelado ou até mesmo falhando. Verifique a lista de compatibilidade da carteira!

Leia o guia relevante dependendo se você está fazendo ou aceitando um pedido para vender bitcoin:

- Criador: Crie uma ordem e modifique as condições do pedido conforme desejar. O pedido pode ser personalizado para exigir um "Temporizador de Garantia/Fatura" (temporizador de expiração) diferente do padrão de {{site.robosats.hours_submit_escrow}} horas, variando de 1 a 8 horas. Quando sua ordem publicada for aceita e o tomador tiver enviado sua fiança de fidelidade, use o código QR mostrado com sua carteira Lightning para bloquear a quantidade indicada de Satoshis como colateral (garantia). _Nota: Os fundos da garantia são liberados para o comprador apenas quando você selecionar "Confirmar Recebimento do Fiat", o que liquida o pedido. Confirme apenas após o fiat ter sido recebido em sua conta._

- Tomador: Navegue pelo livro de ordens e encontre uma ordem de sua preferência. Clique em "Aceitar ordem" e bloqueie sua fiança de fidelidade. Imediatamente após enviar a fiança, use o código QR mostrado com sua carteira Lightning para bloquear a quantidade indicada de Satoshis como colateral (garantia). _Nota: Os fundos da garantia são liberados para o comprador apenas quando você selecionar "Confirmar Recebimento do Fiat", o que liquida o pedido. Confirme apenas após o fiat ter sido recebido em sua conta._

Assim que o tomador da ordem bloquear sua fiança, o comprador e o vendedor devem enviar a fatura de pagamento e a garantia de comércio, respectivamente, dentro do limite de tempo dado.

Por padrão, o temporizador de expiração é de {{site.robosats.hours_submit_escrow}} horas; no entanto, como criador do pedido, você pode personalizar o temporizador para ser de uma hora a oito horas. Em outras palavras, modifique o tempo permitido para bloquear os fundos da garantia e fornecer a fatura de pagamento. Talvez você queira uma transação rápida e configure o temporizador para o máximo de uma hora em vez de {{site.robosats.hours_submit_escrow}} horas.

Se o vendedor bloquear os fundos da garantia antes de o comprador fornecer a fatura de pagamento, então o vendedor aguarda entrar na etapa de chat entre pares somente após o comprador fornecer sua fatura.

Se o vendedor não bloquear os fundos da garantia de forma alguma, então a ordem expirará e o vendedor perderá sua fiança. Metade da fiança perdida vai para o comprador como compensação pelo tempo desperdiçado. Da mesma forma, se o comprador não fornecer a fatura de pagamento dentro do limite de tempo dado, então o comprador perde sua fiança, onde metade vai para o vendedor. Metade restante de uma fiança perdida é "doada" para o RoboSats!

Depois que o depósito for bloqueado, a ordem não poderá ser cancelada, a menos que tanto o criador quanto o tomador concordem em cancelá-lo de forma colaborativa. Além disso, depois que o vendedor confirmar que o decreto foi recebido, o pedido não poderá mais ser cancelado de forma colaborativa. O pedido pode ser concluído com sucesso ou entrar em disputa.

## **Como e quando a garantia é liberada?**

A garantia de comércio é sempre liberada para seu verdadeiro proprietário dependendo do status do comércio ou, se necessário, do resultado da disputa. Existem dois cenários que fazem com que a fatura de retenção da garantia seja liberada:

- Concluir um comércio bem-sucedido onde os fundos são enviados para o comprador (vendedor confirma que o fiat foi recebido)
- Abrir uma disputa se o comércio não foi bem-sucedido onde os fundos são retidos até a resolução da disputa (vendedor intencionalmente não confirmou que o fiat foi recebido)

Os cenários acima são expandidos com mais detalhes abaixo:

Assim que o método de pagamento fiat for coordenado com o comprador, o vendedor clica em "Confirmar Recebimento do Fiat" para encerrar o comércio, o que libera instantaneamente os fundos da garantia para o comprador. O vendedor deve confirmar que o fiat foi recebido após ele aparecer em sua posse.

Se você nunca recebeu o pagamento fiat do comprador, não clique em "Confirmar Recebimento do Fiat" e, em vez disso, abra uma disputa para que a equipe do RoboSats possa revisar. Tentar trapacear intencionalmente não confirmando que o fiat foi recebido resulta em uma disputa sendo aberta automaticamente em nome do comprador.

O robô trapaceiro correrá o risco de perder essa disputa e, consequentemente, perderá sua fiança. A totalidade da garantia bloqueada será liberada e recompensada para o robô honesto.

Não se esqueça do sua ordem! Se seu par enviou o fiat e o temporizador do pedido expirar antes de você confirmar que o fiat foi recebido, então você corre o risco de perder a disputa subsequente, o que por sua vez fará com que sua fiança seja perdida. Tome cuidado para lembrar da sua ordem e faça backup do token único do seu robô!

Devido aos limites de tempo envolvidos no processo de pedido, é recomendável usar métodos de pagamento fiat instantâneos para evitar exceder o temporizador de expiração. Esteja ciente de métodos de pagamento fiat que permitem que o comprador entre em contato com sua instituição fiat e solicite o estorno da transação. É recomendável usar métodos de pagamento que sejam irreversíveis. Consulte [Melhores Práticas > Métodos de Pagamentos](/docs/pt/payment-methods/) para obter informações adicionais.

Embora seja uma janela de tempo muito pequena (cerca de um segundo), a garantia de comércio pode ser permanentemente perdida se o RoboSats for desligado ou desaparecer repentinamente entre o momento em que o vendedor confirma que o fiat foi recebido e o momento em que a carteira Lightning do comprador registra os fundos da garantia liberados. Use uma carteira Lightning bem conectada, com liquidez inbound suficiente, para ajudar a evitar falhas de roteamento e, consequentemente, minimizar qualquer oportunidade nessa janela.

## **Informações adicionais**

Algumas carteiras Lightning têm dificuldade em reconhecer a fatura de retenção do Lightning como uma retenção de seus fundos. Como vendedor, é necessário usar uma carteira que permita múltiplos HTLCs pendentes, pois você precisará bloquear fundos para uma fiança e depois para uma garantia.

Se surgirem problemas, entre em contato com o grupo RoboSats no SimpleX; mas cuidado com os golpistas que podem entrar em contato diretamente com você e se passar por funcionários do RoboSats! Os funcionários do RoboSats nunca entrarão em contato diretamente com você primeiro. Veja [Contribuir > Código > Canais de Comunicação](/contribute/code/#communication-channels) para obter o link do grupo SimpleX.

{% include improve_pt %}