# Benefícios da nuvem
- **Elasticidade:** Ajuste rápido de recursos para cima ou para baixo conforme a demanda, inclusive em picos e quedas inesperadas.
    - Exemplo: Aumentar instâncias de um app em uma campanha e reduzir após o término.

- **Escalabilidade:** Capacidade de crescer de forma planejada, horizontal (mais instâncias) ou vertical (mais capacidade por instância).
    - Exemplo: Migrar de uma VM pequena para outra maior quando o sistema cresce.

- **Alta disponibilidade:** Manter serviços disponíveis mesmo com falhas. Está ligada a redundância e SLAs definidos pelo provedor.
    - Exemplo: Distribuir VMs em zonas de disponibilidade para tolerar falhas locais.

### Tabela Comparativa: Elasticidade x Escalabilidade x Alta Disponibilidade

| Conceito | O que é | Como se aplica | Exemplo |
|---|---|---|---|
| Elasticidade | Ajuste rápido para cima/baixo | Responde a picos/quedas de demanda | Aumentar apps em Black Friday, reduzir depois |
| Escalabilidade | Crescimento planejado | Mais recursos de forma estruturada | Migrar VM pequena para grande conforme grow |
| Alta disponibilidade | Continuidade com falhas | Redundância e failover | Replicar dados em zonas diferentes |

A seguir, uma tabela com os tipos de SLA e seus respectivos tempos de inatividade por semana, mês e ano, conforme o Azure em fevereiro de 2026:

| SLA (%) | Tempo de inatividade por semana | Tempo de inatividade por mês | Tempo de inatividade por ano |
|--|--|--|--|
| 99.9% | 10.08 minutos | 43.2 minutos | 8.76 horas |
| 99.99% | 1.008 minutos | 4.32 minutos | 52.56 minutos |
| 99.999% | 0.1008 minutos | 0.432 minutos | 5.256 minutos |

- **Confiabilidade:** Infraestrutura robusta e distribuída para operar com resiliência e continuidade.
    - Exemplo: Replicação de dados para evitar perda em caso de falha de hardware.

- **Previsibilidade:** Custos e desempenho mais previsíveis com modelo OpEx (pague pelo uso) e SLAs claros.
    - Exemplo: Ajustar o orçamento com base no consumo mensal, sem grande CapEx inicial.

- **Segurança:** Proteções e conformidade oferecidas pelo provedor, dentro do modelo de responsabilidade compartilhada.
    - Exemplo: O provedor protege a infraestrutura; o cliente configura MFA e permissões de acesso.

- **Governança:** Controle de políticas, auditoria e conformidade para uso adequado dos recursos.
    - Exemplo: Aplicar políticas que bloqueiam a criação de recursos fora da região aprovada.

- **Gerenciamento:** Ferramentas para monitorar, automatizar e operar recursos de forma centralizada.
    - Exemplo: Usar Azure Monitor para alertas de uso de CPU e disponibilidade.

## Meios para criar e gerenciar os recursos
- **Portal do Azure:** Interface gráfica baseada na web para criar e gerenciar recursos.
- **Azure CLI:** Linha de comando para automação e gerenciamento.
- **Azure PowerShell:** Cmdlets para scripts e automações.
- **Azure Resource Manager (ARM) Templates:** Infraestrutura como código com JSON.
- **Azure SDKs:** Bibliotecas para integração em aplicações.
- **Azure REST API:** Chamadas HTTP para gerenciamento programático.

# Dicas para prova:
- Elasticidade lida com variação rápida de demanda; escalabilidade é crescimento planejado.
- Alta disponibilidade está ligada a redundância e SLA.
- O modelo OpEx e o pagamento por uso reforçam previsibilidade de custos.
- Segurança segue o modelo de responsabilidade compartilhada.

# Questões de exemplo para prova:
1. Qual benefício está ligado ao ajuste rápido de recursos em picos de demanda?
    - a) Escalabilidade
    - b) Elasticidade **(correta)**
    - c) Governança
    - d) Previsibilidade
    - Explicação: Elasticidade é a capacidade de responder rapidamente a mudanças de demanda, escalando para cima e para baixo automaticamente.

2. Qual benefício descreve manter o serviço disponível mesmo em caso de falhas?
    - a) Confiabilidade
    - b) Alta disponibilidade **(correta)**
    - c) Elasticidade
    - d) Governança
    - Explicação: Alta disponibilidade garante continuidade de serviço com redundância; confiabilidade é sobre qualidade e resiliência da infraestrutura.

3. Qual benefício está mais associado ao modelo de pagamento por uso (OpEx)?
    - a) Previsibilidade **(correta)**
    - b) Confiabilidade
    - c) Segurança
    - d) Escalabilidade
    - Explicação: OpEx oferece custo previsível baseado no consumo real, permitindo orçamento flexível sem investimento inicial (CapEx).
