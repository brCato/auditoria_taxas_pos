# Changelog

Todas as mudanças notáveis deste projeto serão documentadas neste arquivo.

O formato segue [Keep a Changelog](https://keepachangelog.com/pt-BR/1.1.0/), e este projeto adota [Versionamento Semântico](https://semver.org/lang/pt-BR/).

## [1.2.0] - 2026-08-25

### Adicionado
- Deploy estático configurado para **Netlify** via `netlify.toml`.
- Captura de e-mails com **Netlify Forms** antes do download do relatório `.xlsx`.
- Mensagens de status para registro do lead e tratamento de falha no envio.

## [1.1.0] - 2026-08-25

### Adicionado
- Configuração de taxa negociada para **Pix na maquininha** — antes ignorado, agora auditado como as demais modalidades.
- Botão de **download do relatório em `.xlsx`** (resumo executivo + tabela de divergências), liberado após o preenchimento de um e-mail válido.

## [1.0.0] - 2026-08-25

### Adicionado
- Versão inicial: configuração de taxas negociadas (débito, crédito à vista, parcelado 2x–21x) com persistência em `localStorage`.
- Upload de relatório via drag-and-drop ou seleção manual (`.csv` / `.xlsx`).
- Reconhecimento automático de colunas de diversas adquirentes brasileiras.
- Dashboard executivo e tabela de transações divergentes.
