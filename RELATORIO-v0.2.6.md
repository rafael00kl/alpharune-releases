# Relatório AlphaRune v0.2.6

## Downloads e projeto

- **[Baixar o instalador](https://github.com/rafael00kl/alpharune-releases/releases/latest/download/AlphaRune-Setup.exe)** — caminho recomendado para primeira instalação.
- **[Release v0.2.6 e todos os artefatos](https://github.com/rafael00kl/alpharune-releases/releases/tag/v0.2.6)**.
- **[Projeto público de distribuição](https://github.com/rafael00kl/alpharune-releases)** — instruções de instalação e atualização.
- **[Código-fonte privado](https://github.com/rafael00kl/alpharune)** — exige acesso à conta/repositório.
- **[Launcher AlphaRune.exe](https://github.com/rafael00kl/alpharune-releases/releases/download/v0.2.6/AlphaRune.exe)** — depende do runtime instalado; não substitui o Setup.
- **[Checksums](https://github.com/rafael00kl/alpharune-releases/releases/download/v0.2.6/SHA256SUMS)**.
- **[Manifest de versão e validação](https://github.com/rafael00kl/alpharune-releases/releases/download/v0.2.6/release-manifest.json)**.

## Git e segurança

Código atual e histórico preservados. O desenvolvimento ocorreu em codex/card-infra, com checkpoints e pushes ao repositório próprio. PR #1 integrado à master após autorização explícita do usuário. Commit da release: 3943010a7b54bd0d6fc5348a8f645cd4a6da716f. Tag: v0.2.6. VERSION é a fonte única do número 0.2.6.

Origin: rafael00kl/alpharune. Upstream: chorlick/alpharune, somente leitura, com URL de push desabilitada. Nenhum push ao upstream. Nenhuma nova carta ou regra implementada nesta entrega. Builds, relatórios locais, caches e credenciais não entram no Git. O código da engine continua privado; os arquivos de UI/Python necessários ao runtime são naturalmente entregues no pacote.

## Instalador

O novo AlphaRune-Setup.exe é independente do instalador legado, que foi preservado. Ele consulta a última release estável pública, baixa e valida o runtime, instala o launcher e cria atalhos. Uma instalação antiga de desenvolvimento é preservada; o shell de release pode ser instalado ao lado dela em AlphaRuneRelease.

Plataforma desta versão: Windows x64, Ubuntu 26.04 x86_64 no WSL e Microsoft Edge. O Setup pode provisionar Ubuntu/WSL e bibliotecas de runtime (Python/CA/Boost), com permissão administrativa e reboot quando exigidos pelo Windows. Deve ser executado novamente após reboot. Se Edge estiver ausente, é necessário instalá-lo pelo site oficial informado.

O instalador não contém uma versão fixa do jogo. Updates comuns não exigem recriar ou reinstalar o Setup. Instalador de aproximadamente 2,9 MiB, launcher de 7,1 MiB e runtime compactado de 57,8 MiB.

## Cliente e updates

O cliente compara a versão local com a última release estável ao abrir e permite uma consulta manual em Settings. Quando existe uma versão maior, apresenta Install Update & Restart. A instalação exige confirmação, partida encerrada e edição de deck salva.

O pacote é baixado com verificação de SHA-256/tamanho/plataforma e extração segura. A nova versão é preparada em uma pasta separada; após encerramento do cliente antigo, um worker inicia e verifica o novo cliente antes de trocar atomicamente current.json. A janela existente recarrega. Em falha de startup, o cliente anterior é recuperado. As versões anteriores permanecem disponíveis.

Decks, configurações e cache ficam em shared/, separados de versions/. Valores padrão novos não sobrescrevem arquivos do usuário. Preferências do navegador usam perfil persistente. Checkouts de desenvolvimento são recusados pelo aplicador de updates.

Esta primeira entrega aplica pacotes completos de runtime. Alterações C++/cartas compiladas exigem rebuild. UI/scripts/imagens podem futuramente ter entrega data-only com um contrato compatível; isso ainda não é um canal separado implementado. JSON auxiliar não muda regras compiladas automaticamente.

## Testes

No commit final: 1066 testes C++ passaram, com um teste previamente desabilitado; 8 testes do cliente, 11 de auditoria, 7 de integridade/update e 5 de instalação/reinício/recuperação passaram. Coverage e simulações aleatórias também passaram.

Setup.exe e launcher.exe reais foram executados no Windows contra o pacote final em diretórios/portas isolados. O cliente empacotado carregou o registro e serviu uma partida real da engine pela interface HTTP. A transição via API usando engines reais 0.2.5 e 0.2.6 preservou um deck de usuário e a pasta da versão antiga; nesse teste anterior à publicação, apenas a consulta/download remoto foi injetado.

Todos os sete arquivos enviados à release tiveram tamanho e digest SHA-256 conferidos com os arquivos locais. API latest, comparação de versões e download do Setup foram verificados sem autenticação GitHub. O Setup baixado foi executado a partir do Windows TEMP e instalou o runtime pela rede pública em destino isolado; o launcher instalado iniciou 0.2.6 com registro carregado e sem erro. A aplicação/reinício também passou com consulta e download reais sem autenticação; o teste usou o protocolo atual do updater com engine antiga 0.2.5 para verificar preservação de dados, sem simular a rede.

## Card pool

Esta entrega não reimplementou cartas nem fez nova sincronização do dataset. Continua válida a auditoria inicial: 787 registros locais; 693 FULL_CANDIDATE estruturais, 94 PARTIAL, 0 STUB, 190 candidatos MISSING; FULL certificado = 0 por falta de revisão semântica vinculada ao hash; 0 ART_MISSING/ART_BROKEN nas URLs verificadas; 23 CARD_ID_MISMATCH; 8 ERRATA_CHANGED; 189 NEW_OFFICIAL; 977 NEEDS_REVIEW. Categorias se sobrepõem e não são contagem de bugs confirmados.

Fonte auxiliar: LouisCourrian/riftbound-cards, snapshot v2026-09-29, mantido fora do AlphaRune em ~/projects/riftbound-cards. As 845 URLs locais distintas verificadas responderam corretamente no checkpoint inicial. Nenhuma errata foi aplicada automaticamente.

## Limitações de validação

Instalação interativa em Windows limpo sem WSL, incluindo UAC/reboot, e aceitação visual no navegador ainda não foram exercitadas. O teste de executáveis/public download utiliza um Windows com WSL já disponível e destinos isolados. Não é certificação de todas as cartas nem suporte a Windows ARM64/outros Ubuntu.

O CI remoto da master realiza uma verificação adicional em Ubuntu 24.04; ainda estava em execução ao concluir este relatório, acompanhe [execução do CI](https://github.com/rafael00kl/alpharune/actions/runs/36802757328). O pacote público Ubuntu 26.04 foi compilado e totalmente validado localmente, com evidências e hashes no manifest. Não confundir o artefato de desenvolvimento do CI em Ubuntu 24.04 com o runtime público desta release.
