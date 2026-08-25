# Contribuindo

Obrigado por querer contribuir com o Auditor de Taxas POS! É um projeto simples de propósito — um único arquivo estático — então o fluxo de contribuição também é simples.

## Como propor uma mudança

1. Abra uma [issue](../../issues) descrevendo o problema ou a melhoria antes de codar, principalmente para mudanças maiores (nova adquirente, nova modalidade de pagamento, etc.).
2. Faça um fork do repositório e crie uma branch a partir de `main`:
   ```bash
   git checkout -b minha-melhoria
   ```
3. Edite `index.html` diretamente — não há build, então o que você vê é o que roda.
4. Teste localmente abrindo o arquivo no navegador (ou `python3 -m http.server`) com uma planilha de exemplo.
5. Abra um Pull Request descrevendo o que mudou e por quê.

## Adicionando suporte a uma nova adquirente

Se a taxa/coluna da sua adquirente não está sendo reconhecida:

1. Abra o `index.html` e localize o dicionário `COLUMN_SYNONYMS` (dentro da tag `<script>`).
2. Adicione o nome exato do cabeçalho da coluna (já em minúsculas, sem acento — veja a função `normalizeHeader` para entender a normalização) à lista do campo correspondente.
3. Se a adquirente tiver uma nomenclatura de modalidade diferente (ex. "Débito à Vista", "Crédito Rotativo"), ajuste as expressões regulares em `classifyRow`.
4. Descreva no PR qual adquirente você testou e, se possível, anexe um exemplo de arquivo **anonimizado** (sem dados reais de clientes/transações).

## Reportando bugs

Use o template de "Bug report" ao abrir uma issue e, se puder, inclua uma planilha de exemplo com dados fictícios que reproduza o problema.

## Código de conduta

Seja respeitoso. Este é um projeto pequeno mantido nas horas vagas.
