# GF Innovation — Portal de Ferramentas Internas

Portal estático em HTML, CSS e JavaScript puro, sem dependências de execução, backend, banco de dados ou processo de build. A entrada central oferece acesso a duas funcionalidades independentes:

- **Assinaturas de e-mail:** gerador existente em `assinaturas/index.html`.
- **Governança Documental:** apresentação e download oficial do plugin v0.2.2, com a Skill `governanca-documental-institucional` v1.1.1 incorporada, em `/governanca/`.

## Gerador de assinaturas

Site estático para criação de assinaturas sem fundo da GF Innovation. A assinatura gerada não define cor de fundo nem borda externa e **não fixa cores de texto ou hyperlinks**; permite que a apresentação herde a cor do tema do cliente de e-mail, semelhante ao modelo de referência. A divisória usa cinza neutro para visibilidade em fundos claros e escuros. O cabeçalho apresenta o logotipo corporativo e permanece visível durante a rolagem em desktop; em telas menores ou baixas, acompanha o fluxo da página para liberar espaço útil. **Não possui backend nem armazena automaticamente os dados informados**. Os dados preenchidos só saem do formulário se o usuário decidir copiá-los para a área de transferência ou baixar o HTML.

## Usar a assinatura

1. Acesse o portal hospedado em HTTPS e selecione **Assinaturas de e-mail**, ou abra diretamente `assinaturas/index.html`.
2. Preencha nome, cargo e e-mail. O telefone com DDD é opcional e recebe máscara `(DD) NNNNN-NNNN` ou `(DD) NNNN-NNNN`. O endereço está dividido em campos, mas a assinatura permanece em duas linhas.
3. Revise o site e os links das três redes sociais pré-preenchidos. URLs e e-mail são validados antes da exportação/cópia.
4. Use os controles **Claro/Escuro** na prévia para simular a aparência da assinatura. Essa simulação não acompanha a assinatura copiada. Clique em **Copiar assinatura**, abra o [Outlook Web](https://outlook.office.com/mail/) e entre em **Configurações → Contas → Assinaturas**. Crie/edite a assinatura e cole com `Ctrl+V`.
5. Se a cópia automática for bloqueada pelo navegador, o conteúdo fica selecionado para cópia manual com `Ctrl+C`. O botão **Baixar HTML (alternativa)** gera uma página independente para selecionar e copiar a assinatura formatada. **O Outlook Web não importa esse HTML como arquivo.**
6. Salve a assinatura e envie um e-mail de teste, conferindo imagens, telefone e links.

## Hospedagem e implantação — GitHub Pages

O portal está publicado em [johanngf.github.io/gf_ferramentas_internas](https://johanngf.github.io/gf_ferramentas_internas/), pelo **GitHub Pages**. A página de Governança é [gf_ferramentas_internas/governanca/](https://johanngf.github.io/gf_ferramentas_internas/governanca/).

Configuração real reconsultada pela API do GitHub Pages em **23/11/2026**:

- Origem de publicação: branch **`master`**, diretório **`/` (raiz)**.
- Publicação a partir de branch (`build_type: legacy`); não há workflow adicional de deploy criado neste projeto.
- HTTPS habilitado, sem domínio personalizado; estado `built`. Último build publicado: commit `30a06bda7cdde2a2a9447f43b40523c9b5b2559c`.
- Página inicial e `/governanca/` responderam HTTP 200 na URL atual; o site publicado ainda representa a versão anterior, pois esta atualização permanece local.

O site utiliza HTML, CSS e JavaScript estáticos, sem processo de build da aplicação. O arquivo `.nojekyll` é preservado para servir o conteúdo sem processamento Jekyll. Node e npm são utilizados somente nas ferramentas locais de lint e formatação.

Em **Settings → Pages → Build and deployment**, a origem correspondente é **Deploy from a branch**, branch `master`, pasta `/(root)`. Esta revisão apenas consultou a configuração; não a modificou. Mudanças do portal só devem chegar à branch de produção após revisão e autorização. Não é necessário adicionar pipeline, GitHub Actions ou serviço de deploy.

Os caminhos de navegação, CSS, scripts e imagens são relativos para funcionar sob o prefixo atual `/gf_ferramentas_internas/` e em servidor HTTP local. A referência anterior a `/gf_email_assinaturas/` é histórica, não a URL vigente consultada. Preserve os caminhos públicos das imagens usadas pelas assinaturas. Cloudflare Pages não é a hospedagem efetiva deste portal.

## Arquivos

```text
index.html                      Entrada central e navegação do portal
assinaturas/
  index.html                    Formulário, prévia e instruções para Outlook
  assinaturas.css               Estilos específicos do gerador
  assinaturas.js                Máscaras, validações, cópia e exportação
governanca/
  index.html                    Apresentação e download versionado do plugin
  governanca.css                Composição específica da página
shared/
  base.css                      Identidade visual e elementos comuns às três páginas
assets/
  imagens/
    logo.png                    Logotipo com URL pública preservada
    facebook.png                Ícone com URL pública preservada
    instagram.png               Ícone com URL pública preservada
    linkedin.png                Ícone com URL pública preservada
eslint.config.mjs               Regras de lint JavaScript com Prettier integrado
.prettierrc.json                 Convenções de formatação
.prettierignore                  Exclusões da formatação
.vscode/                        Correções ao salvar e extensões recomendadas
package.json                    Scripts e dependências de desenvolvimento
package-lock.json               Versões reproduzíveis das dependências
README.md                       Documentação
.nojekyll                       Compatibilidade GitHub Pages
.gitignore                      Exclusões do repositório
```

As URLs de navegação são `/`, `/assinaturas/` e `/governanca/`, com o servidor estático servindo o `index.html` de cada diretório. Os links são relativos para preservar a publicação sob subdiretórios; não há roteamento JavaScript nem regras adicionais de reescrita. Os endereços antigos com `index.html` continuam acessíveis. Para navegar pelas URLs de diretório, use um servidor HTTP local ou a hospedagem estática. Os módulos usam navegação HTML convencional. O JavaScript e o CSS do gerador são carregados somente em `assinaturas/index.html`. As três páginas carregam `shared/base.css`, que concentra cores, tipografia, navegação, botões, cartões e rodapé. Os estilos de formulário, prévia e instruções ficam em `assinaturas/assinaturas.css`; a composição de Governança Documental fica em `governanca/governanca.css`. A página inicial reutiliza a base, sem CSS exclusivo. A navegação HTML é repetida localmente nas três páginas, sem JavaScript, templates dinâmicos ou dependências externas.

### Caminhos e compatibilidade

As imagens permanecem em `assets/imagens/`, sem cópias adicionais, porque assinaturas já distribuídas podem referenciar suas URLs públicas. Preserve também o domínio e o prefixo de publicação existentes. O gerador acessa essas imagens por `../assets/imagens/`, compatível com publicação na raiz ou em subdiretório. Na cópia e na exportação em HTTP/HTTPS, os caminhos são convertidos para URLs absolutas; em abertura local por `file:`, mantém-se a alternativa com imagens incorporadas em base64.

A raiz agora abre o portal; o gerador está em `assinaturas/index.html`. Os arquivos antigos `assets/app.js` e `assets/style.css` foram transferidos para o módulo. As tabelas e os estilos inline da assinatura foram mantidos. A navegação para outra página não salva os campos preenchidos, como já ocorria ao sair do editor.

### Execução local

Na raiz do repositório, se Python 3 estiver disponível, execute:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Abra `http://localhost:8000/`. As entradas diretas são `http://localhost:8000/assinaturas/` e `http://localhost:8000/governanca/`. Encerre com `Ctrl+C`. Não é necessário instalar pacotes. Também é possível abrir o HTML diretamente, mas a cópia automática depende das permissões do navegador; valide a distribuição em HTTPS e o resultado real no Outlook.

### Lint, formatação e VS Code

Use Node.js `^20.19.0`, `^22.13.0` ou `>=24` e instale as dependências de desenvolvimento com:

```sh
npm ci
```

Os pacotes são exclusivamente de desenvolvimento; o portal continua estático e sem build.

```sh
npm run lint          # Verifica JavaScript com ESLint, incluindo Prettier
npm run lint:fix      # Corrige problemas automaticamente quando possível
npm run format       # Formata HTML, CSS, JavaScript, JSON e Markdown
npm run format:check # Verifica formatação sem alterar arquivos
npm run check        # Executa lint e verificação de formatação
```

No VS Code, instale/habilite as extensões recomendadas em `.vscode/extensions.json`: **ESLint** (`dbaeumer.vscode-eslint`) e **Prettier** (`esbenp.prettier-vscode`). Abra a raiz deste repositório como pasta de trabalho. As configurações são locais ao projeto e não modificam preferências globais do editor.

Ao salvar JavaScript, `source.fixAll.eslint: always` aplica as correções do ESLint, incluindo a formatação pelo plugin do Prettier. O formatador separado é desabilitado para JavaScript para evitar dois processos de formatação no mesmo salvamento. HTML, CSS, JSON e Markdown usam o Prettier como formatador ao salvar. Problemas sem correção automática continuam aparecendo no painel de problemas. A recomendação de extensões não as instala automaticamente.

A [configuração oficial da Rocketseat](https://github.com/Rocketseat/eslint-config-rocketseat) existe, mas sua versão publicada `2.2.2` depende de ESLint 8 e inclui plugins React/TypeScript. Em vez de carregar essas dependências, a configuração local usa ESLint 10 com flat config e adapta as [convenções de React da Rocketseat](https://github.com/Rocketseat/eslint-config-rocketseat/blob/main/react.js) pertinentes ao JavaScript puro: dois espaços, aspas simples, sem ponto e vírgula, vírgula final, parênteses em funções de seta e largura de 80 caracteres. Não são aplicadas regras de JSX, React ou TypeScript. A configuração também verifica erros comuns, igualdade estrita, variáveis não utilizadas e preferência por `const`.

As regras de formatação ficam em `.prettierrc.json`, utilizadas tanto pelo editor quanto pelo ESLint via `eslint-plugin-prettier/recommended`. Foi adotado LF para finais de linha reproduzíveis. `embeddedLanguageFormatting: off` impede reformatação de código embutido em templates, preservando o HTML das assinaturas geradas; `bracketSameLine: true` mantém o `>` na linha do último atributo; `htmlWhitespaceSensitivity: ignore` permite aplicar essa apresentação sem que o Prettier desloque o delimitador para preservar espaços entre tags. As páginas HTML são reformatadas, mas os templates JavaScript das assinaturas continuam preservados. O plugin `prettier-plugin-css-order` organiza as propriedades dos arquivos CSS em ordem alfabética crescente (`cssDeclarationSorterOrder: alphabetical`), inclusive ao salvar. `cssDeclarationSorterKeepOverrides: true` preserva a precedência quando propriedades abreviadas e específicas dependem da ordem. ESLint analisa JavaScript; HTML e CSS recebem formatação, sem análise semântica por um linter específico.

Na implantação dessas ferramentas, `npm run check` passou sem erros. Uma verificação em memória confirmou a correção conjunta de ESLint/Prettier e a detecção de variáveis indefinidas. Os testes locais no Chrome descritos abaixo foram repetidos após a formatação: a cópia formatada e o HTML exportado permaneceram idênticos aos anteriores. O acionamento pelo salvamento na interface do VS Code não foi testado nesta execução.

### Publicação existente

A hospedagem efetiva é GitHub Pages, com origem na raiz de `master`, conforme a configuração verificada na seção de implantação. A navegação em diretórios (`/assinaturas/` e `/governanca/`) é relativa à raiz publicada do repositório. Esta revisão permanece em branch local própria e não altera a publicação nem a configuração de hospedagem.

### Distribuição atual — Plugin v0.2.2 / Skill v1.1.1

A página `/governanca/` aponta diretamente ao **ZIP original do plugin**, hospedado no repositório `johanngf/plugin_governanca_documental`. Não há cópia do pacote no portal, API intermediária, script de download nem ZIP derivado.

- [Release oficial v0.2.2](https://github.com/johanngf/plugin_governanca_documental/releases/tag/v0.2.2), pública, estável e confirmada como Latest no GitHub em 23/11/2026. Essa marcação não comprova publicação no Diretório de Plugins do ChatGPT.
- [Instalável exato e versionado](https://github.com/johanngf/plugin_governanca_documental/releases/download/v0.2.2/Governanca_Documental_Plugin_Importavel_v0.2.2_ESTAVEL.zip): `Governanca_Documental_Plugin_Importavel_v0.2.2_ESTAVEL.zip`, **313.955 bytes**.
- SHA-256: `dc5fab000eb67e8a0efcabc6681ea80e73fe3c845b394793f703ac7fc2ac4b4c`.
- Commit da tag anotada `v0.2.2`: `b93245ae1a8667d451d64436103e8be3b1120bd1`.
- [CI do commit aprovado](https://github.com/johanngf/plugin_governanca_documental/actions/runs/44599404522): concluído com sucesso, com evidência histórica de 59 testes aprovados, 1 ignorado e nenhuma falha. Esta atualização do portal não reexecuta a suíte do plugin.
- [Documentação versionada](https://github.com/johanngf/plugin_governanca_documental/blob/v0.2.2/README.md). Os arquivos automáticos Source code (zip/tar.gz) não substituem o instalável acima; o botão não usa `/releases/latest` nem URL transitória.

O ZIP contém 31 arquivos sob `governanca-documental-plugin/`, incluindo os manifestos `plugin.json` e `.codex-plugin/plugin.json`, a Skill 1.1.1 e seus recursos. Os quatro DOCX canônicos são Contrato Operacional 0.8, Padronização Documental 3.5, Qualidade e Construção de Conteúdo 1.3 e Modelo Formal do Workflow 0.5. Markdown é consulta auxiliar; a Skill aplica as normas e não é uma quinta norma. O portal é referência complementar e não é necessário para executar o plugin.

### Instalação, atualização e limites

A [documentação oficial de plugins do ChatGPT](https://help.openai.com/pt-br/articles/20001256-plugins-in-chatgpt), consultada em 23/11/2026, descreve upload pelo Console de administração para proprietários/administradores habilitados. O portal usa esse procedimento condicionado à disponibilidade. A [documentação de Skills](https://help.openai.com/pt-br/articles/20001066-skills-in-chatgpt) descreve outro fluxo, para Skill isolada; ele não é apresentado como instalação deste plugin.

O responsável informou em 24/11/2026 que testou o plugin no Claude com sucesso. O portal orienta usar o mesmo ZIP oficial v0.2.2 no ChatGPT e no Claude. O Codex não realizou teste independente de instalação ou execução nessas plataformas nesta correção. A disponibilidade depende da conta, do workspace, das permissões e da plataforma.

O acordeão do ChatGPT começa aberto e o do Claude começa fechado. Para atualizar, recomendamos desinstalar ou remover a versão anterior do plugin e repetir o processo normal de instalação com o ZIP atual.

A auditoria OOXML é parcial; a execução portátil depende de leitura íntegra, escrita, Python e acesso aos bytes do DOCX no host. A Skill não substitui controle, validação ou aprovação humana. Não há certificação universal, garantia de acionamento implícito ou nova homologação de Word para Web nesta etapa. O uso é institucional, com direitos reservados; acesso público não concede licença irrestrita de uso, modificação ou redistribuição.

### Abertura dos links do portal

Os links externos das três páginas, incluindo o botão de download, usam `target="_blank"` e `rel="noopener noreferrer"`. O navegador pode iniciar o download diretamente. Os links entre páginas do portal, o link de salto para o conteúdo e outros fragmentos da mesma página permanecem na aba atual. Os links da assinatura gerada, inclusive os da prévia, seguem o comportamento do gerador e de seus formatos de cópia e exportação.

### Histórico — validação da atualização do portal para v0.2.2

Base local: `master` / `origin/master` em `30a06bda7cdde2a2a9447f43b40523c9b5b2559c`, limpa antes da edição. Branch de trabalho: `feat/atualizar-portal-governanca-plugin-v0.2.2`. Naquela etapa, a configuração de Pages foi consultada e a preparação permaneceu local.

As dependências de validação foram instaladas com `npm ci --cache /tmp/gf-governanca-plugin-v022-review-wmi4ijoi/npm-cache`, sem alterar `package-lock.json`. O npm apontou três vulnerabilidades moderadas nas dependências de desenvolvimento existentes; não foi executado `npm audit fix` nem adicionada dependência. O portal continua sem dependências de runtime.

Critérios para repetir a revisão: executar `npm ci` e `npm run check`; servir a raiz por HTTP; conferir a página inicial e Governança em 1280, 768, 390 e 320 px, na raiz e sob `/gf_ferramentas_internas/`; validar headings, IDs, `aria-current`, links relativos, imagens, ausência de overflow global, abertura dos acordeões e do hash por teclado, foco visível e navegação. O botão deve conservar o endereço versionado acima. O SHA-256 deve quebrar dentro do cartão e permanecer selecionável, sem JavaScript adicional.

Resultados observados nesta atualização: `npm run check` aprovado; Chrome headless 158.0.8127.36 com servidor HTTP local, 16 combinações de página/largura/prefixo e oito percursos de teclado aprovados. Sem overflow horizontal global, recursos locais com erro ou exceções JavaScript. Link de salto, Tab, foco visível sem encobrimento e abertura/fechamento dos três controles nativos por Enter/Espaço conferidos. A árvore de acessibilidade mostrou os estados de expansão esperados. Capturas produzidas nas quatro larguras, com inspeção visual adicional em 1280 e 320 px; o hash aberto permaneceu dentro do cartão.

Quatro destinos externos da página retornaram HTTP 200, incluindo o ZIP e a documentação de plugins. A página HTML do README versionado retornou HTTP 503 nas duas tentativas deste ambiente; a conexão GitHub confirmou o arquivo na tag v0.2.2. Essa limitação de acesso externo não foi tratada como download aprovado nem ocultada por troca de URL. A consulta da documentação não constitui observação da interface autenticada do ChatGPT.

O script temporário e as evidências estão em `/tmp/gf-governanca-plugin-v022-review-wmi4ijoi/`, fora do conteúdo publicado. Enquanto disponíveis nesta sessão, os testes de navegador podem ser repetidos com Chrome e o módulo Python `websocket` já instalado:

```sh
python3 /tmp/gf-governanca-plugin-v022-review-wmi4ijoi/validate_browser.py --repo "$PWD" --output /tmp/gf-governanca-plugin-v022-review-wmi4ijoi
```

Não houve teste com leitor de tela, outros navegadores, importação do plugin ou nova homologação institucional. No gerador de assinaturas foi verificada somente a navegação e a inicialização; os fluxos de cópia/exportação não foram reexecutados. Seus arquivos, assets, a base compartilhada, o cartão de Assinaturas e o lockfile permaneceram inalterados. Na data daquela validação, a atualização ainda estava local. A atualização para o plugin 0.2.2 foi publicada posteriormente em `master` no commit `a370a9a2f7c8d7d189d6de3ded24a2711105a40c`. A correção dos hyperlinks e da orientação do Claude está em revisão local.

O download anônimo real do asset foi realizado com Python/urllib, seguindo redirecionamentos; os bytes recebidos tinham exatamente **313955 bytes** e SHA-256 esperado. Não se trata apenas de conferência de metadados. O arquivo e as evidências locais ficam em `/tmp/gf-governanca-plugin-v022-review-wmi4ijoi/`, fora do repositório publicado. Para reconferir o arquivo já baixado nesta sessão:

```sh
wc -c /tmp/gf-governanca-plugin-v022-review-wmi4ijoi/Governanca_Documental_Plugin_Importavel_v0.2.2_ESTAVEL.zip
sha256sum /tmp/gf-governanca-plugin-v022-review-wmi4ijoi/Governanca_Documental_Plugin_Importavel_v0.2.2_ESTAVEL.zip
```

### Histórico — Skill independente v1.0.0

A [release v1.0.0](https://github.com/johanngf/plugin_governanca_documental/releases/tag/v1.0.0) e seu asset `governanca-documental-institucional-v1.0.0.zip` permanecem preservados. Tamanho histórico: 248.808 bytes; SHA-256 `68c408e8c8b5af7da1198856ffc4736d8df4e1f442b4177930f4a1918cd0c085`; commit `589a2970b9dab38859a00bb9eff3810881eafde6`. Eles não representam a distribuição corrente do plugin.

Os cenários [H00–H07 e suas ressalvas](https://github.com/johanngf/plugin_governanca_documental/blob/v1.0.0/tests/HOMOLOGACAO.md) se referem à Skill independente e ao ambiente então testado. O fluxo antigo de upload de Skill e a análise estática de compatibilidade com Claude não comprovam a interface, aceitação ou instalação atual do plugin 0.2.2. Nenhuma adaptação ou reempacotamento foi realizado para o portal.

Os registros abaixo preservam as verificações anteriores. Na revisão histórica dos acordeões foi usada a branch `feat/revisao-governanca-acordeoes`, com foco desktop; as afirmações e contagens seguintes pertencem àquela etapa, não a uma nova homologação do plugin.

### Histórico — validação desktop e dos acordeões

Nesta revisão local, foram verificadas as resoluções **1280 × 720**, **1366 × 768**, **1440 × 900** e **1920 × 1080**, na raiz do servidor e sob `/portal/`, em Chrome headless com contexto anônimo:

- Dois cartões alinhados, sem rolagem horizontal global, com o botão de download visível na área inicial.
- ChatGPT inicialmente aberto e Claude fechado; abertura e fechamento por mouse, Enter e Espaço, sem JavaScript na página.
- Estado de expansão dos controles nativos conferido na árvore de acessibilidade do navegador; navegação por Tab com foco visível, sem encobrimento pelo cabeçalho nos percursos testados.
- Cartão de instalação reduz sua altura quando os acordeões estão fechados, sem altura mínima artificial.
- Download efetivo pelo botão: arquivo oficial de 248.808 bytes e SHA-256 esperado, após redirecionamentos do GitHub, sem login.
- Todos os cinco destinos externos distintos da página retornaram HTTP 200, incluindo a documentação do Claude.
- Navegação da página inicial para Governança e depois para Assinaturas conferida, com inicialização do gerador e sem exceções JavaScript não tratadas.
- `npm run check` executado. Página inicial, arquivos do gerador, base compartilhada, imagens e configurações de desenvolvimento preservados; o breakpoint existente de 900 px foi mantido sem novos breakpoints.

Capturas desktop e resultados temporários da sessão estão em `/tmp/gf-governanca-revisao/`, fora do conteúdo publicado. A configuração de GitHub Pages foi consultada somente para leitura; não foi alterada.

Não foram realizados testes de instalação ou execução no Claude, nova homologação no ChatGPT, testes com leitores de tela ou outros navegadores. O foco desta revisão foi desktop; não houve redesenho nem validação visual específica para mobile. Nenhum commit, push, PR, merge ou publicação foi executado.

### Validação anterior da integração da distribuição

Registro da etapa de integração anterior à revisão dos acordeões. Verificações da integração executadas em Chrome headless com contexto anônimo, servidor HTTP local e scripts temporários externos ao repositório:

- Layout, navegação entre as três páginas, links e recursos locais verificados em 1280, 768, 390 e 320 px, tanto na raiz quanto sob `/portal/`, sem rolagem horizontal global.
- Navegação por Tab, foco visível sem encobrimento e abertura da seção nativa de integridade por Enter verificados. O SHA-256 quebra em múltiplas linhas no celular sem extrapolar o contêiner.
- Botão da página efetivamente clicado no navegador: download concluído após os redirecionamentos do GitHub, sem autenticação, com o nome esperado, 248.808 bytes e SHA-256 correspondente ao pacote oficial.
- Os cinco destinos oficiais distintos (ZIP, documentação, homologação, release e histórico) retornaram HTTP 200 em verificação anônima independente.
- Página inicial sem o aviso antigo de preparação e sem download direto; página de Governança sem scripts novos ou URLs dinâmicas de distribuição. Nenhuma exceção JavaScript não tratada foi observada.
- Gerador de assinaturas, imagens, cabeçalhos, navegação compartilhada, `shared/base.css` e ferramentas de desenvolvimento preservados. Não foram adicionadas dependências nem copiados pacotes para o portal.
- `npm run check` executado. Capturas e resultados temporários disponíveis na sessão em `/tmp/gf-governanca-integration/`, fora dos arquivos publicados.

Os testes não representam nova homologação da Skill. A instalação em contas individuais, leitores de tela, outros navegadores e a hospedagem de produção do portal não foram verificados nesta etapa. Esses resultados se referem à etapa de integração registrada anteriormente; não equivalem à validação da instalação em outras plataformas.

### Template visual e validação anterior à integração

A paleta institucional foi preservada: marinho `#041B44`, ação `#0872D3`, fundo `#F4F7FB`, texto `#172439` e divisórias `#DAE2EC`. A tipografia do portal prioriza Segoe UI e fontes do sistema, com corpo de 16 px, título principal de 28 px, títulos de cartões de 20 px e rótulos de 14 px. O HTML gerado para e-mail conserva suas próprias dimensões, fontes e estilos inline.

O cabeçalho compartilhado tem navegação com `aria-current="page"`, link para pular ao conteúdo e foco visível. Ele permanece sticky em desktop, passando a estático até 900 px de largura ou 600 px de altura. A prévia é uma região acessível por teclado e tem rolagem horizontal própria quando necessário. As instruções e advertências do gerador permanecem abertas e visíveis.

Registro da etapa de template visual, anterior à integração do download oficial. Verificações executadas em Chrome headless, com servidor HTTP local e scripts temporários externos ao repositório:

| Verificação                             | Resultado                                                                                                                                  |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Três páginas em 1280, 768, 390 e 320 px | Sem rolagem horizontal global; navegação e conteúdo utilizáveis                                                                            |
| Layout do gerador                       | Duas colunas no desktop de 1280 px; uma coluna nas demais larguras testadas                                                                |
| Prévia em mobile                        | Rolagem horizontal limitada ao contêiner; assinatura mantém a largura original                                                             |
| Teclado                                 | Link de salto funcional; controles acessíveis por Tab, com foco visível e sem encobrimento pelo cabeçalho nos percursos testados           |
| Formulário e navegação                  | Todos os inputs com label; um h1 e um link ativo por página; botões e links de navegação com altura mínima de 44 px                        |
| Contraste do texto do portal            | Mínimo medido de 4,82:1; sem falhas nos pares de texto/fundo examinados nas quatro larguras (excluídos assinatura e controle desabilitado) |
| Ampliação                               | Refluxo em 320 px; teste adicional com fonte raiz ampliada de 16 para 32 px em viewport de 768 px                                          |
| Gerador antes/depois                    | Prévia, HTML exportado e conteúdos HTML/texto da cópia nativa idênticos para os mesmos dados                                               |
| Funcionalidades do gerador              | Máscaras, validações, tema da prévia, imagens, alternativa de seleção manual e exportação verificadas                                      |
| Caminhos                                | Acesso direto, links e recursos locais na raiz e sob `/portal/`; abertura `file:` com imagens base64 e botão de seleção do HTML exportado  |
| Governança Documental                   | Sem URLs fictícias, scripts novos ou arquivos da Skill; download desabilitado                                                              |
| Qualidade                               | `npm run check` executado; sem exceções JavaScript não tratadas nos testes de navegador                                                    |

O contraste foi avaliado tendo como referência o [critério de contraste da WCAG 2.2 AA](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html); foco e tamanho dos controles seguem as referências de [foco não encoberto](https://www.w3.org/WAI/WCAG22/Understanding/focus-not-obscured-minimum.html) e [tamanho mínimo de alvo](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html). Essas verificações não constituem auditoria completa de conformidade: leitores de tela, zoom real da interface do navegador, outros navegadores, Outlook real e produção não foram testados. A alternativa assíncrona de clipboard não foi exercitada; seu código foi preservado.

Foram produzidas capturas comparativas de antes/depois em desktop e do novo template nas quatro larguras. Os artefatos temporários da sessão ficam em `/tmp/gf-visual-captures/`, fora dos arquivos publicados.

### Validação da migração

A migração foi comparada com uma cópia anterior dos arquivos em Chrome headless, usando servidor HTTP local na raiz e sob o prefixo `/portal/`, além de abertura por `file:`. Não foram instaladas dependências para essa validação.

- HTML exportado e conteúdos HTML/texto da cópia formatada idênticos aos da versão anterior para os mesmos dados. Na prévia, a única diferença comparada foi o caminho relativo das imagens.
- Verificados campos obrigatórios, telefone opcional, máscaras de telefone fixo/celular e CEP, normalização de UF, e-mail inválido, URL insegura, domínio de rede social e escape de texto.
- Verificados atualização da prévia, alternância claro/escuro sem mudança na assinatura, carregamento das imagens, cópia formatada pelo evento nativo e seleção manual com cópia automática indisponível.
- Verificados geração do Blob de download, imagens base64 na abertura local e botão de seleção no HTML exportado.
- Verificados navegação e acesso direto aos módulos, layout em larguras de 1280 e 390 pixels e ausência de exceções JavaScript não tratadas. Os quatro PNGs permaneceram idênticos byte a byte.

Os testes foram pontuais, com script temporário externo ao repositório; não há suíte automatizada instalada. A permissão e o resultado da alternativa assíncrona `navigator.clipboard.write`, outros navegadores, a colagem/envio/recebimento no Outlook e a hospedagem de produção não foram validados. A equivalência observada não garante comportamento idêntico em todos os clientes de e-mail.

## Privacidade, segurança e compatibilidade

- O editor não contém chamadas para salvar, transmitir ou registrar dados dos campos. Não utiliza `localStorage`, cookies analíticos nem banco de dados.
- Copiar a assinatura coloca o conteúdo escolhido na área de transferência; baixar o HTML grava um arquivo **somente por solicitação explícita**.
- Imagens copiadas do site hospedado são referenciadas por URLs públicas. O domínio deve permanecer acessível enquanto as assinaturas estiverem em uso.
- Se o navegador bloquear a cópia automática, siga a orientação para copiar manualmente ou exportar o HTML. O comportamento de imagens e estilos também depende do Outlook e do cliente de e-mail do destinatário.
- A máscara de telefone suporta números brasileiros com DDD e 10/11 dígitos; CEP tem oito dígitos; links sociais só aceitam domínios da própria rede e HTTPS. Validações são básicas, não verificam existência das contas ou do endereço.

Documentação: [Microsoft — Assinaturas](https://support.microsoft.com/en-us/outlook/training/sign-in-and-create-a-signature-for-outlook-on-the-web), [MDN — Clipboard API](https://developer.mozilla.org/en-US/docs/Web/API/Clipboard_API), [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

## Assinatura com contraste adaptável (v9)

- O HTML copiado/exportado não define `background`, `background-color` nem `bgcolor` nas tabelas da assinatura, e não possui borda externa. A área branca da prévia é apenas uma superfície de demonstração no editor.
- Textos e links foram configurados para herdar a cor do tema do cliente de e-mail (`color:inherit` nos links e nenhuma cor explícita nas células), em vez de possuir valores rígidos de azul-escuro. Em Outlook Web, as cores podem mudar conforme o modo de visualização, mas essa herança **não é garantia universal**: o Outlook pode reformatar HTML e cada cliente apresenta regras próprias.
- Logotipo e ícones PNG existentes foram preservados com transparência; não se alterou o logotipo original.
- O cabeçalho fixo da aplicação continua azul-escuro e não faz parte da assinatura enviada.

### Prévia claro/escuro e limitações

- Os botões **Claro/Escuro** alteram apenas a superfície de teste do editor; o HTML copiado não recebe classes ou scripts da prévia.
- A assinatura não contém `color:#...` ou `background-color` nos blocos de texto. A cor é herdada da mensagem e pode ser modificada pelo Outlook.
- A logomarca PNG e os ícones de redes sociais mantêm suas cores institucionais; eles **não mudam automaticamente** de tonalidade. A divisória neutra permanece visível nas duas aparências.
- O modo escuro do Outlook é controlado pelo aplicativo e pode modificar a forma de exibição, inclusive de cores explicitamente definidas; portanto teste **envio e recebimento reais** nos temas claro e escuro.

Fonte oficial: https://support.microsoft.com/pt-br/outlook/mail/dark-mode-in-outlook

### Histórico — revisão editorial enxuta

A revisão manteve o template original, remeteu os detalhes normativos à release e orientou invocar o plugin explicitamente na conversa. A recomendação de atualização vigente está na seção Instalação, atualização e limites.

### Histórico — revisão v3 do Claude

A v3 registrou a declaração do responsável sobre o funcionamento no Claude, sem ensaio independente. O download direto foi reconferido (313.955 bytes, SHA-256 esperado e 31 arquivos). O inventário do ZIP registrou a ausência de `.claude-plugin/plugin.json`. A análise estática da época levou à retirada provisória das etapas de upload e à suspensão da revisão para PR. O teste informado em 24/11/2026 superou essa decisão editorial.

### Histórico — revisão v4 do Claude

A v4 restaurou as cinco etapas de instalação e publicou uma ressalva sobre o manifesto ausente no ZIP. Após o teste informado pelo responsável em 24/11/2026, a orientação vigente passou a indicar o mesmo ZIP oficial para as duas plataformas. O pacote e a release foram preservados em todas essas revisões.
