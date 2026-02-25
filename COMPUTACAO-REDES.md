# Máquinas Virtuais (VMs)

## O que são VMs?
Máquinas Virtuais (VMs) são ambientes de computação isolados que simulam uma máquina física. Elas permitem que múltiplos sistemas operacionais e aplicações sejam executados em um único hardware físico.

- **Modelo de serviço:** IaaS (Infrastructure as a Service). O cliente gerencia SO, aplicações e dados; a Microsoft gerencia a infraestrutura.
- **Exemplo:** Migrar um servidor local para uma VM no Azure mantendo total controle sobre configurações.
- **Benefícios:** Escalabilidade, elasticidade e alta disponibilidade (com configuração adequada).

## Conjuntos de dimensionamento (Scale Sets)
Grupos de VMs idênticas que escalam automaticamente com base na demanda.
- **Exemplo:** Aumentar de 2 para 10 VMs durante Black Friday, reduzir após o pico.
- **Benefício:** Elasticidade e agilidade para lidar com variações de carga.

## Conjuntos de disponibilidade
Grupos de VMs distribuídas para garantir alta disponibilidade em caso de falhas.
- **Domínio de falha:** Separa VMs em racks/servidores diferentes para evitar falha em cascata.
- **Domínio de atualização:** Aplica atualizações gradualmente, mantendo parte do sistema disponível.
- **Exemplo:** 3 VMs em 3 domínios diferentes: se uma falha, 2 continuam rodando.

### Tabela Comparativa: Scale Sets x Availability Sets

| Aspecto | Conjuntos de dimensionamento | Conjuntos de disponibilidade |
|---|---|---|
| Propósito | Escalabilidade automática | Alta disponibilidade |
| Número de VMs | Aumenta/diminui dinamicamente | Quantidade fixa |
| Caso de uso | Atender picos de demanda | Tolerar falhas de hardware |
| Exemplo | App Web em Black Friday | Banco de dados crítico |

![Image](/imagens/df-da.png)

# Área de Trabalho Virtual
Ambiente de desktop hospedado na nuvem acessível de qualquer dispositivo. Mistura de PaaS e IaaS onde o cliente controla a experiência do usuário, mas a infraestrutura é gerenciada.

- **Pool compartilhado:** Vários usuários compartilham VMs, reduzindo custos. Exemplo: Call center com 100 operadores em 20 VMs.
- **VM dedicada:** Cada usuário tem sua própria VM. Exemplo: Equipe de design que precisa de alto desempenho.
- **Exemplo de uso:** Trabalhadores remotos acessam ambiente corporativo de home office em qualquer dispositivo.

# Containers
Formalismo leve de virtualização que empacota uma aplicação com suas dependências. Compartilham o SO do host, oferecendo eficiência e portabilidade.

- **Modelo de serviço:** PaaS. A Microsoft gerencia orquestração e infraestrutura.
- **Exemplo:** App Node.js em um container Docker roda igual em qualquer lugar (laptop, servidor, nuvem).
- **Benefício:** Agilidade e portabilidade.

## Instâncias de Container do Azure
Executar um único container rapidamente sem gerenciar infraestrutura.
- **Exemplo:** Deploy de um container com um script Python para processar arquivos.
- **Caso de uso:** Tarefas simples, curtas e isoladas.

## Azure Kubernetes Service (AKS)
Orquestrador de containers que gerencia múltiplos containers como um sistema. Skaliza, monitora e orquestra automaticamente.
- **Exemplo:** App com 1 container de API, 1 de banco, 1 de cache escalando conforme demanda.
- **Benefício:** Orquestração automática, tolerância a falhas, escalabilidade.

# Azure Functions
Computação serverless que executa código em resposta a eventos sem gerenciar infraestrutura.

- **Modelo de serviço:** PaaS. Você escreve apenas a função; a Microsoft gerencia o resto.
- **Cobrança:** Por execução e tempo de processamento. Ideal para cargas esporádicas.
- **Exemplo:** Função disparada quando um arquivo é enviado para Storage, processa e salva resultado.
- **Benefício:** Agilidade, custos otimizados (paga só pelo que usa), escalabilidade automática.

# Azure App Service
Plataforma PaaS gerenciada para hospedar aplicativos web, API, mobile e WebJobs.

- **Modelo de serviço:** PaaS. Você gerencia código; Azure gerencia infraestrutura, SO e routing.
- **Suporte:** ASP.NET, Node.js, Python, Java, Ruby, PHP em Windows ou Linux.
- **Exemplo:** App web em Node.js rodando em escala automática com HTTPS e domínio customizado.
- **Benefício:** Agilidade, escalabilidade, integração com ferramentas DevOps.

## Tipos de Cargas no App Service

| Tipo | O que é | Exemplo |
|---|---|---|
| **App Web** | Site ou aplicação web | Loja online em ASP.NET Core |
| **App de API** | API REST | API de cotação de moedas |
| **App Móvel** | Backend para app mobile | Backend de app iOS/Android |
| **WebJobs** | Tarefas em segundo plano | Processar fila de e-mails |

- **WebJobs:** Executam scripts ou programas em background. Podem rodar contínuos ou agendados.
  - Exemplo: Job que processa imagens enviadas por usuários a cada 15 minutos.

# Azure Virtual Network (VNet)
Rede privada na nuvem Azure com isolamento, segmentação e controle sobre conectividade.

- **Isolamento:** Recursos em uma VNet não são acessíveis de fora sem configuração explícita.
- **Sub-redes:** Segmentam a rede para organizar recursos e aplicar regras de segurança.
- **Exemplo:** VNet com sub-rede para VMs de frontend, outra para banco de dados.

## Grupo de Segurança de Rede (NSG)
Firewall virtual que controla tráfego de entrada e saída.
- **Regras:** Definem quem pode acessar o quê (porta, protocolo, IP origem).
- **Exemplo:** Bloquear SSH vindo de qualquer lugar, permitir apenas de IP corporativo.

## Emparelhamento de VNets
Conecta duas VNets para comunicação privada (mesma região ou cross-region).
- **Exemplo:** VNet "Produção" se comunica com VNet "Desenvolvimento".
- **Benefício:** Integração de ambientes sem usar internet pública.

## Gateway de VPN
Permite conexão segura entre rede local e VNet Azure via internet pública criptografada.

- **VPN Site-a-Site:** Conecta toda a rede local ao Azure. Exemplo: Filial da empresa com Azure.
- **VPN Ponto-a-Site:** Conecta usuários individuais ao Azure. Exemplo: Trabalho remoto seguro.
- **Exemplo:** Empresa com datacenter local criando túnel VPN seguro para produção no Azure.

### Tabela Comparativa: VPN vs ExpressRoute

| Aspecto | VPN | ExpressRoute |
|---|---|---|
| Conexão | Internet pública criptografada | Linha privada dedicada |
| Latência | Variável | Consistente e baixa |
| Largura de banda | Até ~1.25 Gbps | Até 100 Gbps |
| Custo | Mais baixo | Mais alto |
| Caso de uso | Conectividade básica | Aplicações críticas, alto volume |

## Azure ExpressRoute
Conexão privada dedicada entre rede local e Azure (não usa internet pública).

- **Benefício:** Baixa latência consistente, alta segurança, alta largura de banda.
- **Caso de uso:** Migrações em larga escala, aplicações críticas, backup/DR de dados massivos.
- **Exemplo:** Banco precisa de conexão de 50 Mbps garantida e segura para sistema de core banking na nuvem.
- **Custo:** Maior que VPN, mas justificável para aplicações críticas.

---

# Dicas para prova:
- **IaaS (VMs):** Cliente gerencia SO e aplicação; Microsoft gerencia hardware.
- **PaaS (App Service, Functions, Containers):** Cliente gerencia código; Microsoft gerencia infraestrutura.
- **Scale Sets:** Para elasticidade (variação de demanda); **Availability Sets:** Para alta disponibilidade.
- **VPN:** Conexão via internet criptografada; **ExpressRoute:** Linha privada dedicada.
- Em provas, procure por palavras-chave: "sem gerenciar infraestrutura" (PaaS), "total controle" (IaaS).

# Questões de exemplo para prova:
1. Qual serviço permite hospedar uma aplicação web sem se preocupar com gerenciamento de infraestrutura?
    - a) Máquinas Virtuais
    - b) Azure App Service **(correta)**
    - c) Azure Virtual Network
    - d) Azure ExpressRoute
    - Explicação: App Service é PaaS; você gerencia o código, Azure gerencia infraestrutura. VMs são IaaS (você gerencia SO).

2. Qual é a diferença principal entre Conjuntos de Dimensionamento e Conjuntos de Disponibilidade?
    - a) Scale Sets garantem alta disponibilidade; Availability Sets escalam automaticamente
    - b) Scale Sets escalam automaticamente; Availability Sets garantem alta disponibilidade **(correta)**
    - c) São a mesma coisa, nomes diferentes
    - d) Ambos fazem escalabilidade e alta disponibilidade
    - Explicação: Scale Sets = elasticidade (responder a picos); Availability Sets = tolerar falhas de hardware.

3. Qual serviço oferece conexão privada dedicada entre rede local e Azure?
    - a) VPN Site-to-Site
    - b) Azure Virtual Network
    - c) Azure ExpressRoute **(correta)**
    - d) Gateway de VPN
    - Explicação: ExpressRoute é linha privada; VPN usa internet criptografada. Para dados críticos, ExpressRoute é melhor.

4. Qual modelo de serviço Azure Functions representa?
    - a) IaaS
    - b) PaaS **(correta)**
    - c) SaaS
    - d) DaaS
    - Explicação: Functions é PaaS (serverless). Você escreve código; Azure gerencia escalabilidade, infraestrutura e cobrança por execução.

