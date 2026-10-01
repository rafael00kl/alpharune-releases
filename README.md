# AlphaRune — downloads oficiais do projeto

## Origem e créditos

Esta versão modificada do AlphaRune foi construída inicialmente sobre a **base completa de [chorlick/alpharune](https://github.com/chorlick/alpharune)**: engine C++, arquitetura, implementações de cartas, regras, testes e ferramentas. O crédito por essa base pertence ao projeto original de **chorlick** e aos seus contribuidores. O nosso trabalho preserva o histórico recebido e acrescenta as customizações locais, cliente/interface, auditoria, versionamento, instalação e updates.

O dataset de **[LouisCourrian/riftbound-cards](https://github.com/LouisCourrian/riftbound-cards)** é a fonte auxiliar de metadata, textos, IDs, sets e URLs de imagens usada na comparação e auditoria de cartas. Crédito a LouisCourrian e aos contribuidores. Ele é mantido separadamente e não implementa regras/cartas automaticamente na engine.

Riftbound e suas artes pertencem à **Riot Games**. As [cartas oficiais](https://playriftbound.com/en-us/card-gallery/) e [regras oficiais](https://playriftbound.com/en-us/rules/) continuam como referências. O repositório original é acompanhado por upstream somente leitura; mudanças da engine são analisadas antes de qualquer integração. A auditoria consulta a fonte externa semanalmente e também pode ser executada manualmente.


Código do projeto: [rafael00kl/alpharune](https://github.com/rafael00kl/alpharune) (privado, exige acesso).
Este repositório público contém instruções e releases. Não contém o histórico da engine privada.

## Baixar e instalar

- [Baixar AlphaRune-Setup.exe](https://github.com/rafael00kl/alpharune-releases/releases/latest/download/AlphaRune-Setup.exe)
- [Versão estável mais recente e todos os arquivos](https://github.com/rafael00kl/alpharune-releases/releases/latest)
- [Todas as versões e rollback manual](https://github.com/rafael00kl/alpharune-releases/releases)

Execute o Setup no Windows x64. Ele verifica Microsoft Edge, prepara Ubuntu 26.04 no WSL quando necessário, instala as bibliotecas de runtime, baixa a última versão estável, verifica SHA-256 e cria atalhos. A instalação do WSL pode pedir permissão de administrador e reboot; execute o Setup novamente depois de reiniciar. Se Edge não estiver disponível, instale-o pelo site oficial indicado pelo Setup.

O instalador usa a release mais recente; não é necessário baixar outro Setup a cada update do jogo. Não há necessidade de autenticação GitHub para baixar os arquivos deste repositório.

Se uma instalação de desenvolvimento já estiver configurada no Windows, o Setup a preserva e instala o cliente de release ao lado dela. O código local não é substituído.

## Atualizar o jogo

O cliente verifica updates ao abrir. Em Settings, use **Check Game Updates** e **Install Update & Restart**. Termine a partida e salve a edição de deck antes de atualizar. O pacote é baixado, validado e preparado separadamente; o novo cliente é verificado antes de ativar a versão. Decks/configurações/cache são preservados, e a versão anterior fica disponível.

A atualização aplica pacotes completos de runtime nesta primeira versão. Não aplica automaticamente novas cartas, mecânicas ou erratas. Um checkout de desenvolvimento não recebe updates de pacote; nele use o fluxo Git/build.

## Arquivos da release

- **AlphaRune-Setup.exe**: primeira instalação/ambiente base, recomendado.
- **AlphaRune.exe**: launcher Windows; sozinho não inclui o runtime do jogo.
- **AlphaRune-v<VERSÃO>-ubuntu-26.04-x86_64.tar.gz**: runtime Linux para WSL/Ubuntu compatível.
- **release-manifest.json**: plataforma, versão, commit de origem, hashes e evidências de validação.
- **SHA256SUMS**: checksums dos artefatos.
- **release-notes.md** e **relatorio.md**: mudanças, validações e limitações.

Releases antigas são preservadas; artefatos publicados não são substituídos. O upstream original não recebe alterações deste projeto.

## Limites da primeira distribuição

Plataforma suportada: Windows x64 + Ubuntu 26.04 x86_64 em WSL + Microsoft Edge.
Os executáveis Windows reais, o cliente empacotado e a engine foram testados em diretórios e portas isolados. A instalação interativa em um Windows limpo sem WSL, incluindo UAC/reboot, ainda precisa de teste de aceitação; o relatório da release detalha esse limite. Não se trata de certificação de todas as cartas.

Logs do backend ficam em `%LOCALAPPDATA%/AlphaRune/logs` ou `AlphaRuneRelease/logs`. Logs de atualização ficam no WSL em `~/.local/share/alpharune/logs/update.log` e `update-status.json`.

[Relatório completo da entrega v0.2.6](RELATORIO-v0.2.6.md), incluindo testes e limitações.
