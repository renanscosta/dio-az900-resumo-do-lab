# Componentes de Arquitetura Azure

## Região e Zona de Disponibilidade ##

- **Região:** Localização geográfica onde os serviços de nuvem estão disponíveis. Cada região é composta por vários data centers, e as empresas podem escolher a região mais próxima para reduzir a latência e melhorar o desempenho. Essa escolha pode influenciar em custos (preços variam entre regiões) e em conformidade regulatória.
    - Exemplo: Aplicação para usuários no Brasil costuma usar Brazil South para reduzir latência.

- **Zona de Disponibilidade:** Subdivisão dentro de uma região com data centers fisicamente separados e energia, rede e resfriamento independentes. Distribuir recursos entre zonas aumenta alta disponibilidade e tolerância a falhas.
    - Exemplo: Duas VMs em zonas diferentes com load balancer.

- Quanto mais disponibilidade for necessária, maior tende a ser o custo;
- Nem todas as regiões possuem zonas de disponibilidade, e nem todos os serviços estão disponíveis em todas as zonas. Verifique antes de planejar a arquitetura;

**Alguns tipos de serviços nas zonas de disponibilidade:**
- **Serviços de zona**: Implantados em uma zona específica. A alta disponibilidade depende da arquitetura do cliente.
    - Exemplo: Uma VM em zona 1 sem réplica em outra zona.
- **Serviços com redundância de zona**: Implantados com réplicas em várias zonas, oferecendo alta disponibilidade intrarregional.
    - Exemplo: Azure Kubernetes Service (AKS) com nós distribuídos em zonas.
- **Serviços não regionais**: Serviços globais que não ficam presos a uma única região.
    - Exemplo: Microsoft Entra ID e Azure Traffic Manager.

### Comparativo: Região x Zona x Par de Região

| Conceito | O que é | Para que serve | Exemplo prático |
|---|---|---|---|
| Região | Área geográfica com vários data centers | Reduzir latência e atender requisitos de conformidade | Hospedar um app no Brazil South para usuários no Brasil |
| Zona de disponibilidade | Data centers isolados dentro da mesma região | Alta disponibilidade e tolerância a falhas | VMs em zonas diferentes com balanceador |
| Par de região | Duas regiões emparelhadas na mesma geografia | Recuperação de desastres e continuidade regional | GRS replica dados para a região pareada |

![Imagem](imagens/zonas-disponibilidade.png)
imagem retirada do site oficial do Azure: https://azure.microsoft.com/pt-br/global-infrastructure/availability-zones/


### Pares de região ###
- São regiões emparelhadas dentro da mesma geografia, projetadas para recuperação de desastres e alta disponibilidade regional. Os pares permitem replicação assíncrona para outra região.
    - Exemplo: Storage GRS replica dados da região primária para a região pareada.

- Alguns serviços exigem configuração do cliente para usar pares de região (ex.: Azure Site Recovery). Outros oferecem replicação geográfica integrada (ex.: Azure SQL Database).

- Nem todas as regiões possuem pares de região, e nem todos os serviços estão disponíveis em todas as regiões. Verifique antes de planejar a arquitetura.

- Em geral, pares de região são bidirecionais dentro da mesma geografia. O mapeamento exato depende da geografia e deve ser consultado na documentação oficial.

![Imagem](imagens/par-regioes.png)
imagem retirada do site oficial do Azure: https://azure.microsoft.com/pt-br/global-infrastructure/geographies/


## Regiões Soberanas ##
- São regiões que atendem a requisitos específicos de conformidade e soberania de dados, mantendo os dados dentro de um país ou região.
    - Exemplo: Órgãos públicos que exigem dados hospedados apenas no território nacional.

### US DoD Central, US Government, US Gov Virginia, US Gov Arizona ###
- Regiões soberanas para o governo dos EUA, com requisitos de conformidade como FedRAMP e CJIS. São isoladas das regiões comerciais.
    - Exemplo: Aplicações de defesa e segurança nacional.

### Azure China 21Vianet ###
- Região soberana operada pela 21Vianet para atender requisitos de residência de dados na China e leis locais.
    - Exemplo: Empresas que precisam hospedar dados de usuários chineses dentro do país.

## Grupos de Recursos ##
- São contêineres lógicos que agrupam recursos relacionados, facilitando organização, gerenciamento e monitoramento. Ajudam na governança e no controle de custos (OpEx).
    - Exemplo: Grupo de recursos "app-loja-prod" com App Service, Banco e Storage.

    - Os recursos só podem estar em um único grupo de recursos, e um grupo pode conter vários recursos. Grupos de recursos não contêm outros grupos.
    - Recursos podem estar em regiões diferentes, mesmo dentro do mesmo grupo.

## Assinaturas ##
- São unidades de faturamento e gerenciamento. Permitem organizar recursos e controlar custos por projeto, departamento ou ambiente.
    - Exemplo: Assinaturas separadas para "Marketing-Prod" e "TI-Prod".

- Uma conta do Azure pode conter várias assinaturas, e cada assinatura pode conter vários grupos de recursos. As assinaturas também podem ser associadas a diferentes formas de pagamento, como cartão de crédito, fatura ou contrato corporativo, permitindo que as empresas controlem seus custos de forma eficiente. Além disso, as assinaturas também permitem que as empresas monitorem o uso e os custos dos recursos de forma centralizada, facilitando a otimização dos custos na nuvem.

![Imagem](imagens/assinaturas.png)
imagem retirada do site oficial do Azure: https://azure.microsoft.com/pt-br/overview/azure-subscription/

### Limites de Assinaturas ###

- **Limite de cobrança ou Billing boundary:** A assinatura define onde começa e termina a fatura.Tudo que rodar dentro da Assinatura A gera uma fatura/relatório de custos da Assinatura A. Tudo que rodar na Assinatura B gera outra fatura/relatório, separado.

**Imagine uma empresa com:**
- Departamento de Marketing  
- Departamento de TI

Você cria:

- Assinatura “Marketing-Prod”  
- Assinatura “TI-Prod”

No fim do mês, você tem dois relatórios/faturas:

- Uma só com os custos dos recursos de Marketing (storage para campanhas, VMs para landing pages etc.).
- Outra só com os custos de TI (servidores internos, APIs, banco de dados corporativo).

Assim, o financeiro consegue ver exatamente quanto cada área gastou, pois a assinatura é a **fronteira / limite de cobrança**.

- **Limite de Controle de Acesso ou Access Control Boundary:** A assinatura é o limite onde você define quem tem acesso a quais recursos. Você pode criar grupos de usuários e atribuir permissões específicas para cada assinatura, garantindo que apenas as pessoas autorizadas possam acessar os recursos dentro daquela assinatura.

- Você configura RBAC (roles, permissões) na assinatura.  
- Quem tem papel de Owner/Contributor/Reader nessa assinatura pode (ou não) mexer em todos os recursos dentro dela.

Voltando à empresa:

- Assinatura “Marketing-Prod”  
- Assinatura “TI-Prod”

Você faz:

- Dá acesso de Contributor apenas ao time de Marketing na assinatura “Marketing-Prod”.  
- Dá acesso de Contributor apenas ao time de TI na assinatura “TI-Prod”.  

Resultado:

- O pessoal de Marketing **não consegue** nem ver nem apagar recursos da TI, porque eles estão em outra assinatura.
- O pessoal de TI não mexe nos recursos de Marketing.  

A assinatura virou uma **fronteira de acesso**: o que está dentro de uma assinatura pode ter regras de acesso completamente diferentes do que está em outra.

### Ligando os dois conceitos ###
A mesma assinatura serve ao mesmo tempo como:

**Unidade de cobrança (billing boundary).**
**Unidade de controle de acesso (access control boundary).**

Por isso, você cria mais assinaturas quando precisa:
- Separar custos (por departamento, projeto, cliente ou ambiente).
- Separar acessos (times diferentes, níveis de segurança diferentes).
​​
**Billing boundary → “Quem paga o quê” (fatura separada por assinatura).**
​**Access control boundary → “Quem pode mexer em quê” (permissões separadas por assinatura).**
​
## Grupos de Gerenciamento ##

- São contêineres lógicos para organizar assinaturas em uma hierarquia de governança. Permitem aplicar políticas e RBAC em escala.
    - Exemplo: Grupo de gerenciamento "Corporativo" com os grupos "Financeiro" e "Produtos".
- Um grupo de gerenciamento pode conter várias assinaturas, e uma assinatura só pode estar em um grupo. Grupos de gerenciamento podem conter outros grupos.

![Imagem](imagens/grupos-gerenciamento.png)
imagem retirada do site oficial do Azure: https://azure.microsoft.com/pt-br/overview/management-groups/

## Hierarquia de governança (ordem correta)
- Entidades de gerenciamento -> Assinaturas -> Grupos de recursos -> Recursos.
    - Exemplo: Grupo de gerenciamento "Corporativo" > Assinatura "TI-Prod" > Grupo de recursos "app-loja-prod" > App Service.

# Dicas para prova:
- Região é localização geográfica; zona de disponibilidade são data centers isolados dentro da mesma região (alta disponibilidade).
- Pares de região servem para recuperação de desastres com replicação assíncrona.
- Grupos de recursos não podem conter outros grupos; assinaturas são limite de cobrança e acesso.
- Em provas, escolha a opção que atende ao requisito com o menor nível necessário de custo/complexidade.

# Questões de exemplo para prova:
1. Em qual nível da hierarquia de governança se aplicam políticas para várias assinaturas ao mesmo tempo?
    - a) Região
    - b) Zona de disponibilidade
    - c) Grupo de gerenciamento **(correta)**
    - d) Grupo de recursos
    - Explicação: Políticas em escala são aplicadas em grupos de gerenciamento, que abrangem várias assinaturas.

2. Qual afirmação descreve melhor uma zona de disponibilidade?
    - a) Regiões emparelhadas para failover automático
    - b) Data centers isolados dentro da mesma região **(correta)**
    - c) Regiões soberanas para conformidade governamental
    - d) Serviços globais sem região definida
    - Explicação: Zonas são data centers fisicamente separados dentro de uma mesma região.

3. Qual item representa a ordem correta da hierarquia de governança no Azure?
    - a) Assinaturas -> Entidades de gerenciamento -> Recursos -> Grupos de recursos
    - b) Entidades de gerenciamento -> Assinaturas -> Grupos de recursos -> Recursos **(correta)**
    - c) Grupos de recursos -> Assinaturas -> Recursos -> Entidades de gerenciamento
    - d) Recursos -> Grupos de recursos -> Assinaturas -> Entidades de gerenciamento
    - Explicação: A ordem segue do nível mais alto (entidades de gerenciamento) até os recursos.
