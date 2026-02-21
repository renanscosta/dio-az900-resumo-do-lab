# Máquinas Virtuais (VMs)

## O que são VMs?
Máquinas Virtuais (VMs) são ambientes de computação isolados que simulam uma máquina física. Elas permitem que múltiplos sistemas operacionais e aplicações sejam executados em um único hardware físico, proporcionando flexibilidade e eficiência no uso dos recursos.
Fornecem IaaS (Infrastructure as a Service), permitindo que os usuários criem, configurem e gerenciem suas próprias máquinas virtuais.

## Conjuntos de dimensionamento
Conjuntos de dimensionamento são grupos de VMs idênticas que podem ser gerenciadas como uma única unidade. Eles permitem a escalabilidade automática, onde o número de VMs pode ser ajustado automaticamente com base na demanda, garantindo desempenho e disponibilidade.

## Conjuntos de disponibilidade
Conjuntos de disponibilidade são grupos de VMs que garantem alta disponibilidade. Eles distribuem as VMs em diferentes domínios de falha e atualização, minimizando o impacto de falhas de hardware ou atualizações planejadas, garantindo que pelo menos uma VM esteja sempre disponível.

- **Domínio de falha**: Agrupa VMs em diferentes racks ou servidores para evitar que uma falha de hardware afete todas as VMs.
- **Domínio de atualização**: Agrupa VMs para que as atualizações sejam aplicadas a um grupo de VMs de cada vez, garantindo que nem todas as VMs sejam atualizadas simultaneamente, o que pode causar indisponibilidade.

![Image](/imagens/df-da.png)

# Área de Trabalho Virtual
Área de Trabalho Virtual é um ambiente de computação que permite aos usuários acessar um desktop virtual hospedado na nuvem ou em um data center. Ele oferece uma experiência de desktop completa, permitindo que os usuários acessem seus aplicativos e dados de qualquer lugar, usando qualquer dispositivo.
É uma mistura de PaaS e IaaS, onde os usuários têm controle sobre o ambiente de desktop virtual, mas a infraestrutura subjacente é gerenciada pelo provedor de serviços.

O acesso por ser:
- **Pool de VMs**: Os usuários compartilham um conjunto de VMs, onde cada VM pode ser usada por vários usuários, proporcionando uma solução econômica para ambientes com muitos usuários.
- **VM dedicada**: Cada usuário tem sua própria VM dedicada, garantindo desempenho e personalização, ideal para usuários com necessidades específicas ou que exigem maior desempenho.

# Containers
Containers são uma forma leve de virtualização que permite empacotar uma aplicação e suas dependências em um ambiente isolado. Eles compartilham o mesmo sistema operacional subjacente, mas cada container é executado de forma independente, proporcionando portabilidade e eficiência.
Fornecem PaaS (Platform as a Service), permitindo que os desenvolvedores criem, implantem e gerenciem aplicações sem se preocupar com a infraestrutura subjacente.

## Instâncias de Container
Instâncias de Container são uma forma de executar containers sem a necessidade de gerenciar a infraestrutura subjacente. Elas permitem que os usuários criem e executem containers de forma rápida e fácil, proporcionando uma solução escalável e eficiente para aplicações baseadas em containers.

## Aplicativos de Container
Semelhante às instâncias de container, mas com a capacidade de orquestrar e gerenciar múltiplos containers como um único aplicativo. Eles permitem que os usuários criem, implantem e gerenciem aplicativos baseados em containers de forma eficiente, proporcionando uma solução escalável e flexível para aplicações complexas.

## Orquestração de Containers
Orquestração de Containers é o processo de gerenciar e coordenar múltiplos containers para garantir que eles funcionem juntos de forma eficiente. Ferramentas como Kubernetes e Docker Swarm são usadas para orquestrar containers, permitindo que os usuários escalem, monitorem e gerenciem seus aplicativos baseados em containers de forma eficaz.
O Azure oferece serviços como o Azure Kubernetes Service (AKS) para facilitar a orquestração de containers na nuvem, proporcionando uma solução gerenciada para implantar e gerenciar aplicativos baseados em containers.

# Functions
Functions são uma forma de computação sem servidor (serverless) que permite aos desenvolvedores executar código em resposta a eventos sem se preocupar com a infraestrutura subjacente. Elas permitem que os usuários criem e executem funções de forma rápida e fácil, proporcionando uma solução escalável e eficiente para aplicações baseadas em eventos.
Fornecem PaaS (Platform as a Service), permitindo que os desenvolvedores criem, implantem e gerenciem funções sem se preocupar com a infraestrutura subjacente.
Os recursos de Functions são cobrados com base no número de execuções e no tempo de execução, proporcionando uma solução econômica para aplicações baseadas em eventos.

# Serviços de Aplicativos
Serviços de Aplicativos são uma plataforma gerenciada que permite aos desenvolvedores criar, implantar e gerenciar aplicativos web e móveis de forma eficiente. Eles fornecem uma solução escalável e flexível para aplicativos baseados em nuvem.
Fornecem PaaS (Platform as a Service), permitindo que os desenvolvedores criem, implantem e gerenciem aplicativos sem se preocupar com a infraestrutura subjacente.

## Tipos de Serviços de Aplicativos
- **Aplicativos Web**
O Serviço de Aplicativo inclui suporte completo para a hospedagem de aplicativos Web usando ASP.NET, ASP.NET Core, Java, Ruby, Node.js, PHP ou Python. Você pode escolher Windows ou Linux como sistema operacional do host.
- **Aplicativos de API**
Da mesma forma como se hospeda um site, você pode criar APIs Web baseadas em REST usando a linguagem e a estrutura que você quiser. Receba o suporte completo do Swagger e a capacidade de empacotar e publicar sua API no Azure Marketplace. Os aplicativos produzidos podem ser consumidos por qualquer cliente baseado em HTTP ou em HTTPS.
- **Aplicativos Móveis**
Você pode usar o recurso do WebJobs para executar um script (.cmd, .bat, PowerShell ou Bash) ou um programa (.exe, Java, PHP, Python ou Node.js) no mesmo contexto de um aplicativo Web, aplicativo de API ou aplicativo móvel. Eles também podem ser agendados ou executados por um gatilho. O WebJobs geralmente é usado para executar tarefas em segundo plano como parte da lógica do aplicativo.
- **WebJobs**
Use o recurso Aplicativos Móveis do Serviço de Aplicativo para criar rapidamente um back-end para aplicativos iOS e Android. Com apenas algumas ações no portal do Azure, você pode:

- Armazenar dados de aplicativo móvel em um Banco de Dados SQL baseado em nuvem.
- Autentique clientes em provedores sociais comuns, como MSA, Google, X e Facebook.
- Enviar notificações por push.
- Executar lógica de back-end personalizada em C# ou Node.js.
- No lado do aplicativo móvel, há suporte do SDK para aplicativos nativos para iOS, Android, Xamarin e React.

# Azure Virtual Network (VNet)
Azure Virtual Network (VNet) é um serviço de rede virtual que permite criar redes privadas na nuvem Azure. Ele fornece isolamento e controle sobre a rede, permitindo que os usuários criem sub-redes, configurem regras de segurança e estabeleçam conexões seguras entre suas redes locais e a nuvem Azure.

## Isolamento e segmentação de rede
O Azure VNet permite criar sub-redes dentro de uma rede virtual, proporcionando isolamento e segmentação de rede. Isso permite que os usuários organizem seus recursos de forma lógica e controlem o acesso entre diferentes partes da rede, melhorando a segurança e a eficiência.

## Conexão entre serviços
O Azure VNet permite estabelecer conexões seguras entre diferentes serviços e recursos na nuvem Azure. Isso inclui conexões entre VMs, bancos de dados, serviços de aplicativos e outros recursos, permitindo que os usuários criem arquiteturas de rede complexas e seguras para suas aplicações.

## Roteamento e segurança
O Azure VNet oferece recursos avançados de roteamento e segurança, permitindo que os usuários configurem regras de segurança, firewalls e grupos de segurança de rede para proteger seus recursos e controlar o tráfego de rede. Isso inclui a capacidade de criar regras de entrada e saída, configurar VPNs e estabelecer conexões seguras entre redes locais e a nuvem Azure, garantindo a segurança e a confiabilidade das aplicações e dados na nuvem.

## Conexão entre redes virtuais
O emparelhamento de redes virtuais é um recurso do Azure VNet que permite conectar duas ou mais redes virtuais dentro da mesma região ou em regiões diferentes. Isso permite que os recursos em diferentes redes virtuais se comuniquem entre si como se estivessem na mesma rede, proporcionando uma solução eficiente para arquiteturas de rede complexas e distribuídas na nuvem Azure.

## Gateway de VPN
O Gateway de VPN é um serviço do Azure VNet que permite estabelecer conexões seguras entre redes locais e a nuvem Azure usando VPNs (Virtual Private Networks). Ele suporta diferentes tipos de VPNs, incluindo VPNs de site a site, VPNs de ponto a site e VPNs de rede virtual, proporcionando uma solução flexível e segura para conectar redes locais à nuvem Azure e garantir a segurança e a confiabilidade das conexões de rede.
- **VPN baseada em política**: Usa regras de segurança para definir as rotas e as conexões, proporcionando uma solução mais simples para cenários de rede menos complexos.

- **VPN baseada em rota**: Usa o protocolo BGP para roteamento dinâmico, permitindo que as rotas sejam aprendidas e propagadas automaticamente entre as redes locais e a nuvem Azure.
    Use um gateway de VPN baseado em rota se precisar de qualquer um dos seguintes tipos de conectividade:
    - Conexões entre redes virtuais
    - Conexões ponto a site
    - Conexões multissite
    - Coexistência com um gateway do Azure ExpressRoute

### Cenários de alta disponibilidade
O Azure VNet oferece opções de alta disponibilidade para garantir que as conexões de rede sejam resilientes e confiáveis. 
- **Gateway de VPN ativo-ativo**: Configura dois ou mais gateways de VPN em modo ativo-ativo para garantir que, se um gateway falhar, o tráfego seja automaticamente redirecionado para o gateway restante, proporcionando alta disponibilidade e continuidade de negócios.
- **Gateway de VPN ativo-passivo**: Configura um gateway de VPN em modo ativo-passivo, onde um gateway é o principal e o outro é o backup. Se o gateway principal falhar, o gateway de backup assume automaticamente, garantindo alta disponibilidade e continuidade de negócios para as conexões de rede entre as redes locais e a nuvem Azure. Em casos de interrupções não planejadas, as conexões são restauradas em cerca de 90 segundos, proporcionando uma solução resiliente para conexões de rede críticas.
- **Gateway de VPN com redundância geográfica**: Configura gateways de VPN em diferentes regiões para garantir que, se uma região inteira ficar indisponível, as conexões de rede possam ser redirecionadas para outra região, proporcionando alta disponibilidade e resiliência para conexões de rede críticas entre as redes locais e a nuvem Azure.

## ExpressRoute
O Azure ExpressRoute é um serviço que permite estabelecer conexões privadas e dedicadas entre as redes locais e a nuvem Azure. Ele oferece uma alternativa mais rápida, segura e confiável em comparação com as conexões de internet pública, proporcionando uma solução ideal para empresas que exigem alta performance e segurança para suas conexões de rede com a nuvem Azure. O ExpressRoute é ideal para cenários que exigem alta largura de banda, baixa latência e conexões seguras entre as redes locais e a nuvem Azure, como migração de dados em larga escala, backup e recuperação de desastres, e aplicações críticas para os negócios. Ele oferece opções de conectividade flexíveis, incluindo conexões de peering privado, conexões de peering público e conexões de peering de Microsoft, permitindo que as empresas escolham a melhor opção para suas necessidades de conectividade com a nuvem Azure.

