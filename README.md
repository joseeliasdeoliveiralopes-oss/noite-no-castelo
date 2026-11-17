# Noite no Castelo

Jogo de plataforma 2D em pixel art, com tema de castelo gótico, protagonizado por uma caçadora de cabelo preto cacheado, vestida de preto, com lenço vermelho.
Três fases, quatro tipos de monstros, um chefe (O Conde), trilha chiptune original e 27 efeitos sonoros.
Roda inteiro no navegador, em um único arquivo, sem coletar nenhum dado.

## Como jogar

| Ação | Teclado | Toque |
| --- | --- | --- |
| Mover | Setas ou A / D | botões na tela |
| Pular (segure para pular mais alto) | Z, Espaço ou K | PULAR |
| Chicote | X ou J | CHICOTE |
| Correr | Shift, C ou L | CORRER |
| Pausa / Som | P ou Esc / M | botões abaixo do jogo |

Pule em cima dos monstros ou acerte-os com o chicote. Quebre as velas para achar gemas e corações. Toque os sinos para marcar o ponto de continuação. Cruze a porta no fim de cada fase.

## Arquivos

- `index.html`: o jogo completo (abra direto no navegador ou hospede em qualquer lugar).
- `_headers`: cabeçalhos de segurança prontos para Netlify e Cloudflare Pages, com a CSP calculada para este arquivo.
- `LICENSE.md`: licença de uso. `PRIVACY.md`: política de privacidade (LGPD). `SECURITY.md`: segurança. `NOTICE.md`: créditos e licença da fonte.

## Publicar

1. Suba `index.html` e `_headers` na hospedagem (Netlify, Cloudflare Pages, GitHub Pages com cabeçalhos via CDN).
2. Confirme HTTPS ativo.
3. Preencha o foro (cidade/UF) na cláusula 11 da licença e rode o build de novo.
4. Não adicione analytics, fontes externas nem scripts de terceiros: a CSP vai bloquear e a política de privacidade deixaria de ser verdadeira.

## Código-fonte

`src/` contém o código (sprites, motor, fases, áudio, cenas, CSS e HTML). `tools/build.py` junta tudo em `dist/index.html` e gera `dist/_headers`.
`tools/bot.py` é um jogador automático que verifica se as três fases e o chefe têm solução; `tools/audio_test.py` mede o volume da música e dos efeitos; `tools/smoke.py` confere erros de console e violações de CSP.

```
python3 tools/build.py
python3 tools/bot.py "$PWD/dist/index.html" 0 god
```

## Aviso

Os documentos jurídicos são modelos próprios e não substituem a orientação de um advogado. Revise-os antes de qualquer uso comercial. A titularidade de partes criadas com apoio de IA pode ter tratamento jurídico incerto; confirme com um profissional.

(c) 2026 José Elias de Oliveira Lopes (Elias Dev). Todos os direitos reservados, salvo o uso previsto na licença.

## Combate e equipamentos (v2)

| Tecla | Ação |
|---|---|
| X / J | Atacar (repita para combos) |
| ↑ + X / ↓ + X | Golpe ascendente / golpe baixo (no ar: mergulho) |
| B | Arte especial da arma (gasta energia) |
| V | Arma secundária (gasta energia) |
| R | Item rápido (poção/elixir) |
| Q / E | Trocar arma principal / secundária |
| Tab, I ou Enter | Menu de equipamentos |

14 armas principais (punhos, manoplas, chicotes, espadas, florete, adagas, machado, lança, montante, alabarda, cajado), 6 secundárias (adaga, machado, água benta, cruz, bola de fogo, raio), elmos, armaduras, acessórios, consumíveis e relíquias. Itens ficam escondidos nas velas e caem dos inimigos; a heroína ganha XP e sobe de nível.

### Especial do pai (F)
O coração vermelho abaixo do HUD enche ao acertar (+2), derrotar (+6) e sofrer dano (+4). Cheio, **F** (ou o botão PAI) chama o pai da heroína: ele surge num círculo de luz, avança, carrega e dispara um raio de corações que atinge uma vez cada inimigo na linha. Depois some e a barra recomeça do zero.

### Fases e chefes (v3)
5 fases: Portões do Castelo, Biblioteca Proibida, Salão do Conde (chefe: O Conde), Catacumbas (chefe: O Ceifador) e Trono Sombrio (chefe final: Elias, o Rei Sombrio). Ao vencer cada chefe a heroína fala sobre libertar Elias; no fim, ela o liberta com amor.
