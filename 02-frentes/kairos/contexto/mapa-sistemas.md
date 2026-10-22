# Mapa de Sistemas — Overlabs / SKY

> Contexto para as skills do Discovery. Consultado por `/analise-demanda` e `/desenho-solucao`.

> **Fonte:** SKY Architecture Applications Mapping (últ. atualização 28/01/2022) + Inventário de Sistemas DTV/Sky + Workshop TI CORE (jul/2024).
> **Atenção:** a base de arquitetura é de 2022 e está defasada. Sistemas marcados com ⚠️ vieram do material de 2024 e ainda não têm ficha completa.
> Dono deste arquivo: Arquitetura. Alteração via PR.

## Como usar

- Ao avaliar um requisito, confronte os sistemas citados com este mapa. Sistema citado que **não** existe aqui é achado — pode ser nome interno, sistema novo ou erro de entendimento.
- O campo **Domínio** segue TMForum. Requisito que cruza mais de um domínio quase sempre implica integração via OSB/SOA.
- Sistema com ambiente `On-premise` tende a ter janela de mudança mais restrita que SaaS.

## Panorama

- **101 sistemas em produção** no mapeamento de 2022 (123 registros no total: 16 descontinuados, 6 em projeto). O workshop de 2024 reporta **172 sistemas** — a diferença indica o grau de defasagem desta base.
- Distribuição por ambiente: On-premise 41 · Oracle IaaS 32 · SaaS de parceiro 16 · AWS IaaS 4 · Oracle SaaS 3 · Oracle PaaS 3 · AWS SaaS 2

---

## Customer — clientes, billing e atendimento

| Sistema | O que faz | TAM (nível 1) | Ambiente | Dono técnico |
|---|---|---|---|---|
| **APP Minha SKY** | Aplicativo desenvolvido pela equipe de inovação, permite a clientes pós pagos a consulta de seus dados, dados das f… | Customer Self Management | AWS IaaS |  |
| **Autorizador** | Solução interna de Gateway de Pagamentos responsável pela orquestração de ações de pagamento entre sistemas interno… | Receivables Management | On-premise |  |
| **Base Cartão de Crédito** | Base dentro da rede PCI destinada a informações de cartão de crédito criptografadas pelo HSM. O nome desta base é P… | Receivables Management | On-premise |  |
| **BI PUBLISHER** | Aplicação destinada ao gerenciamento e disponibilização de relatórios e documentos. | Transactional Document Production | Oracle IaaS |  |
| **BOS** | Aplicação de suporte ao fluxo dos contatos não resolvidos pelo atendimento 1º nível(Atendimento 2º Nível). Sua inte… | Customer Problem Management | Oracle IaaS |  |
| **BRM** | Aplicação designada a parte de billing, responsável pelo faturamento e gerenciamento de dados financeiros dos clien… | Billing Account Management Collection Ma… | On-premise | Sergio Ricardo da Costa |
| **Clisitef** | Aplicação responsável pela captura de dados de pagamento e bate os dados com o SKYTef. | Receivables Management | On-premise |  |
| **CYBER** | ODI responsável pelo envio dos dados dos assinantes em série de cobrança para a agência de cobrança. | Collection Management | On-premise |  |
| **Fila de Ações** | Banco de dados utilizado pelo BRM para registrar as ações que devem ser realizadas pelo ODI de régua de cobrança, s… | Collection Management | On-premise |  |
| **File Split** | Aplicação responsável por verificar os arquivos bancários que foram transformados pelo SKYLine e atualizar os pagam… | Receivables Management | On-premise |  |
| **GMAP** | Aplicação destinada ao gerenciamento das promessas de pagamento. | Receivables Management | On-premise |  |
| **GPAG** | Logs de pagamentos entre a SKY e entidades financeiras (CC, Débito, PEC (CEF), Bradesco, Pag Fácil, Mensalidade Rec… | Receivables Management | On-premise |  |
| **GPF** | Módulo do iCare acrônimo de Guia de Procedimentos Financeiros, responsável pelo suporte ao atendimento do cliente. … | Customer Service Representative Toolbox | Oracle IaaS |  |
| **GPT** | Módulo do iCare acrônimo de Guia de Procedimento Técnico, responsável pelo suporte ao atendimento do cliente. Possu… | Customer Service Representative Toolbox | Oracle IaaS |  |
| **iCare BKO** | Front-end do sistema de backoffice com os clientes (CRM) utilizado pelo Call Center (grupo e acesso a público restr… | Customer Service Representative Toolbox | Oracle IaaS |  |
| **iCare Clientes** | Front-end do sistema de relação com os clientes (CRM) utilizado pelo Call Center, permite o gerenciamento de pacote… | Customer Service Representative Toolbox | Oracle IaaS | Italo Josenilton |
| **MAESTRO** | Aplicação responsável pela orquestração dos processos necessários para a execução de pedidos do cliente (Customer O… | Customer Order Management | Oracle IaaS |  |
| **Mensitef** | Aplicação destinada ao monitoramento das faturas em débito automático a vencer. No vencimento realiza a cobrança do… | Receivables Management | On-premise |  |
| **Pague Aqui** | Aplicação responsável pela consulta de dívidas e recebimento de pagamentos On-Line vindos do Bradesco Pague Fácil, … | Receivables Management | Ambiente Parceiro - SaaS |  |
| **PC6** | Aplicação construída em ODI e Java que verifica inconsistências de parque entre o BRM e o Siebel, executando a sinc… | Fallout Management | On-premise |  |
| **PCB** | Centraliza e processo o retorno dos pagamentos das instituições bancárias | Receivables Management | On-premise |  |
| **PEC** | Aplicação responsável pela consulta de dívidas e recebimento de pagamentos On-Line das lotéricas (atualmente soment… | Receivables Management | Oracle IaaS |  |
| **Portal SKY Clientes** | Portal destinado a centralização de informações, notificações e procedimentos utilizados no atendimento. Seus princ… | Customer Service Representative Toolbox | Ambiente Parceiro - SaaS |  |
| **POS** | Aplicação responsável pelo pagamento de contas (adesão) e recarga , uso exclusivo dos credenciados SKY. Interface u… | Customer Service Representative Toolbox | On-premise |  |
| **SDA** | Sistema de Devolução de Valores responsável pela extração dos contatos feitos pelo iCare que solicitam a devolução … | Billing Inquiry, Dispute & Adjustment Ma… | On-premise |  |
| **Siebel CCP** | CRM responsável pela gestão dos clientes e seus respectivos pacotes e produtos, bem como gerenciar os produtos e pa… | Customer Information Management | On-premise | Francisco Bolismar |
| **Site SKY** | Site Institucional, permite a clientes pós pagos a consulta de seus dados, dados das faturas, compra de PPV, compra… | Customer Information Management | AWS IaaS |  |
| **SKY Pré Pago (Site Livre)** | Site de autoatendimento que permite a clientes pré pagos a consulta de seus dados, recarga do pacote, compra de pro… | Customer Self Management | AWS IaaS |  |
| **Skyline** | Aplicação responsável por transformar os arquivos bancários recebidos e enviados pela Nexxera, empresa a qual provê… | Receivables Management | On-premise |  |
| **SKYTEF** | Aplicação responsável por intermediar todas as chamadas de pagamento via cartão de credito e enviá-las para o SITEF… | Receivables Management | On-premise |  |
| **SoftwareExpress** | Aplicação responsável pela captura de dados de pagamento e bate os dados com o SKYTef. | Receivables Management | On-premise |  |

## Integration — barramento, APIs e processos

| Sistema | O que faz | TAM (nível 1) | Ambiente | Dono técnico |
|---|---|---|---|---|
| **ADCC** | Broker de mensages para integração com canais eletronicos (WhatsApp, Messenger, Telegram, SMS, E-mail) | Enterprise Application Integration | Ambiente Parceiro - SaaS |  |
| **AWS Api Gateway** | Plataforma SaaS de Api Gateway disponibilizada pela AWS utilizado para o consumo externo de APIs de integração B2B | API Management | AWS SaaS |  |
| **Camunda** | Camunda BPM Engine é um sistema de gerenciamento de processos de negócios (BPM, DMN e CMMN) para qualquer tipo e ta… | Business Process Management and Workflow… | Oracle IaaS |  |
| **Control-M** | O Control-M simplifica a orquestração do fluxo de trabalho de aplicativos e dados no local ou como um serviço. Ele … | Enterprise Application Integration | On-premise |  |
| **EIM** | Interface de integração batch Siebel | Enterprise Application Integration | On-premise |  |
| **Kong Api Management** | Platafoma de Api Gateway e Api Management, adquirida para substituição da plataforma SaaS AWS | API Management | AWS IaaS |  |
| **Oracle Data Integrator - ODI** | Aplicação responsável pelas integrações em lote que o correm no ambiente. | Enterprise Application Integration | On-premise |  |
| **Oracle Service Bus - OSB** | Ambiente de exposição e integração entre os diversos sistemas e interfaces, através de serviços corporativos. | Enterprise Application Integration | On-premise | Allif Henrique Pereira |
| **Oracle Soa Suite - SOA** | Ambiente de execução e orquestração de processos de negócios complexos de integração (BPELs) | Enterprise Application Integration | On-premise | Danyllo Andrade |
| **PIP - Order to Cash** | Processos responsáveis pela integração do Siebel e BRM com o Maestro. | Enterprise Application Integration | Oracle IaaS |  |
| **Riversoft** | Aplicação que prove a transferência de arquivos via FTP entre credenciados. | Enterprise Application Integration | On-premise |  |
| **SOAP Web** | Ferramenta custom, construída e mantida pelo time de Sustentação de TI, para a realização de processos de fallout. | Fallout Management | Oracle IaaS |  |
| **UEL** | Interface de integração batch BRM | Enterprise Application Integration | On-premise |  |

## Resource — provisionamento, campo e inventário

| Sistema | O que faz | TAM (nível 1) | Ambiente | Dono técnico |
|---|---|---|---|---|
| **ASAP/OCA** | Aplicação de controle de aprovisionamento da rede, responsável em converter os comandos provenientes das aplicações… | Resource Domain Management | Oracle IaaS |  |
| **Base Certa** | Aplicação designada à correção da base de dados referente as campanhas. Após as correções serem feitas, as mesmas n… | Location Management | Oracle IaaS |  |
| **CSI** | Inventário de serializados (decodificadores e smartcars) | Resource Inventory Management | Oracle IaaS |  |
| **iCare Campo / Parceiro** | Front-end que tem como função o auxílio aos credenciados na gestão de estoque e a administração das OSs. O iCare Ca… | Workforce Management | Oracle IaaS |  |
| **Oracle Field Service Cloud Service - TOA** | Gerenciamento de Serviços de Campo | Workforce Management | Oracle SaaS |  |
| **Oracle Field Service Cloud Service Mobile - TOA** | Aplicação mobile para utilização dos técnicos na realização de serviços de campo | Workforce Management | Oracle SaaS |  |
| **SPS (Sistema de Provisionamento SKY) - AsapLess** | Aplicação custom de controle de aprovisionamento da rede, responsável em converter os comandos provenientes das apl… | Resource Domain Management | On-premise |  |
| **URA Habilitação** | Central de atendimento automatizado utilizada pelos técnicos em campo. Permite a habilitação do equipamento, envio … | Resource Domain Management | Ambiente Parceiro - SaaS |  |
| **URA Habilitação Pré-Pago (Livre)** | Central de atendimento automatizado utilizada pelos técnicos em campo ao atender um cliente livre. Permite ao técni… | Resource Domain Management | Ambiente Parceiro - SaaS |  |

## Service — ordens de serviço

| Sistema | O que faz | TAM (nível 1) | Ambiente | Dono técnico |
|---|---|---|---|---|
| **MOS** | Aplicação responsável pelo gerenciamento das Ordens de Serviço (OS). Como funcionalidade adicional possui um proces… | Service Order Management | Oracle IaaS |  |

## Product — catálogo e ciclo de vida

| Sistema | O que faz | TAM (nível 1) | Ambiente | Dono técnico |
|---|---|---|---|---|
| **Aumento de Preço Nohs** | ODI responsável pelo tratamento do aumento de preço anual, a aplicação altera o preço no SIEBEL e BRM de acordo com… | Product Lifecycle Management | On-premise |  |
| **Siebel Enterprise Catalog** | Catálogo corporativo de produtos e serviços | Product Catalog Management | On-premise |  |

## Market & Sales — vendas e canais

| Sistema | O que faz | TAM (nível 1) | Ambiente | Dono técnico |
|---|---|---|---|---|
| **iSelling** | Aplicação corporativa destinada a realização de campanhas de Marketing, Produtos, Fidelização e Negociação para púb… | Campaign & Funnel Management | Oracle IaaS |  |
| **Oracle Commerce Cloud - OCC** | Plataforma de E-commerce utilizada pelo site assine.sky.com.br | Channel Sales Management | Oracle SaaS |  |
| **Power BI** | Geração de dashboards com indicadores de negócio | Sales & Marketing Reporting | On-premise |  |
| **Salesforce Mobile** | Automação da força de venda, plataforma para captura e processamento de propostas de vendas através de app mobile | Sales Portals | Ambiente Parceiro - SaaS |  |
| **Salesforce Salescloud** | Automação da força de venda, plataforma para captura e processamento de propostas de vendas | Sales Portals | Ambiente Parceiro - SaaS | Danilo Lima |
| **Site Assine** | Aplicação eCommerce (executado na plataforma Oracle Commerce Cloud), para aquisição de pacotes de novas assinaturas… | Sales Portals | AWS SaaS |  |
| **Speed Web** | Interface web voltada para criação de novas assinaturas, utilizado pelos credenciados SKY, com sistema de vendas de… | Sales Portals | On-premise |  |
| **Splunk** | Inferface para criação de dashboards de negócios | Sales & Marketing Reporting | Ambiente Parceiro - SaaS |  |

## Enterprise — corporativo, ERP, segurança e ferramentas

| Sistema | O que faz | TAM (nível 1) | Ambiente | Dono técnico |
|---|---|---|---|---|
| **Automation Anywhere** | Solução para criação e gestão de processos de automação RPA. | Enterprise Application Integration | Oracle IaaS |  |
| **BDI** | Base intermediária entre BRM e SAP. Destinada também à extração de informações para realizar conciliações. | Financial Management | On-premise |  |
| **Bigdata** | Datalake de ingestão de dados de diversas fontes de informações | Knowledge Management | On-premise |  |
| **Blacklist** | Base de dados responsável por manter dados utilizados para controle antifraude de clientes SKY. | Fraud Management | Oracle IaaS |  |
| **Confluence** | Ferramenta de colaboração e documentação dos artefatos relacionados os projetos JIRA Software | Administrative Services | Oracle IaaS |  |
| **Distribuidor** | ODI responsável pelo envio dos arquivos de débito em conta para o banco e alimentação da base do Mensitef. | Financial Management | On-premise |  |
| **Financeiro WEB** | Aplicação web com alarmes financeiros. Utiliza IBS e BRM, usa como base D-1 e consulta o GPAG. Ainda não há alarme … | Financial Management | Oracle IaaS |  |
| **ForgeRock Identity Platform (IDM, IG, DS e AM)** | Plataforma de gestão de identidades e acessos para os operadores do callcenter, vendedores e credenciados (utilizad… | Security Management | Ambiente Parceiro - SaaS |  |
| **GLOBALSUITE** | Identifica vulnerabilidades e ameaças aos ativos de informações e decida com o proprietário do risco as contramedid… | Security Management | On-premise |  |
| **HSM** | Aplicação responsável pela criptografia e descriptografia dos dados do cartão de crédito na rede segura (PCI). | Security Management | On-premise |  |
| **IDM Oracle** | Front-end disponível somente via intranet responsável pela abertura de chamados para a criação de usuários. Também … | Security Management | Oracle IaaS |  |
| **Jira Help Desk** | Getsão e workflow de chamados / incidentes | Administrative Services | Oracle IaaS |  |
| **JIRA Software** | Gestão de projetos e demandas | Administrative Services | Oracle IaaS |  |
| **Oracle Identity Cloud Service - IDCS** | Plataforma PaaS para gerenciamento de identidade e acessos | Security Management | Oracle PaaS |  |
| **Oracle OBI EE** | Oracle Business Intelligence Enterprise Edition | Knowledge Management | On-premise |  |
| **Payment Control** | Aplicação usada pelo portal finanças como back-end, responsável pela conciliação de pagamentos online. Tem como fun… | Financial Management | Oracle IaaS |  |
| **Ping Federate** | Ferramento de autenticação Vrio SSO | Security Management | Ambiente Parceiro - SaaS |  |
| **Portal LGPD** | Portal destinado a tratativa da Lei Geral de Proteção a Dados | Regulatory & Compliance Management | Oracle IaaS |  |
| **Portal SAP Reembolso** | Aplicação responsável pelo lançamento de reembolsos de funcionários. | HR Management | On-premise |  |
| **Safekey** | Aplicação responsável por gerenciar os acessos de usuários nos sistemas. Utiliza como fonte de autenticação os Ads … | Security Management | Oracle IaaS |  |
| **SAP 500** | Sistema Modular fornecido pela SAP, dentro da SKY existem os módulos tributário e contábil. O SAP é responsável pel… | Financial Management | On-premise | Celso Lapides |
| **SAP 600 (MM)** | Sistema em desenvolvimento, apresentará muitas das funções que atualmente são do GTI, tais como o gerenciamento do … | Supply Chain Management | On-premise |  |
| **SAP Arriba** | Requisições e controles de compras | Supply Chain Management | Ambiente Parceiro - SaaS |  |
| **Sky Analytics** | Ferramenta de BI que o usuário pode efetuar queries AdHoc. Essa ferramenta foi desenvolvida em cima do OBIEE (ferra… | Knowledge Management | Oracle IaaS |  |

## Supplier & Partner — parceiros e meios de pagamento

| Sistema | O que faz | TAM (nível 1) | Ambiente | Dono técnico |
|---|---|---|---|---|
| **Mundipagg** | Solução de meio de pagamento utilizado pela estrutura Digital | Supplier & Partner Management | Ambiente Parceiro - SaaS |  |
| **SITEF** | Aplicação voltada ao registro das transações de cartões de créditos efetuadas e posterior geração de relatórios. | Supplier & Partner Management | On-premise |  |

## Ferramentas e infraestrutura (sem domínio TMForum)

| Sistema | O que faz | TAM (nível 1) | Ambiente | Dono técnico |
|---|---|---|---|---|
| **Apache Maven** | Apache Maven é uma ferramenta de gerenciamento e compreensão de projetos de software. Apache Maven, ou Maven, é uma… | N/A | Ambiente Parceiro - SaaS |  |
| **AppDynamics** | Plataforma de monitoração de aplicações e infraestrutura | N/A | Ambiente Parceiro - SaaS |  |
| **BitBucket** | Versionamento de códigos fontes GIT | N/A | Oracle IaaS |  |
| **Jenkis** | Jenkins é um servidor de Integração Contínua open-source feito em Java, responsável pelo gerenciamento do pipeline … | N/A | Oracle IaaS |  |
| **Microsoft Office 365** | Suite de produtos da linha Office (word, excel, powerpoint, one note), versão SaaS, utilizado por toda a companhia … | N/A | Ambiente Parceiro - SaaS |  |
| **Microsoft Teams** | Plataforma da microsoft para colaboração e comunicação interna/externa das equipes | N/A | Ambiente Parceiro - SaaS |  |
| **Nexus** | é um gerenciador de repositório que armazena “artefatos”, permitindo o acesso direto e gerenciamento de suas depend… | N/A | Oracle IaaS | Franco Fuentes (DevOps ARG) |
| **Oracle Container Engine - OKE** | Infraestrutura de gerenciamento de containers oferecida pela Oracle Cloud | N/A | Oracle PaaS |  |
| **Rancher** | Software open source que possibilita a criação de uma plataforma privada para criação de containers. Por meio dele,… | N/A | Oracle PaaS |  |
| **VmWare** | Aplicação responsavel pelo gerenciamento e execução de maquinas virtuais | N/A | On-premise |  |
| **Zabix** | Plataforma de monitoração de aplicações e infraestrutura | N/A | Oracle IaaS |  |
---

## Sistemas do material de 2024 ainda sem ficha ⚠️

Aparecem na arquitetura de alto nível do Workshop TI CORE (jul/2024) ou em demandas recentes, mas **não constam do mapeamento de 2022**. Precisam de ficha completa.

| Sistema | O que se sabe |
|---|---|
| **Magento (E-commerce)** | Captura de pedido de venda no canal e-commerce |
| **KillBill** | Billing — aparece na timeline de tecnologia a partir de 2024 |
| **SAS Fraud & Credit Scoring** | Antifraude e score de crédito, integrado via Kong |
| **Portal Nova Parabólica** | Portal de habilitação; citado em demandas do CPA |
| **Site Parceiros** | Canal de habilitação por credenciado |
| **Spring Batch** | Processamento batch em Java (microsserviços) |
| **GPT** | Guia de atendimento por flows (consta em 2022 como Customer, validar se é o mesmo) |
| **Calidus / Callidus** | Comissionamento de credenciados (SaaS) — grafia divergente entre fontes |
| **DSM** | Segurança na esteira DevOps |
| **Grafana / Loki / Prometheus / Ansible / Terraform / SonarQube / Veracode / Docker / Kubernetes (OKE)** | Esteira DevOps |

---

## Fluxo de alto nível (arquitetura 2024)

```
Canais de venda        Middleware        BSS                    OSS
─────────────────      ──────────        ───────                ───────────
Salesforce (Web/Mob)                     Oracle Siebel          Maestro (SOA)
Magento (e-commerce)   →  KONG    →      · Customer/Account      · Order Fulfillment
iCare CRM (CSR)           (Corporate     · Enterprise Catalog       ↓
Minha SKY / SKY Web        APIs,                                 CIS (serial inventory)
WhatsApp / IVR             TMForum)      Oracle BRM              MOS (work order)
OFSC-TOA (campo)          Oracle         · Billing               ASAPLess (provisionamento)
                          Service Bus    · Revenue                    ↓
                          (SOA           SAP/ERP                 sinal / satélite
                          Corporate      · Stock, FICO, Ledger
                          Services)
                                         SAS — fraude e score
                                         Payment Gateway
                                         (Caixa, Cielo, Pix, Stone, Getnet)
```

**Volumes atendidos (2024):** 3,5 M clientes · 11.000 representantes de vendas · 7.000 técnicos · 6.000 CSR · 200 mil prospects/mês.

---

## Vocabulário de estimativa

As tecnologias abaixo são as reconhecidas pela **calculadora** (aba `Racional` da planilha de estimativa, 322 linhas de `tecnologia × componente × complexidade → horas`). Um requisito só é decomponível se puder ser expresso neste vocabulário:

`ODI` · `BD Oracle` · `OSB` · `SOA` · `MDS` · `ASP .NET UI (Front)` · `.NET Business Tier` · `.NET Data Tier` · `.NET WCF` · `BRM` · `ASAP` · `Siebel` · `Salesforce` · `SF Mobile` · `Java`

**Não estão na calculadora, mas aparecem em demandas:** Camunda, Spring Batch, KONG, BI/ingestão, Magento. Requisito que dependa dessas tecnologias exige tratamento fora da tabela — sinalizar como ponto de atenção.

---

## Lacunas conhecidas — a preencher pela Arquitetura

- [ ] Atualizar a base: são 172 sistemas em 2024, 101 mapeados aqui
- [ ] Integrações ponto a ponto (quem chama quem) — hoje só existe a visão de alto nível
- [ ] Donos técnicos: apenas 10 dos 101 sistemas têm contato nominal
- [ ] Janelas de mudança e criticidade por sistema
- [ ] Sistemas dos produtos FTTH, OTT, Seguros e MVNO — sub-representados nesta base
- [ ] Confirmar quais dos 16 "descontinuados" de 2022 realmente saíram do ar
