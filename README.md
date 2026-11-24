# 🗺️ Gerador de Declaração de Reconhecimento de Limite (Anuência de Confrontantes)

Aplicação web desenvolvida para agilizar a elaboração de **Declarações de Reconhecimento de Limite (Anuência de Confrontantes)** em processos de georreferenciamento de imóveis rurais (INCRA / SIGEF) e retificação de registro imobiliário, em conformidade com a **Lei nº 10.267/2001** e o **art. 213, § 10 da Lei nº 6.015/1973 (Lei de Registros Públicos)**.

## 📋 Índice

* [Sobre o Projeto](#-sobre-o-projeto)
* [Privacidade e Conformidade com a LGPD](#-privacidade-e-conformidade-com-a-lgpd)
* [Principais Funcionalidades](#-principais-funcionalidades)
* [Manual de Utilização](#-manual-de-utilização)
  * [1. Barra Superior e Gestão de Projetos](#1-barra-superior-e-gestão-de-projetos)
  * [2. Empresa, Logotipo e Responsável Técnico (RT)](#2-empresa-logotipo-e-responsável-técnico-rt)
  * [3. Imóvel Objeto (IMÓVEL 2) e Proprietários](#3-imóvel-objeto-imóvel-2-e-proprietários)
  * [4. Confrontantes (IMÓVEL 1), Co-proprietários e Múltiplos Trechos](#4-confrontantes-imóvel-1-co-proprietários-e-múltiplos-trechos)
  * [5. Importação de Coordenadas (Excel, QGIS e AutoCAD)](#5-importação-de-coordenadas-excel-qgis-e-autocad)
  * [6. Pré-visualização A4 e Exportação (Individual ou em Lote)](#6-pré-visualização-a4-e-exportação-individual-ou-em-lote)
* [Padrão Técnico e Legal dos Documentos Gerados](#-padrão-técnico-e-legal-dos-documentos-gerados)
* [Autoria e Incentivo](#-autoria-e-incentivo)

## 🎯 Sobre o Projeto

Na rotina de agrimensura, topografia e regularização fundiária, a redação manual de cartas de anuência para dezenas de confrontantes — muitas vezes envolvendo condôminos (co-proprietários) e vizinhos com múltiplas matrículas lindeiras — consome tempo e está sujeita a erros de digitação ou concordância gramatical.

Esta ferramenta resolve esse gargalo gerando documentos padronizados e prontos para assinatura e protocolo em Cartórios de Registro de Imóveis.

## 🔒 Privacidade e Conformidade com a LGPD

Este sistema foi concebido em total conformidade com a **Lei Geral de Proteção de Dados Pessoais (LGPD — Lei nº 13.709/2018)**:

* **Zero Armazenamento em Servidor:** Por se tratar de uma página estática, **nenhum dado inserido nos formulários é enviado, interceptado ou armazenado em servidores externos ou bancos de dados na nuvem**.
* **Processamento 100% Local:** Todas as informações (nomes, CPFs, RGs, endereços, matrículas e coordenadas) são processadas exclusivamente na memória do navegador do próprio utilizador.
* **Responsabilidade do Utilizador:** A guarda, o compartilhamento e o descarte dos arquivos gerados (`.pdf`, `.doc` e backups `.json`), bem como das configurações salvas localmente no navegador (`localStorage`), permanecem integralmente sob o controle e a responsabilidade do próprio utilizador.

## ✨ Principais Funcionalidades

* **Flexão Gramatical Automática:** Ajusta automaticamente o texto jurídico entre singular (*"Eu, proprietário(a)..."*) e plural (*"Nós, proprietários(as) condôminos(as)..."*) conforme a quantidade de proprietários do Imóvel Objeto e de cada Confrontante.
* **Suporte a Múltiplos Trechos por Confrontante:** Permite vincular várias propriedades/matrículas e suas respectivas tabelas de vértices a um único vizinho confrontante no mesmo documento.
* **Exportação em PDF/A-3b (Padrão Cartorial):** Pós-processamento nativo com injeção de metadados XMP (`pdfaid:part=3`, `pdfaid:conformance=B`) e perfil de cor `sRGB IEC61966-2.1`, atendendo às exigências de arquivamento digital dos Cartórios de Registro de Imóveis.
* **Exportação em MS Word (`.doc`):** Gera arquivos compatíveis com Microsoft Word e LibreOffice Writer com margens estreitas (1,27 cm), logotipo dimensionado e rodapé dinâmico nativo (`p. X de Y`).
* **Download em Lote (`.zip`):** Empacota todas as declarações do projeto em um único arquivo `.zip` (tanto em `.doc` quanto em `.pdf`).
* **Importação Rápida de Vértices:** Cola tabelas diretamente do **Excel**, **QGIS**, **AutoCAD** ou arquivos `.txt`/`.csv` separados por tabulação, ponto-e-vírgula ou vírgula.
* **Identidade Visual Persistente:** Salva o logotipo, dados da empresa e credenciais do Responsável Técnico localmente no navegador para preenchimento automático em futuros trabalhos.
* **Backup de Projetos (`.json`):** Salva e reabre projetos completos (incluindo logotipo, qualificação das partes e tabelas de coordenadas).

## 📖 Manual de Utilização

### 1. Barra Superior e Gestão de Projetos

No topo da tela encontram-se os controles globais do sistema:

| Botão | Função |
| :--- | :--- |
| **✨ Preencher Exemplo Fictício** | Preenche todos os formulários com dados fictícios de exemplo (empresa, RT, imóvel objeto, co-proprietários, confrontantes e vértices) para testes rápidos. |
| **🗑️ Limpar Tudo** | Apaga todos os campos preenchidos na sessão atual e reinicia o formulário em branco. |
| **💾 Salvar (`.json`)** | Exporta todo o trabalho atual (dados da empresa, logo, imóveis, confrontantes e coordenadas) em um arquivo `Projeto_Anuencias_[Imovel].json`. |
| **📂 Abrir (`.json`)** | Carrega um arquivo `.json` salvo anteriormente para continuar a edição ou reemitir documentos. |
| **☕ Incentivo** | Exibe informações do autor e QR Code PIX caso deseje apoiar a manutenção do projeto. |

### 2. Empresa, Logotipo e Responsável Técnico (RT)

No **Card 1**, configure a identificação do escritório de topografia/agrimensura e do profissional habilitado:

1. **Logotipo da Empresa:** Clique em **📷 Enviar Logo (PNG/JPG)** para carregar a marca do escritório. Ela será centralizada no topo das declarações com altura padronizada de `1,4 cm`.
2. **Dados da Empresa:** Preencha nome do escritório, subtítulo/especialidade, telefone, e-mail e endereço.
3. **Responsável Técnico (RT):** Informe nome, título profissional, registro CREA/CFT, RG, CPF, **Código de Credenciamento INCRA/SIGEF** e o **Nº da TRT/ART**.
   * Marque ou desmarque a caixa *"Incluir bloco de assinatura do Responsável Técnico como testemunha"* conforme a necessidade do cartório.
4. **Salvar como Padrão:** Clique em **⭐ Salvar Padrão** no cabeçalho do Card 1. Sempre que você abrir o sistema no mesmo navegador, esses dados já virão preenchidos automaticamente. Para apagar o padrão salvo, clique em **Limpar Padrão**.

### 3. Imóvel Objeto (IMÓVEL 2) e Proprietários

No **Card 2**, informe os dados do imóvel que está sendo georreferenciado/certificado (denominado **IMÓVEL 2** no texto legal):

1. **Dados Registrais:** Preencha o *Nome do Imóvel Objeto*, *Matrícula nº*, *CCIR nº*, *Município/Comarca* e o *Local e Data da Declaração* (ex.: `Cidade Exemplo - SP, 23 de novembro de 2026`).
2. **Proprietário Principal:** Informe nome completo/razão social, CPF/CNPJ, RG, nacionalidade, estado civil, profissão e endereço residencial.
3. **Co-proprietários (Condôminos):** Caso o imóvel possua mais de um proprietário, clique em **+ Adicionar Co-proprietário (Imóvel Objeto)** e preencha sua qualificação. Todos os co-proprietários serão incluídos automaticamente no texto e no bloco de assinaturas.

### 4. Confrontantes (IMÓVEL 1), Co-proprietários e Múltiplos Trechos

No **Card 3**, cadastre cada vizinho lindeiro que deverá assinar a declaração de anuência:

1. Clique em **+ Adicionar Confrontante** (botão laranja no topo do Card 3 ou na barra inferior).
2. **Qualificação do Confrontante Principal:** Preencha os dados pessoais do vizinho e o município/comarca do imóvel confrontante.
3. **Co-proprietários deste Confrontante:** Se o imóvel vizinho pertencer a mais de um condômino, clique em **+ Adicionar Co-proprietário (Confrontante)**.
4. **Trechos & Propriedades Confrontantes:**
   * Informe o *Nome da Propriedade (Imóvel 1)*, *Matrícula nº* e *CCIR nº*.
   * Caso o mesmo confrontante faça divisa com o Imóvel Objeto por meio de **duas ou mais propriedades/matrículas distintas**, clique em **+ Adicionar Novo Trecho / Propriedade para este Confrontante**. O sistema unificará as matrículas no texto jurídico e gerará uma tabela de vértices separada para cada trecho dentro do mesmo documento.

### 5. Importação de Coordenadas (Excel, QGIS e AutoCAD)

Dentro de cada trecho do confrontante, há uma tabela com as 7 colunas padrão do memorial tabular:

`De` | `Longitude` | `Latitude` | `Altitude (m)` | `Para` | `Azim. 3ª Ed.` | `Dist. 3ª Ed. (m)`

Você pode preencher os vértices manualmente clicando em **+ Linha** ou importar dezenas de vértices de uma só vez:

1. Copie as células da sua planilha Excel ou arquivo de texto (sem a linha de cabeçalho) na ordem das 7 colunas acima.
2. Clique no botão **📋 Colar (Excel/TXT)** acima da tabela do trecho.
3. Cole o conteúdo na caixa de texto (o sistema reconhece automaticamente separadores por **Tabulação**, **Ponto-e-vírgula `;`** ou **Vírgula `,`**).
4. Clique em **Importar Coordenadas**.

### 6. Pré-visualização A4 e Exportação (Individual ou em Lote)

* **Pré-visualização A4:** Clique em **👁️ Ver na Prévia** no cabeçalho de qualquer confrontante para conferir a diagramação exata em folha A4 antes de baixar. Dentro do modal de prévia, você pode alternar entre os confrontantes pelo seletor superior.
* **Exportação Individual:** Nos botões de cada card de confrontante, clique em:
  * **📄 .DOC** — Baixa `DECLARAÇÃO - [Matrícula(s)] - [Nome].doc`
  * **⚡ PDF** — Baixa `DECLARAÇÃO - [Matrícula(s)] - [Nome].pdf` (padrão PDF/A-3b)
* **Exportação em Lote (Barra Fixa Inferior):** Quando houver dois ou mais confrontantes cadastrados, utilize os botões na barra inferior da tela:
  * **📄 Baixar Todos em .DOC (.zip)** — Gera `Declaracoes_Anuencia_Word.zip`
  * **⚡ Baixar Todos em PDF (.zip)** — Gera `Declaracoes_Anuencia_PDFA3.zip`

## ⚖️ Padrão Técnico e Legal dos Documentos Gerados

* **Configuração de Página:** Papel A4 (`210 mm × 297 mm`), margens estreitas de `1,27 cm` em todos os lados, fonte `Times New Roman` (`11 pt` no corpo e `8–9 pt` nas tabelas e rodapés).
* **Fundamentação Legal:** Texto padronizado com declaração expressa de inexistência de litígio/discordância nos limites comuns, ciência quanto ao disposto no **§ 10 do art. 213 da Lei nº 6.015/73** (dispensa de outorga uxória/marital na anuência de confrontação e responsabilidade de condômino no trecho confrontante), identificação do RT credenciado INCRA e vinculação à planta e memorial descritivo anexos.
* **Rodapé Automático:** Exibe o nome da(s) propriedade(s) confrontante(s) alinhado à esquerda e a numeração de páginas (`p. X de Y`) alinhada à direita em todas as páginas, tanto no arquivo `.doc` quanto no `.pdf`.

## 👨‍💻 Autoria e Incentivo

Desenvolvido por **Rafael R. Santoro (2026)**.

Se esta ferramenta facilitou o seu dia a dia no escritório ou em campo, clique no ícone da **xícara de café ("Incentivo")** no canto superior esquerdo da aplicação para contribuir via PIX e incentivar o desenvolvimento de novas soluções gratuitas para a área de geotecnologias e agrimensura.
