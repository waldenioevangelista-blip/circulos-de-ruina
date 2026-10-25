# Círculos de Ruína — Pacote de Assets de Desenvolvimento

Pacote padronizado de referências visuais geradas para o projeto.

## Estrutura

- `assets/source/generated/` — PNGs-fonte gerados. Os nomes originais são preservados para rastreabilidade.
- `previews/` — pranchas de contato para consulta visual rápida.
- `docs/inventario_tecnico.csv` — número, nome de arquivo, resolução e tamanho.
- `docs/manifest.json` — metadados, SHA-256, caminho e origem de cada arquivo.
- `docs/NAMING.md` — padrão obrigatório para novos assets aprovados.

## Convenções vigentes

1. Não editar o arquivo-fonte: crie uma variação versionada.
2. Todo asset novo precisa entrar no manifesto e no índice visual.
3. Assets aprovados devem seguir: `[dominio]_[categoria]_[assunto]_[variante]_vNN.ext`.
4. Domínios: `ui`, `unit`, `arena`, `board`, `vfx`, `icon`, `audio`, `promo`.
5. Categorias: `screen`, `portrait`, `concept`, `sprite`, `tileset`, `effect`, `logo`, `sfx`, `music`.
6. Use minúsculas, sem acentos, espaços ou caracteres especiais.

Exemplo: `ui_screen_colecao_mobile_v01.png`
