# Catálogo de veículos da Elettra

Os carros que aparecem na Elettra vêm só deste catálogo. Os usuários não importam carros: eles escolhem um destes na janela do veículo (ou deixam no automático, que alterna os carros do catálogo).

O catálogo fica num **repositório público só dos veículos** no GitHub, publicado pelo GitHub Pages. O código da Elettra continua no repositório privado.

A Elettra lê a lista em:

```
https://viniciusmorsch-eng.github.io/elettra-veiculos/catalogo.json
```

Se o repositório tiver outro nome, troque `CATALOGO_URL` no `index.html`.

## Repositório

O repositório é [viniciusmorsch-eng/elettra-veiculos](https://github.com/viniciusmorsch-eng/elettra-veiculos), público, com o GitHub Pages publicando a branch `main`, pasta `/ (root)` (**Settings → Pages**). Ele tem o `catalogo.json`, o `.nojekyll` (só a presença dele conta: com ele, o Pages publica os arquivos como estão), este README e a pasta `modelos/` para os arquivos dos carros. A pasta `catalogo-veiculos` do projeto da Elettra guarda uma cópia deste conteúdo.

## Pôr um carro novo

Dá para fazer tudo pelo site do GitHub, sem instalar nada:

1. No repositório, abra a pasta `modelos/`, clique em **Add file → Upload files**, arraste o `.glb` do carro e confirme em **Commit changes**. Use GLB com tudo embutido: texturas dentro do arquivo, de preferência com até 15 MB (o site aceita até 25 MB por arquivo). Use só modelos com licença de uso; carros de montadoras, só com autorização. O repositório é público: qualquer pessoa pode baixar os arquivos.
2. Abra o `catalogo.json`, clique no lápis (**Edit this file**), acrescente o carro na lista `veiculos` e confirme em **Commit changes**. Entre um carro e outro vai uma vírgula:

```json
{
  "versao": 1,
  "veiculos": [
    {
      "id": "sedan-eletrico-branco",
      "nome": "Sedã elétrico branco",
      "arquivo": "modelos/sedan-eletrico-branco.glb",
      "comprimento": 4.7,
      "giro": 0,
      "upZ": false,
      "ativo": true,
      "auto": true,
      "versao": 1,
      "descricao": "Sedã médio, para vagas comuns e de recarga"
    }
  ]
}
```

3. Em alguns minutos o carro aparece para todos os usuários (o andamento da publicação fica na aba **Actions** do repositório). Quem já está com a Elettra aberta vê o carro novo ao recarregar a página ou ao usar "Atualizar catálogo" em Biblioteca 3D → Veículos da plataforma.

## Campos de cada carro

| Campo | O que é |
|---|---|
| `id` | Identificador do carro: letras, números, `-`, `_` ou `.`. **Nunca mude** depois de publicado: os estudos dos usuários guardam o carro por ele. |
| `nome` | Nome que o usuário vê na lista de modelos. |
| `arquivo` | Caminho do `.glb`, relativo ao `catalogo.json` (ou um endereço completo). |
| `comprimento` | Comprimento real do carro, em metros (de 2 a 12). A Elettra ajusta a escala por ele. |
| `giro` | `0`, `90`, `180` ou `270`: correção, em graus, para um modelo que aparece de lado ou de ré. |
| `upZ` | `true` se o arquivo vier com o eixo Z para cima (exportado de programas de CAD); o normal é `false`. |
| `ativo` | `false` tira o carro da lista de escolha. Os estudos que já usam o carro continuam com ele. |
| `auto` | `false` deixa o carro fora do automático: ele só aparece quando escolhido. |
| `versao` | Troque o número quando substituir o arquivo `.glb`, para os navegadores baixarem o novo. |
| `descricao` | Texto curto opcional, mostrado na Biblioteca 3D. |

Se você apagar um carro da lista, os veículos que usavam esse carro passam a mostrar o modelo genérico.

## Rodas que giram

Nos veículos que andam nas rotas, as rodas giram e as da frente esterçam. A Elettra acha as rodas pelo nome das peças (wheel, roda, tire, pneu, rim, aro…) ou, se não achar, pelo formato. A Biblioteca 3D mostra, no cartão de cada carro, quantas rodas foram achadas. Se o cartão disser que não achou, a roda está ligada à carroceria na mesma malha do modelo. Nesse caso, separe as rodas no Blender antes de publicar.

## Testar um carro antes de publicar

1. Na pasta do projeto da Elettra, ponha o `.glb` em `catalogo-veiculos/modelos/` e o carro em `catalogo-veiculos/catalogo.json`. Os `.glb` dessa pasta ficam fora do repositório privado, pelo `.gitignore`.
2. Sirva a pasta do projeto, por exemplo com `python -m http.server 8000`.
3. Abra `http://localhost:8000/?catalogo=local`. Com esse endereço, a Elettra usa só a lista local.
4. Ao abrir a Elettra sem `?catalogo=local`, vale a lista online. A cópia local só entra quando a lista online não responde.
