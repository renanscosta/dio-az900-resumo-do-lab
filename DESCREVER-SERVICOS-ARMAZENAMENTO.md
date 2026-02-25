# Contas de Armazenamento no Azure
Fornecem armazenamento escalável e seguro para dados, arquivos, blobs, filas e tabelas. São essenciais para armazenar dados de aplicativos, backups e arquivos de log. Devem possuir nome único, pois esse nome é como se fosse um identificador global para acessar os dados armazenados. 

**Ao nomear sua conta de armazenamento, lembre-se dessas regras:**
- Os nomes da conta de armazenamento devem ter entre 3 e 24 caracteres e podem conter apenas números e letras minúsculas.
- O nome da sua conta de armazenamento deve ser exclusivo no Azure. Duas contas de armazenamento não podem ter o mesmo nome. Isso dá suporte à capacidade de ter um namespace exclusivo e acessível no Azure.


## Tipos de Contas de Armazenamento
- **Standard general-purpose v2 (GPv2)**: Suporta todos os tipos de armazenamento (blobs, arquivos, filas e tabelas) e é recomendado para a maioria dos casos.
- **Premium block blobs**: Otimizada para desempenho de blocos de dados, ideal para cargas de trabalho que exigem alta taxa de transferência e baixa latência.
    - Exemplo: Armazenamento de grandes arquivos de mídia ou dados de análise que exigem acesso rápido.
- **Premium file shares**: Projetada para compartilhamento de arquivos de alto desempenho, ideal para cargas de trabalho que exigem acesso rápido a arquivos.
    - Exemplo: Armazenamento de arquivos para aplicativos que exigem acesso rápido, como servidores de arquivos ou aplicativos de compartilhamento de arquivos.
- **Premium page blobs**: Otimizada para desempenho de páginas de dados, ideal para cargas de trabalho que exigem acesso rápido a páginas de dados, como máquinas virtuais.
    - Exemplo: Armazenamento de discos de máquinas virtuais que exigem acesso rápido a páginas de dados.

## Pontos de extremidade de serviço

| Serviço de armazenamento | Endpoint |
|--------------------------|----------|
| Armazenamento de Blobs | `https://<storage-account-name>.blob.core.windows.net` |
| Data Lake Storage Gen2 | `https://<storage-account-name>.dfs.core.windows.net` |
| Arquivos do Azure | `https://<storage-account-name>.file.core.windows.net` |
| Armazenamento de Filas | `https://<storage-account-name>.queue.core.windows.net` |
| Armazenamento de Tabelas | `https://<storage-account-name>.table.core.windows.net` |

# Redundância e Replicação
Até o momento, o padrão de replicação são de ,no mínimo, três cópias dos dados para garantir a durabilidade. O Azure oferece diferentes opções de redundância para atender às necessidades de negócios e garantir a disponibilidade dos dados em caso de falhas ou desastres.
As opções incluem:

- **Locally-redundant storage (LRS)**: Replica os dados três vezes dentro de um único data center na mesma região. Protege contra falhas de hardware, mas não contra falhas de data center ou desastres naturais. Essa opção possui um SLA de 99,999999999% (11 noves) de durabilidade dos dados ao longo de um ano.

- **Zone-redundant storage (ZRS)**: Replica os dados em três zonas de disponibilidade (data centers separados) dentro da mesma região. Protege contra falhas de zona, mas não contra falhas de região ou desastres naturais. Essa opção possui um SLA de 99,9999999999% (12 noves) de durabilidade dos dados ao longo de um ano.

- **Geo-redundant storage (GRS)**: Utiliza LRS para replicar os dados em uma região primária e, em seguida, replica os dados para uma região secundária geograficamente distante, também utilizando LRS. Protege contra falhas de região e desastres naturais. Essa opção possui um SLA de 99,99999999999999% (16 noves) de durabilidade dos dados ao longo de um ano.

- **Geo-zone-redundant storage (GZRS)**: Combina ZRS e GRS para replicar os dados em três zonas de disponibilidade dentro da região primária e, em seguida, replica os dados para uma região secundária geograficamente distante, utilizando LRS. Protege contra falhas de zona, falhas de região e desastres naturais. Essa opção possui um SLA de 99,99999999999999% (16 noves) de durabilidade dos dados ao longo de um ano.

### Leituras na região secundária
- **Read-access geo-redundant storage (RA-GRS)**: Permite acesso de leitura aos dados na região secundária, além da replicação GRS. Isso é útil para cenários de recuperação de desastres, onde os dados podem ser lidos mesmo que a região primária esteja indisponível. 
- **Read-access geo-zone-redundant storage (RA-GZRS)**: Permite acesso de leitura aos dados na região secundária, além da replicação GZRS. Isso é útil para cenários de recuperação de desastres, onde os dados podem ser lidos mesmo que a região primária esteja indisponível.

## Failover
O processo de failover para GRS e GZRS é manual, o que significa que o cliente deve iniciar o failover para a região secundária em caso de falha na região primária. O failover pode levar algum tempo para ser concluído, dependendo do tamanho dos dados e da carga de trabalho. Durante o processo de failover, os dados na região secundária se tornam a nova região primária, e a região primária original se torna a nova região secundária. Após o failover, os dados são replicados novamente para garantir a continuidade da proteção contra falhas.

É possível habilitar a leitura na região secundária mesmo que a região primária esteja operacional, o que pode ser útil para cenários de recuperação de desastres ou para acessar os dados em caso de falha na região primária. No entanto, é importante lembrar que a leitura na região secundária pode ter latência mais alta do que a leitura na região primária, devido à distância geográfica entre as regiões. Outro ponto a destacar, é que a sincronização entre as regiões primária e secundária pode levar algum tempo, o que significa que os dados na região secundária podem não estar atualizados em tempo real. Portanto, é importante considerar esses fatores ao habilitar a leitura na região secundária e planejar adequadamente para garantir a continuidade dos negócios em caso de falha na região primária.

**RPO (Recovery Point Objective)**: O tempo máximo tolerável para perda de dados em caso de falha. Para GRS e GZRS, o RPO é de até 15 minutos, o que significa que os dados na região secundária podem estar atrasados em até 15 minutos em relação à região primária.

# Serviços de Armazenamento
- **Armazenamento de Blobs**: Armazena grandes quantidades de dados não estruturados, como arquivos de mídia, documentos e backups. Os blobs são organizados em containers, que são semelhantes a pastas. Os tipos de blobs incluem blocos, páginas e anexos, cada um otimizado para diferentes cenários de uso.

- **Data Lake Storage Gen2**: Oferece armazenamento de dados otimizado para análise de big data, combinando as capacidades de armazenamento de blobs com recursos de hierarquia de arquivos. É ideal para cenários de análise de dados em larga escala, como processamento de dados e machine learning.

- **Arquivos do Azure**: Fornece compartilhamento de arquivos gerenciado na nuvem, permitindo que os aplicativos acessam arquivos usando o protocolo SMB (Server Message Block). É ideal para cenários de compartilhamento de arquivos entre máquinas virtuais ou para migração de servidores de arquivos locais para a nuvem.

- **Armazenamento de Filas**: Oferece um serviço de mensagens para comunicação assíncrona entre componentes de aplicativos. As filas permitem que os aplicativos se comuniquem de forma confiável, mesmo quando estão em execução em ambientes distribuídos ou quando enfrentam falhas temporárias.

- **Armazenamento de Tabelas**: Fornece um serviço de armazenamento NoSQL para dados estruturados, permitindo que os aplicativos armazenem e consultem grandes volumes de dados de forma escalável. As tabelas são organizadas em partições, o que permite consultas eficientes e escalabilidade horizontal. Exemplo: Armazenamento de dados de telemetria, logs de aplicativos ou dados de sessão para aplicativos web.

# Camadas de Acesso
As camadas de acesso permitem que os clientes otimizem os custos de armazenamento com base na frequência de acesso aos dados. As camadas de acesso incluem:

- **Hot**: Para dados acessados com frequência. Os custos de armazenamento são mais altos, mas os custos de acesso são mais baixos. Exemplo: Dados de aplicativos ativos, arquivos de log recentes ou dados de telemetria que precisam ser acessados rapidamente.

- **Cool ou Esporádico**: Para dados acessados com menos frequência e que possuem um tempo de retenção mínimo de 30 dias. Os custos de armazenamento são mais baixos do que a camada Hot, mas os custos de acesso são mais altos. Exemplo: Dados de backup, arquivos de mídia que não são acessados com frequência ou dados de telemetria antigos.

- **Cold ou Fria**: Para dados acessados raramente e que possuem um tempo de retenção mínimo de 90 dias. Os custos de armazenamento são os mais baixos, mas os custos de acesso são os mais altos. Exemplo: Arquivos de backup de longo prazo, dados de conformidade ou arquivos de mídia que não são acessados por longos períodos.

- **Archive ou Arquivo morto**: Para dados que não são acessados e que possuem um tempo de retenção mínimo de 180 dias. Os custos de armazenamento são os mais baixos, mas os custos de acesso são os mais altos, e o acesso aos dados pode levar várias horas. Exemplo: Dados de conformidade de longo prazo, arquivos de backup que não precisam ser acessados por longos períodos ou dados de telemetria antigos que precisam ser mantidos para análise histórica.

# Migração de Dados
O Azure oferece várias ferramentas e serviços para facilitar a migração de dados para as contas de armazenamento, incluindo:

- **Azure Data Box**: Um dispositivo físico que pode ser enviado para o cliente para coletar grandes volumes de dados localmente e, em seguida, enviar o dispositivo de volta para a Microsoft para upload para o Azure. É ideal para migrações de dados em larga escala, especialmente quando a largura de banda da rede é limitada. Exemplo: Migração de grandes volumes de dados de um data center local para o Azure, como arquivos de mídia, backups ou dados de telemetria. Hoje a Microsoft oferece dispositivos com capacidade de até 1 PB, o que é ideal para migrações de dados em larga escala.

- **Migrações para Azure: Descoberta e avaliação**: Uma ferramenta que ajuda a descobrir e avaliar os dados locais para migração para o Azure. Ela fornece insights sobre os dados, como tamanho, tipo e dependências, para ajudar a planejar a migração de forma eficiente. Exemplo: Avaliação de dados locais para identificar quais arquivos ou conjuntos de dados são adequados para migração para o Azure, como arquivos de mídia, backups ou dados de telemetria.

- **Migrações para Azure: Migração de Servidor**: Uma ferramenta que ajuda a migrar servidores locais para o Azure, incluindo a migração de dados para as contas de armazenamento. Ela suporta a migração de servidores físicos e virtuais, e pode ser usada para migrar dados de arquivos, bancos de dados e aplicativos. Exemplo: Migração de um servidor local para o Azure, incluindo a migração de arquivos de mídia, backups ou dados de telemetria para as contas de armazenamento do Azure. Suporte a VMware, Hyper-V e servidores físicos, o que torna a migração de dados mais flexível e eficiente.

- **Serviço de Migração de Banco de Dados do Azure**: Uma ferramenta que ajuda a migrar bancos de dados locais para o Azure, incluindo a migração de dados para as contas de armazenamento. Ela suporta a migração de bancos de dados SQL Server, MySQL, PostgreSQL e MongoDB, e pode ser usada para migrar dados de bancos de dados relacionais e NoSQL. Exemplo: Migração de um banco de dados local para o Azure, incluindo a migração de dados para as contas de armazenamento do Azure. Suporte a uma variedade de bancos de dados, o que torna a migração de dados mais flexível e eficiente.

- **Assistente de Migração do Serviço de Aplicativo do Azure**: Migração de sites locais (.NET e PHP) para o Azure App Service, incluindo a migração de dados para as contas de armazenamento. Ele pode ser usado para migrar dados de arquivos, bancos de dados e aplicativos. Exemplo: Migração de um site local para o Azure App Service, incluindo a migração de arquivos de mídia, backups ou dados de telemetria para as contas de armazenamento do Azure. 

# Gerenciamento de Contas de Armazenamento
As contas de armazenamento podem ser gerenciadas por meio do portal do Azure, Azure CLI, PowerShell ou APIs REST. Os clientes podem configurar opções de segurança, como criptografia, controle de acesso e monitoramento, para garantir a proteção dos dados armazenados. Além disso, os clientes podem configurar alertas e notificações para monitorar o uso e o desempenho das contas de armazenamento, e podem usar ferramentas de análise para obter insights sobre o uso e o desempenho das contas de armazenamento, como o Azure Monitor e o Azure Storage Analytics. O gerenciamento eficiente das contas de armazenamento é essencial para garantir a segurança, a disponibilidade e o desempenho dos dados armazenados no Azure, e para otimizar os custos de armazenamento com base nas necessidades de negócios.

- **AzCopy**: Uma ferramenta de linha de comando que permite transferir dados para e a partir das contas de armazenamento do Azure. Faz sincronização em apenas uma direção, o que significa que os dados são transferidos apenas do local para o Azure ou do Azure para o local, mas não em ambas as direções. Exemplo: Transferência de arquivos de mídia, backups ou dados de telemetria para as contas de armazenamento do Azure usando a linha de comando, o que pode ser útil para automação ou para transferências em larga escala.

- **Azure Storage Explorer ou Gerenciador de Armazenamento do Azure**: Uma ferramenta gráfica que permite gerenciar as contas de armazenamento do Azure, incluindo a criação, configuração e monitoramento das contas de armazenamento. Por baixo dos panos utiliza o AzCopy. Exemplo: Gerenciamento de contas de armazenamento do Azure usando uma interface gráfica, o que pode ser útil para usuários que preferem uma abordagem visual para gerenciamento de recursos.

- **Azure File Sync ou Sincronização de arquivos do Azure**: Um serviço que permite sincronizar arquivos entre servidores locais e as contas de armazenamento do Azure. Ele pode ser usado para manter os arquivos atualizados em ambos os locais, o que é útil para cenários de compartilhamento de arquivos ou para garantir a disponibilidade dos arquivos em caso de falha no local. 


# Dicas para a prova:
- Lembre-se de que as contas de armazenamento são usadas para armazenar dados, arquivos, blobs, filas e tabelas, e que cada tipo de conta de armazenamento é otimizado para diferentes cenários de uso.
- Entenda as opções de redundância e replicação, e como elas afetam a durabilidade e a disponibilidade dos dados.
- Familiarize-se com as camadas de acesso e como elas podem ser usadas para otimizar os custos de armazenamento com base na frequência de acesso aos dados.
- Conheça as ferramentas e serviços disponíveis para migração de dados para as contas de armazenamento, e como eles podem ser usados para facilitar a migração de dados para o Azure.
- Esteja ciente das opções de gerenciamento disponíveis para as contas de armazenamento, e como elas podem ser usadas para garantir a segurança, a disponibilidade e o desempenho dos dados armazenados no Azure.

# Questões de exemplo para a prova:
1. Qual tipo de conta de armazenamento é recomendado para armazenar grandes quantidades de dados não estruturados, como arquivos de mídia, documentos e backups?
    - a) Standard general-purpose v2 (GPv2) **(correta)**
    - b) Premium block blobs
    - c) Premium file shares
    - d) Premium page blobs
    
    - Resumo: A GPv2 cobre blobs, arquivos, filas e tabelas no mesmo recurso, oferecendo flexibilidade e bom custo-benefício (OpEx) para a maioria dos cenarios.

2. Qual opção de redundância é recomendada para proteger os dados contra falhas de região e desastres naturais?
    - a) Locally-redundant storage (LRS)
    - b) Zone-redundant storage (ZRS)
    - c) Geo-redundant storage (GRS) **(correta)**
    - d) Geo-zone-redundant storage (GZRS)
    
    - Resumo: O GRS replica para outra regiao, garantindo tolerancia a falhas regionais e maior disponibilidade; o GZRS adiciona protecao por zona, o que nao foi exigido no enunciado.

3. Qual camada de acesso é recomendada para dados que são acessados com frequência?
    - a) Hot **(correta)**
    - b) Cool ou Esporádico
    - c) Cold ou Fria
    - d) Archive ou Arquivo morto
    
    - Resumo: A camada Hot prioriza baixa latencia e maior desempenho para dados acessados com frequencia, favorecendo agilidade no uso diario.

4. Qual ferramenta de migração é recomendada para migrar grandes volumes de dados de um data center local para o Azure, especialmente quando a largura de banda da rede é limitada?
    - a) Azure Data Box **(correta)**
    - b) Migrações para Azure: Descoberta e avaliação
    - c) Migrações para Azure: Migração de Servidor
    - d) Serviço de Migração de Banco de Dados do Azure
    
    - Resumo: O Azure Data Box permite migracao offline de grandes volumes quando a rede e limitada, acelerando a transferencia e reduzindo impacto operacional.

5. Qual ferramenta de gerenciamento é recomendada para transferir dados para e a partir das contas de armazenamento do Azure usando a linha de comando?
    - a) AzCopy **(correta)**
    - b) Azure Storage Explorer ou Gerenciador de Armazenamento do Azure
    - c) Azure File Sync ou Sincronização de arquivos do Azure
    - d) Azure Monitor
    
    - Resumo: O AzCopy e a opcao de CLI para copiar dados com eficiencia e automacao, ideal para rotinas de transferencia em escala.
    