# Segurança - Noite no Castelo

Versão 1.0 - 28 de outubro de 2026

## Como relatar uma vulnerabilidade

Envie uma mensagem direta ao autor no Instagram **@elias_dev0101** com: o que você encontrou, passos para reproduzir e o navegador usado. Pedimos divulgação responsável: não publique detalhes antes de uma correção ou de 30 dias, o que vier primeiro. Não há programa de recompensas. O autor agradece e dá crédito, se você quiser.

Escopo: o código deste Jogo. Fora de escopo: falhas do navegador ou do serviço de hospedagem.

## Arquitetura de segurança (privacidade por padrão)

| Medida | Como funciona |
| --- | --- |
| Sem rede | O Jogo é um único arquivo. Não há API, servidor, login nem requisição de saída. A CSP usa `connect-src 'none'`. |
| CSP por hash | A versão independente (`index.html`) traz uma CSP em `<meta>` que só permite o script e o estilo com o hash SHA-256 exato do arquivo. `default-src 'none'`, `img-src data:`, `font-src data:`, `object-src 'none'`, `base-uri 'none'`, `form-action 'none'`. Qualquer script injetado é bloqueado. |
| Sem terceiros | Fonte, imagens, música e efeitos estão embutidos ou são gerados por código. Nada de CDN, Google Fonts ou analytics (isso evitaria vazar o IP do jogador). |
| Armazenamento mínimo | Só com consentimento. Chave `nnc.v1` com 3 campos. A leitura valida o tipo e o intervalo de cada campo antes de usar. |
| Sem código dinâmico | Não usa `eval`, `new Function`, `innerHTML` com dados externos nem `postMessage`. |
| Referrer | `<meta name="referrer" content="no-referrer">`. |
| Permissões | O Jogo não pede câmera, microfone, localização nem notificações. |

## Cabeçalhos HTTP recomendados na hospedagem

O build gera `dist/_headers` (formato Netlify e Cloudflare Pages) com a CSP calculada para o arquivo e os cabeçalhos abaixo. Algumas proteções só existem como cabeçalho HTTP, não como `<meta>`:

- `Content-Security-Policy` com `frame-ancestors 'none'` (impede que outro site coloque o Jogo em um frame);
- `X-Content-Type-Options: nosniff`;
- `Referrer-Policy: no-referrer`;
- `Permissions-Policy: camera=(), microphone=(), geolocation=(), payment=(), usb=(), interest-cohort=()`;
- `Cross-Origin-Opener-Policy: same-origin`;
- `Strict-Transport-Security` (HTTPS obrigatório; normalmente já vem na hospedagem).

Se você mudar qualquer linha do Jogo, rode o build de novo: o hash da CSP muda junto.

## Lista de verificação antes de publicar

1. HTTPS ativo e sem conteúdo misto.
2. `_headers` (ou equivalente no servidor) aplicado.
3. Nenhum script de analytics, fonte externa ou widget de terceiros adicionado à página.
4. Foro e cidade preenchidos na licença.
5. Revisão jurídica da licença e da política de privacidade.

## Riscos conhecidos e aceitos

- O armazenamento local pode ser lido por outro programa ou extensão que já tenha acesso ao navegador do jogador. Os dados guardados (recorde e som) não são sensíveis.
- Um jogador pode editar o próprio recorde. O Jogo não tem ranking online, então isso só afeta ele mesmo.
