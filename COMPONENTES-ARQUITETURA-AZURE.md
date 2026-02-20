# Componentes de Arquitetura Azure

## Região e Zona de Disponibilidade ##

- **Região:** Localização geográfica onde os serviços de nuvem estão disponíveis. Cada região é composta por vários data centers, e as empresas podem escolher a região mais próxima para reduzir a latência e melhorar o desempenho, mas quanto mais perto a região estiver do usuário final, melhor será a experiência. Essa escolha pode influenciar em custos, pois os preços podem variar entre regiões, e também pode afetar a conformidade regulatória, já que algumas regiões podem ter requisitos específicos de conformidade.

- **Zona de Disponibilidade:** Subdivisão dentro de uma região que é isolada de falhas em outras zonas. Cada zona de disponibilidade é composta por um ou mais data centers (preferencialmente no mínimo três para garantir alta disponibilidade), e as empresas podem distribuir seus recursos entre diferentes zonas para garantir alta disponibilidade e resiliência. 

- Quanto mais disponíbilidade for necessária, mais caro é;
- Nem todas as regiões possuem zonas de disponibilidade, e nem todos os serviços estão disponíveis em todas as zonas de disponibilidade. Portanto, é importante verificar a disponibilidade dos serviços e das zonas de disponibilidade na região escolhida antes de planejar a arquitetura da aplicação;

Alguns tipos de serviços nas zonas de disponibilidade:
- **Serviços de zona**: São serviços que são implantados em uma única zona de disponibilidade, o que significa que eles não têm alta disponibilidade. Esses serviços são adequados para cargas de trabalho que não exigem alta disponibilidade ou para ambientes de desenvolvimento e teste. Exemplos incluem máquinas virtuais (VMs) e bancos de dados SQL.
- **Serviços com redundância de zona**: São serviços que são implantados em várias zonas de disponibilidade dentro da mesma região, o que significa que eles têm alta disponibilidade. Esses serviços são adequados para cargas de trabalho críticas que exigem alta disponibilidade e resiliência. Exemplos incluem Azure App Service, Azure SQL Database e Azure Kubernetes Service (AKS).
- **Serviços não regionais**: São serviços que são implantados globalmente e não estão vinculados a uma região específica. Esses serviços são adequados para cargas de trabalho que exigem alta disponibilidade global e resiliência. Exemplos incluem Azure Cosmos DB, Azure Active Directory e Azure Traffic Manager.

![Imagem](imagens/zona_disponibilidade.png)
imagem retirada do site oficial do Azure: https://azure.microsoft.com/pt-br/global-infrastructure/availability-zones/


### Pares de região ###
- São regiões emparelhadas dentro da mesma geografia, projetadas para fornecer recuperação de desastres e alta disponibilidade. Os pares de região permitem que as empresas repliquem seus dados e aplicativos entre as regiões emparelhadas, garantindo que, em caso de falha em uma região, os serviços possam ser rapidamente restaurados na região emparelhada. Os pares de região são projetados para fornecer uma recuperação de desastres eficiente, com replicação de dados assíncrona e failover automático. 

- Alguns serviços precisam ser configurados pelo cliente para aproveitar os benefícios dos pares de região, como o Azure Site Recovery, que permite replicar máquinas virtuais entre regiões emparelhadas para garantir a continuidade dos negócios em caso de falha. Outros serviços, como o Azure SQL Database, oferecem opções de replicação geográfica integrada que permitem replicar bancos de dados entre regiões emparelhadas para garantir alta disponibilidade e resiliência.

- Nem todas as regiões possuem pares de região, e nem todos os serviços estão disponíveis em todas as regiões. Portanto, é importante verificar a disponibilidade dos serviços e dos pares de região na região escolhida antes de planejar a arquitetura da aplicação.

- Algumas regiões fazem backup bi direcional, ou seja, cada região é o par da outra, enquanto outras regiões fazem backup unidirecional, onde uma região é o par da outra, mas a outra região não é o par da primeira. Por exemplo, a região Leste dos EUA é o par da região Oeste dos EUA, e a região Oeste dos EUA é o par da região Leste dos EUA, enquanto a região Leste dos EUA 2 é o par da região Leste dos EUA, mas a região Leste dos EUA não é o par da região Leste dos EUA 2.

![Imagem](imagens/par-regioes.png)
imagem retirada do site oficial do Azure: https://azure.microsoft.com/pt-br/global-infrastructure/geographies/


## Regiões Soberanas ##
- São regiões que atendem a requisitos específicos de conformidade e regulamentação, como requisitos de soberania de dados, onde os dados devem permanecer dentro de um país ou região específica. As regiões soberanas são projetadas para atender às necessidades de clientes que operam em setores altamente regulamentados, como governo, saúde e finanças, onde a conformidade com regulamentos específicos é essencial.

### US DoD Central, US Government, US Gov Virginia, US Gov Arizona ###
- São regiões soberanas projetadas para atender às necessidades do governo dos Estados Unidos, incluindo o Departamento de Defesa (DoD) e outras agências governamentais. Essas regiões oferecem recursos e serviços específicos para atender aos requisitos de segurança e conformidade do governo dos EUA, como FedRAMP, DoD SRG e CJIS. Essas regiões são isoladas das regiões comerciais do Azure e são operadas por pessoal de segurança do governo dos EUA, garantindo que os dados e recursos dos clientes sejam protegidos de acordo com os padrões de segurança do governo dos EUA.

### Azure China 21Vianet ###
- É uma região soberana operada pela 21Vianet, uma empresa de internet chinesa, que atende às necessidades de clientes na China, onde os dados devem permanecer dentro do país. A região Azure China 21Vianet oferece recursos e serviços específicos para atender aos requisitos de conformidade e regulamentação da China, como a Lei de Segurança Cibernética da China. Essa região é isolada das regiões comerciais do Azure e é operada pela 21Vianet, garantindo que os dados e recursos dos clientes sejam protegidos de acordo com os padrões de segurança da China.

## Grupos de Recursos ##
- São contêineres lógicos que agrupam recursos relacionados, facilitando a organização, gerenciamento e monitoramento dos recursos na nuvem. Os grupos de recursos permitem que as empresas organizem seus recursos de forma lógica, com base em critérios como projeto, departamento ou ambiente, facilitando a gestão e o monitoramento dos recursos. Os grupos de recursos também permitem que as empresas apliquem políticas de governança e controle de acesso de forma centralizada, garantindo que os recursos sejam gerenciados de forma eficiente e segura. Além disso, os grupos de recursos também permitem que as empresas monitorem o uso e os custos dos recursos de forma centralizada, facilitando a otimização dos custos na nuvem.

    - Os recursos só podem estar em um grupo de recursos, mas um grupo de recursos pode conter vários recursos. Os grupos de recursos também podem conter outros grupos de recursos, permitindo uma hierarquia de organização dos recursos na nuvem.
    - Os recursos podem estar em regiões diferentes, mas devem estar no mesmo grupo de recursos. Isso permite que as empresas organizem seus recursos de forma lógica, independentemente da localização geográfica dos recursos.

## Assinaturas ##
- São unidades de faturamento e gerenciamento que permitem que as empresas organizem seus recursos e controlem seus custos na nuvem. As assinaturas permitem que as empresas criem e gerenciem seus recursos de forma eficiente, com base em critérios como projeto, departamento ou ambiente, facilitando a gestão e o monitoramento dos recursos. As assinaturas também permitem que as empresas apliquem políticas de governança e controle de acesso de forma centralizada, garantindo que os recursos sejam gerenciados.

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
​## Grupos de Gerenciamento ##

- São contêineres lógicos que permitem organizar e gerenciar várias assinaturas de forma hierárquica. Os grupos de gerenciamento permitem que as empresas organizem suas assinaturas de forma lógica, com base em critérios como projeto, departamento ou ambiente, facilitando a gestão e o monitoramento das assinaturas. Os grupos de gerenciamento também permitem que as empresas apliquem políticas de governança e controle de acesso de forma centralizada, garantindo que as assinaturas sejam gerenciadas de forma eficiente e segura. Além disso, os grupos de gerenciamento também permitem que as empresas monitorem o uso e os custos das assinaturas de forma centralizada, facilitando a otimização dos custos na nuvem.
- Um grupo de gerenciamento pode conter várias assinaturas, e uma assinatura pode estar em apenas um grupo de gerenciamento. Os grupos de gerenciamento também podem conter outros grupos de gerenciamento, permitindo uma hierarquia de organização das assinaturas na nuvem.

![Imagem](imagens/grupos-gerenciamento.png)
imagem retirada do site oficial do Azure: https://azure.microsoft.com/pt-br/overview/management-groups/
