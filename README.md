# 🧾 Auditor de Taxas POS

Ferramenta **100% client-side** (HTML + CSS + JS, sem backend) para auditar e conciliar as taxas cobradas por adquirentes de cartão (Stone, Cielo, Rede, Getnet, PagBank, Ton, SumUp, InfinitePay, SafraPay, Mercado Pago, Vero, Bin, Global Payments, Zettle, Nubank, entre outras) contra as taxas negociadas com o lojista.

Nenhum dado de venda é enviado ao backend da aplicação — todo o processamento do arquivo acontece no próprio navegador. O e-mail informado para liberar o relatório é enviado ao Netlify Forms para captura do lead.

## ✨ Funcionalidades

- Configuração das taxas negociadas: débito, crédito à vista, **Pix na maquininha** e crédito parcelado (2x a 21x), salvas no `localStorage` do navegador.
- Upload por drag-and-drop ou seleção manual de arquivos `.csv` ou `.xlsx`.
- Mapeamento automático de colunas — reconhece variações comuns de nomenclatura entre adquirentes (`Valor Bruto` / `Gross Amount` / `Amount`, `Taxa (%)` / `MDR` / `Taxa Aplicada`, `Valor Líquido` / `Net Amount`, `Modalidade` / `Tipo de Pagamento` / `Transaction Type`, etc.).
- Identificação automática da modalidade (débito, crédito à vista, Pix, crédito parcelado + número da parcela) e exclusão de estornos/cancelamentos e saques.
- Dashboard executivo: total bruto processado, total de taxas cobradas, quantidade de divergências e prejuízo total.
- Tabela detalhada apenas das transações em que a taxa praticada foi maior que a negociada.
- Download do relatório completo em `.xlsx` (resumo + divergências), liberado após o preenchimento de um e-mail.
- Captura do e-mail via **Netlify Forms**, sem backend próprio.

## 🌐 Deploy no Netlify

O projeto é uma aplicação estática e não possui etapa de build. O arquivo `netlify.toml` configura a raiz do repositório como diretório publicado.

No Netlify, importe o repositório do GitHub e use:

- **Branch:** `main`
- **Build command:** vazio
- **Publish directory:** `.`

O formulário `lead-capture` está marcado com `data-netlify="true"`. Depois do primeiro deploy, os e-mails enviados pelos usuários ficam disponíveis em **Netlify → Forms → lead-capture → Submissions**.

O envio é feito pelo navegador via `POST` para o próprio site. O download do relatório só é liberado depois que o Netlify confirma o recebimento do e-mail.

## ⚠️ Limitações conhecidas

Adquirentes que exportam relatórios em formato posicional EDI com **códigos numéricos** de produto em vez de texto descritivo (ex.: alguns layouts EDI puros da Cielo e da Bin) não trazem uma coluna de modalidade legível. Nesses casos a ferramenta ignora essas linhas com segurança em vez de arriscar uma classificação incorreta. Isso não afeta as exportações em CSV/XLSX feitas pelos portais web, que é o formato mais comum.

O processamento das vendas continua 100% client-side. Porém, o e-mail solicitado antes do download é enviado ao **Netlify Forms** para captura do lead. Portanto, a aplicação continua sem backend próprio, mas deixa de ser totalmente isolada do ponto de vista do e-mail.

## 📁 Estrutura do projeto

```
.
├── index.html                          # a aplicação (HTML + CSS + JS embutidos)
├── README.md                           # este arquivo
├── CHANGELOG.md                        # histórico de versões
├── CONTRIBUTING.md                     # como propor mudanças / novas adquirentes
├── LICENSE                             # MIT
├── .editorconfig                       # padronização de indentação entre editores
├── .gitignore                          # evita versionar .csv/.xlsx reais
└── .github/
    ├── workflows/deploy.yml            # publica no GitHub Pages a cada push na main
    ├── PULL_REQUEST_TEMPLATE.md
    └── ISSUE_TEMPLATE/
        ├── bug_report.md
        └── feature_request.md
```

## 🚀 Como usar localmente

Não há build nem dependências — é um único arquivo estático.

```bash
git clone https://github.com/SEU_USUARIO/auditor-taxas-pos.git
cd auditor-taxas-pos
# abra index.html direto no navegador, ou sirva localmente:
python3 -m http.server 8080
# depois acesse http://localhost:8080
```

## 🌐 Publicar no Netlify

O deploy recomendado é pelo Netlify conectado ao repositório GitHub. O Netlify publica automaticamente a `main` a cada `push`.

Configuração:

- **Branch to deploy:** `main`
- **Build command:** vazio
- **Publish directory:** `.`

O arquivo `netlify.toml` já registra o diretório publicado.

## 📦 Subindo este projeto para o GitHub

```bash
cd auditor-taxas-pos
git init
git add .
git commit -m "Auditor de Taxas POS - versão inicial"
git branch -M main
git remote add origin https://github.com/SEU_USUARIO/auditor-taxas-pos.git
git push -u origin main
```

## 🗂️ Organizando o repositório no GitHub

1. **Nome do repositório**: `auditor-taxas-pos` (minúsculo, com hífen) — mantém consistência com a URL do GitHub Pages usada neste README.
2. **Descrição curta** (aparece no topo do repo): "Auditoria e conciliação de taxas de maquininha (Stone, Cielo, Rede, Getnet e outras) — 100% client-side."
3. **Topics** (em "About" → engrenagem): `fintech`, `pos`, `mdr`, `javascript`, `tailwindcss`, `client-side`, `auditoria-financeira` — ajuda outras pessoas a encontrarem o projeto.
4. **Visibilidade**: pode ser público sem risco, já que o código não contém dados de vendas — só a lógica de auditoria.
5. **Branch padrão**: `main` (já configurado nos comandos abaixo).
6. **Branch protection** (opcional, em Settings → Branches): exigir Pull Request antes de mesclar na `main`, mesmo sozinho — cria o hábito de revisar antes de publicar no Pages.
7. **Releases**: a cada mudança relevante, crie uma tag/release (ex. `v1.1.0`) correspondente ao que está no `CHANGELOG.md`, em Releases → "Draft a new release".
8. **Settings → Pages**: Source = **GitHub Actions** (o workflow incluso cuida do resto).

## 🛠️ Stack

- HTML5 / CSS3 / JavaScript (vanilla, sem framework)
- [Tailwind CSS](https://tailwindcss.com/) via CDN
- [SheetJS (xlsx)](https://sheetjs.com/) via CDN, para leitura de `.csv` e `.xlsx`
- `localStorage` do navegador para persistência da configuração de taxas

## 📄 Licença

MIT — veja [LICENSE](LICENSE).
