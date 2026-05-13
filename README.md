# Grelha de turnos · Farmácia Faria

Ferramenta web que converte o mapa mensal de turnos (Excel) numa grelha visual pintada de 30 em 30 minutos, das 08:30 às 22:00, uma célula por colaborador.

## Como usar

1. Abre o site: `https://[teu-username].github.io/[nome-do-repo]/`
2. Arrasta o `.xlsx` mensal para a área de upload (ou clica para escolher)
3. Confirma a deteção (colaboradores, dias, turnos)
4. Descarrega a grelha em Excel

Toda a lógica corre no browser — o ficheiro nunca sai do teu computador.

## Estrutura esperada do ficheiro de entrada

- **Dois blocos verticais:** dias 1-16 (linhas 1-13) e dias 17-31 (linhas 16-28)
- **Linha 1 / linha 16:** dias da semana (Seg, Ter, …, Sáb, Dom)
- **Linha 2 / linha 17:** números dos dias
- **Coluna A:** iniciais dos colaboradores
- **Restantes células:** turnos em texto

## Códigos reconhecidos

| Código | Significado |
|---|---|
| `9-13`, `9-13+15-19` | Turnos normais (intervalos separados por `+`) |
| `8.30-12.30` | Minutos com ponto ou dois pontos (`9:30` = `9.30`) |
| `F1`, `F2`, `F1/10` | Férias (com ou sem fração de tipo "1 de 10") |
| `f` | Folga |
| `FN`, `FN 30/4` | Folga da noite (com ou sem data) |
| `formação` | Formação |
| `-` ou vazio | Não trabalha |
| `(r)`, `(e)`, `(c)` | Anotações — preservadas no texto mas ignoradas no parsing |
| `+N` no fim | Turno de noite a seguir — não contabilizado na grelha diurna |
| `*9-13+14-18*` | Asteriscos envolventes são removidos antes do parsing |

## Correções automáticas de typos

A app deteta e corrige automaticamente padrões prováveis de typo, listando-os no Excel final para revisão:

- `9.13` isolado → `9-13`
- `9+12+13-19` → `9-12+13-19`
- `14-18.30-19.30-22` → `14-18.30+19.30-22`

## Paleta de cores predefinida

| Iniciais | Cor |
|---|---|
| AB | Azul claro |
| BF | Pêssego |
| DC | Verde claro |
| IA | Cinza |
| IM | Amarelo claro |
| MA | Lavanda |
| MO | Verde menta |
| RL | Azul lavanda |
| SA | Rosa |
| SP | Verde sálvia |
| TA | Azul céu |
| TM | Laranja claro |

Colaboradores fora desta lista recebem uma cor pastel de reserva automaticamente.

## Deploy no GitHub Pages

1. Cria um repositório público (ex: `grelha-turnos`)
2. Faz upload do `index.html`
3. Settings → Pages → Source: `Deploy from a branch` → `main` / `(root)` → Save
4. Espera 1-2 min e acede ao URL que aparece

## Tecnologia

- HTML/CSS/JS puro, zero build step
- [SheetJS](https://sheetjs.com/) para ler e escrever `.xlsx`
- [JSZip](https://stuk.github.io/jszip/) para o empacotamento OOXML
- Bibliotecas carregadas via CDN (cloudflare)

## Privacidade

Tudo corre no browser. O ficheiro Excel nunca é enviado para nenhum servidor.
