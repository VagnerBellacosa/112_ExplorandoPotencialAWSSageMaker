# O que é o Amazon S3?

[PDF](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/s3-userguide.pdf#Welcome)

[RSS](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/s3-userguide-rss-updates.rss)



O Amazon Simple Storage Service (Amazon S3) é um serviço de armazenamento de objetos que oferece escalabilidade líder do setor, disponibilidade de dados, segurança e performance. Clientes de todos os tamanhos e setores podem usar o Amazon S3 para armazenar e proteger qualquer volume de dados para uma variedade de casos de uso, como data lakes, sites, aplicações móveis, backup e restauração, arquivamento, aplicações corporativas, dispositivos IoT e análises de big data. O Amazon S3 fornece recursos de gerenciamento para que você possa otimizar, organizar e configurar o acesso aos seus dados para atender aos seus requisitos específicos de negócios, organizacionais e de compatibilidade.

**Tópicos**

- [Recursos do Amazon S3](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#S3Features)
- [Como funciona o Amazon S3](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#CoreConcepts)
- [Modelo de consistência de dados do Amazon S3](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#ConsistencyModel)
- [Serviços relacionados](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#RelatedAmazonWebServices)
- [Acesso ao Amazon S3](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#API)
- [Pagar pelo Amazon S3](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#PayingforStorage)
- [Conformidade do PCI DSS](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#pci-dss-compliance)

## Recursos do Amazon S3

### Classes de armazenamento

O Amazon S3 oferece uma ampla variedade de classes de armazenamento para diferentes casos de uso. Por exemplo, você pode armazenar dados de produção essenciais à missão no S3 Standard para acesso frequente, economizar custos armazenando dados acessados com pouca frequência no S3 Standard-IA ou S3 One Zone-IA e arquivar dados com os menores custos no S3 Glacier e no S3 Glacier Deep Archive.

Você pode armazenar dados com padrões de acesso alterados ou desconhecidos no S3 Intelligent-Tiering, o que otimiza os custos de armazenamento movendo automaticamente seus dados entre quatro camadas de acesso quando seus padrões de acesso mudam. Esses quatro níveis de acesso incluem dois níveis de acesso de baixa latência otimizados para acesso frequente e infrequente e dois níveis de acesso de arquivamento de inclusão projetados para acesso assíncrono para dados acessados raramente.

Para obter mais informações, consulte [Uso de classes de armazenamento do Amazon S3](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/storage-class-intro.html). Para obter mais informações sobre o S3 Glacier, consulte o [*Guia do desenvolvedor do Amazon S3 Glacier*](https://docs.aws.amazon.com/amazonglacier/latest/dev/introduction.html).

### Gerenciamento de armazenamento

O Amazon S3 tem recursos de gerenciamento de armazenamento que você pode usar para gerenciar custos, atender aos requisitos normativos, reduzir a latência e salvar várias cópias distintas de seus dados para requisitos de compatibilidade.

- [S3 Lifecycle](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html): configura uma política de ciclo de vida para gerenciar seus objetos e armazená-los de maneira econômica durante todo o ciclo de vida. Você pode fazer a transição de objetos para outras classes de armazenamento do S3 ou expirar objetos que atingem o fim de suas vidas.
- [Bloqueio de objetos do S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock.html): evita que os objetos do Amazon S3 sejam excluídos ou substituídos por um período de tempo fixo ou indefinidamente. Você pode usar o bloqueio de objetos para ajudar a atender aos requisitos regulamentares que exigem armazenamento *write-once-read-many* *(WORM)* ou simplesmente adicionar outra camada de proteção contra alterações e exclusão de objetos.
- [Replicação do S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/replication.html): replica objetos e seus respectivos metadados e etiquetas de objeto para um ou mais buckets de destino nas mesmas Regiões da AWS , ou diferentes, para reduzir a latência, compatibilidade, segurança e outros casos de uso.
- [Operações em lote do S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/batch-ops.html): gerencia bilhões de objetos em escala com uma única solicitação de API do S3 ou com alguns cliques no console do Amazon S3. Você pode usar operações em lote para executar operações como **Copy** (Copiar), **Invoke AWS Lambda function** (Chamar função Lambda da AWS) e **Restore** (Restaurar) em milhões ou bilhões de objetos.

### Gerenciamento de acesso

O Amazon S3 fornece recursos para auditoria e gerenciamento de acesso a seus buckets e objetos. Por padrão, os buckets do S3 e os objetos deles são privados. Você tem acesso somente aos recursos do S3 criados. Para conceder permissões de recursos detalhadas que suportam seu caso de uso específico ou para auditar as permissões de seus recursos do Amazon S3, você pode usar os seguintes recursos.

- [Bloqueio de acesso público do S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-control-block-public-access.html): bloqueie o acesso público a buckets e objetos do S3. Por padrão, as configurações de bloqueio de acesso público são ativadas no nível da conta e do bucket.
- [AWS Identity and Access Management (IAM)](https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-access-control.html): crie usuários do IAM para sua Conta da AWS para gerenciar o acesso aos recursos do Amazon S3. Por exemplo, você pode usar o IAM com o Amazon S3 para controlar o tipo de acesso de um usuário ou grupo de usuários a um bucket do S3 pertencentes à sua Conta da AWS .
- [Políticas de buckets](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-policies.html): use a linguagem de política baseada em IAM para configurar permissões baseadas em recursos para os buckets do S3 e os objetos neles contidos.
- [Listas de controle de acesso (ACLs)](https://docs.aws.amazon.com/AmazonS3/latest/userguide/acls.html): conceda permissões de leitura e gravação para buckets e objetos individuais a usuários autorizados. Como regra geral, recomendamos o uso de políticas baseadas em recursos do S3 (políticas de bucket e políticas de ponto de acesso) ou políticas do IAM para controle de acesso, em vez de ACLs. ACLs são mecanismos de controle de acesso que antecedem políticas baseadas em recursos e IAM. Para obter mais informações sobre quando você usaria ACLs, em vez de políticas baseadas em recursos ou políticas do IAM, consulte [Diretrizes para políticas de acesso](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/access-policy-alternatives-guidelines.html).
- [Analisador de acesso para S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-analyzer.html): avalie e monitore suas políticas de acesso ao bucket do S3, garantindo que as políticas forneçam apenas o acesso pretendido aos seus recursos do S3.

### Processamento de dados

Para transformar dados e acionar fluxos de trabalho para automatizar uma variedade de outras atividades de processamento em escala, você pode usar os seguintes recursos.

- [S3 Object Lambda](https://docs.aws.amazon.com/AmazonS3/latest/userguide/transforming-objects.html): adiciona seu próprio código às solicitações GET do S3 para modificar e processar dados, conforme eles são retornados para uma aplicação. Filtra linhas, redimensiona imagens dinamicamente, edita dados confidenciais e muito mais.
- [Notificações de eventos](https://docs.aws.amazon.com/AmazonS3/latest/userguide/NotificationHowTo.html): aciona fluxos de trabalho que usam o Amazon Simple Notification Service (Amazon SNS), o Amazon Simple Queue Service (Amazon SQS) e o AWS Lambda quando uma alteração for feita em seus recursos do S3.

### Registro e monitoramento do armazenamento

O Amazon S3 fornece ferramentas de registro e monitoramento que você pode usar para monitorar e controlar como seus recursos do Amazon S3 estão sendo usados. Para obter mais informações, consulte [Ferramentas de monitoramento](https://docs.aws.amazon.com/AmazonS3/latest/userguide/monitoring-automated-manual.html).

**Ferramentas de monitoramento automatizadas**

- [Métricas do Amazon CloudWatch para o Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/cloudwatch-monitoring.html): acompanha a integridade operacional de seus recursos do S3 e configura alertas de faturamento quando as cobranças estimadas atingirem um limite definido pelo usuário.
- [AWS CloudTrail](https://docs.aws.amazon.com/AmazonS3/latest/userguide/cloudtrail-logging.html): registra ações executadas por um usuário, uma função ou um Serviço da AWS no Amazon S3. Os logs do CloudTrail fornecem rastreamento detalhado de API para operações no nível de bucket e objeto do S3.

**Ferramentas de monitoramento manual**

- [Log de acesso ao servidor](https://docs.aws.amazon.com/AmazonS3/latest/userguide/ServerLogs.html): fornece detalhes sobre as solicitações que são feitas a um bucket. Você pode usar logs de acesso ao servidor para muitos casos de uso, como conduzir auditorias de segurança e acesso, saber mais sobre sua base de clientes e entender sua fatura do Amazon S3.
- [AWSTrusted Advisor](https://docs.aws.amazon.com/awssupport/latest/user/trusted-advisor.html): avalia sua conta usando verificações de práticas recomendadas da AWS para identificar maneiras de otimizar sua infraestrutura da AWS, melhorar a segurança e o desempenho, reduzir custos e monitorar cotas de serviço. Em seguida, você pode seguir as recomendações para otimizar seus serviços e recursos.

### Análise e insights

O Amazon S3 oferece recursos para ajudá-lo a obter visibilidade do uso do armazenamento, o que permite que você entenda melhor, analise e otimize seu armazenamento em escala.

- [Amazon S3 Storage Lens](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage_lens.html): entende, analisa e otimiza seu armazenamento. O S3 Storage Lens fornece mais de 29 métricas de uso e atividade e painéis interativos para agregar dados de toda a sua organização, contas específicas, Regiões da AWS , buckets ou prefixos.
- [Análise de classe de armazenamento](https://docs.aws.amazon.com/AmazonS3/latest/userguide/analytics-storage-class.html): analisa padrões de acesso ao armazenamento para decidir quando é hora de mover seus dados para uma classe de armazenamento mais econômica.
- [Inventário do S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-inventory.html): audita e relata sobre objetos e seus metadados correspondentes e configura outros recursos do Amazon S3 para executar ações nos relatórios de inventário. Por exemplo, você pode gerar relatórios sobre o status da replicação e da criptografia de seus objetos. Para obter uma lista de todos os metadados disponíveis para cada objeto nos relatórios de inventário, consulte [Lista de inventário do Amazon S3](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/storage-inventory.html#storage-inventory-contents).

### Consistência forte

O Amazon S3 oferece uma forte consistência de leitura após gravação para solicitações de PUT e DELETE de objetos no bucket do Amazon S3 em todas as Regiões da AWS . Isso se aplica a ambas as gravações em novos objetos, bem como solicitações PUT que sobrescrevem objetos existentes e solicitações DELETE. Além disso, as operações de leitura no Amazon S3 Select, listas de controle de acesso (ACLs) do Amazon S3, etiquetas de objeto do Amazon S3 e metadados de objeto (por exemplo, objeto HEAD) são fortemente consistentes. Para obter mais informações, consulte [Modelo de consistência de dados do Amazon S3](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#ConsistencyModel).

## Como funciona o Amazon S3

O Amazon S3 é um serviço de armazenamento de objetos que armazena dados como objetos em buckets. Um *objeto* é um arquivo e quaisquer metadados que descrevam o arquivo. Um *bucket* é um contêiner de objetos.

Para armazenar seus dados no Amazon S3, crie um bucket e especifique um nome de bucket e a Região da AWS . Em seguida, carregue seus dados para esse bucket como objetos no Amazon S3. Cada objeto tem uma *chave* (ou *nome de chave*), que é um identificador exclusivo do objeto no bucket.

O S3 fornece recursos que você pode configurar para oferecer suporte ao seu caso de uso específico. Você pode usar o versionamento do S3 para manter várias versões de um objeto no mesmo bucket que permite que você restaure objetos excluídos ou substituídos acidentalmente.

Os buckets e os objetos neles são privados e poderão ser acessados somente se você conceder explicitamente permissões de acesso. Você pode usar políticas de bucket, políticas do AWS Identity and Access Management (IAM), listas de controle de acesso (ACLs) e pontos de acesso do S3 para gerenciar o acesso.

**Tópicos**

- [Buckets](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#BasicsBucket)
- [Objects](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#BasicsObjects)
- [Keys](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#BasicsKeys)
- [Versionamento do S3](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#Versions)
- [ID da versão](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#BasicsVersionID)
- [Política de bucket](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#BucketPolicies)
- [Listas de controle de acesso (ACLs)](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#S3_ACLs)
- [Pontos de acesso do S3](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#BasicsAccessPoints)
- [Regions](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#Regions)

### Buckets

Um bucket é um contêiner para objetos armazenados no Amazon S3. Você pode armazenar qualquer número de objetos em um bucket e pode ter até 100 buckets na sua conta. Para solicitar um aumento, visite o [Service Quotas Console](https://console.aws.amazon.com/servicequotas/home/services/s3/quotas/) (Console de cotas de serviço).

Cada objeto está contido em um bucket. Por exemplo, se o objeto chamado `photos/puppy.jpg` estiver armazenado no bucket `DOC-EXAMPLE-BUCKET` da região oeste dos EUA (Oregon), ele poderá ser endereçado usando o URL `https://DOC-EXAMPLE-BUCKET.s3.us-west-2.amazonaws.com/photos/puppy.jpg`. Para obter mais informações, consulte [Accessing a Bucket](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/access-bucket-intro.html) (Como acessar um bucket).

Ao criar um bucket, você insere um nome de bucket e escolhe a Região da AWS onde o bucket residirá. Assim que você cria um bucket, não pode mais alterar o nome do bucket ou sua região. Os nomes de bucket devem seguir as [regras de nomeação de bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucketnamingrules.html). Você também pode configurar um bucket para usar o [Versionamento do S3](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Versioning.html) ou outros recursos do [gerenciamento de armazenamento](https://docs.aws.amazon.com/AmazonS3/latest/userguide/managing-storage.html).

Os buckets também:

- Organizam o namespace do Amazon S3 no nível mais elevado.
- Identificam a conta responsável por cobranças de transferência de dados e armazenamento.
- Fornecem opções de controle de acesso, como políticas de bucket, listas de controle de acesso (ACLs) e pontos de acesso do S3, que podem ser usados para gerenciar o acesso aos recursos do Amazon S3.
- Serve como a unidade de agregação para relatório de uso.

Para obter mais informações sobre buckets, consulte [Visão geral dos buckets](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/UsingBucket.html).

### Objects

Os objetos são as entidades fundamentais armazenadas no Amazon S3. Os objetos consistem em metadados e dados de objeto. Os metadados são um conjunto de pares de nome e valor que descrevem o objeto. Esses pares incluem alguns metadados padrão, como a data da última modificação, e metadados HTTP padrão, como o `Content-Type`. Você também pode especificar metadados personalizados no momento em que o objeto é armazenado.

Um objeto é identificado exclusivamente em um bucket por uma [chave (nome)](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#BasicsKeys) e um [ID da versão](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html#BasicsVersionID) (se o Versionamento do S3 estiver habilitado no bucket). Para obter mais informações sobre objetos, consulte [Visão geral de objetos Amazon S3](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/UsingObjects.html).

### Keys

Uma *chave de objeto* (ou *nome da chave*) é um identificador exclusivo de um objeto em um bucket. Cada objeto em um bucket tem exatamente uma chave. A combinação de um bucket, chave de objeto e, opcionalmente, o ID de versão (se o Versionamento do S3 estiver habilitado para o bucket) identifica exclusivamente cada objeto. Portanto, é possível pensar no Amazon S3 como um mapa de dados básico entre "bucket + chave + versão" e o objeto em si.

Cada objeto no Amazon S3 pode ser endereçado exclusivamente por meio da combinação do endpoint de serviço da web, do nome de bucket, da chave e, opcionalmente, de uma versão. Por exemplo, no URL `https://DOC-EXAMPLE-BUCKET.s3.us-west-2.amazonaws.com/photos/puppy.jpg`, `DOC-EXAMPLE-BUCKET` é o nome do bucket e `/photos/puppy.jpg` é a chave.

Para obter mais informações sobre chaves de objeto, consulte [Criar nomes de chave de objeto](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/object-keys.html).

### Versionamento do S3

Use o versionamento do S3 para manter diversas variantes de um objeto no mesmo bucket. Com o versionamento do S3, você pode preservar, recuperar e restaurar todas as versões de cada objeto armazenado em seus buckets. Você pode se recuperar facilmente de ações não intencionais do usuário e de falhas da aplicação.

Para obter mais informações, consulte [Usando o versionamento em buckets do S3](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Versioning.html).

### ID da versão

Se você habilitar o versionamento do S3 em um bucket, o Amazon S3 gerará um ID de versão exclusivo para cada objeto adicionado ao bucket. Os objetos que já existiam no bucket no momento em que você habilita o controle de versão têm um ID de versão `null`. Se você modificar esses (ou quaisquer outros) objetos com outras operações, como [CopyObject](https://docs.aws.amazon.com/AmazonS3/latest/API/API_CopyObject.html) e [PutObject](https://docs.aws.amazon.com/AmazonS3/latest/API/API_PutObject.html), os novos objetos obtêm um ID de versão exclusivo.

Para obter mais informações, consulte [Usando o versionamento em buckets do S3](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Versioning.html).

### Política de bucket

Uma política de bucket é baseada em recursos do AWS Identity and Access Management (IAM) que você pode usar para conceder permissões de acesso ao bucket e aos objetos nele contidos. Só o proprietário do bucket pode associar uma política a um bucket. As permissões anexadas ao bucket se aplicam a todos os objetos do bucket que pertencem ao proprietário do bucket. As políticas de bucket são limitadas a 20 KB.

As políticas de bucket usam uma linguagem de políticas de acesso baseada em JSON que é padrão na AWS. Você pode usar políticas de bucket para adicionar ou negar permissões para os objetos em um bucket. As políticas de bucket permitem ou negam solicitações com base nos elementos da política, incluindo o solicitante, ações do S3, recursos e aspectos ou condições da solicitação (por exemplo, o endereço IP usado para fazer a solicitação). Por exemplo, você pode criar uma política de bucket que conceda permissões entre contas para carregar objetos em um bucket do S3 enquanto garante que o proprietário do bucket tenha controle total dos objetos carregados. Para obter mais informações, consulte [Exemplos de políticas de bucket](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/example-bucket-policies.html).

Na política de bucket, você pode usar caracteres curinga nos nomes de recursos da Amazon (ARNs) e outros valores para conceder permissões a um subconjunto de objetos. Por exemplo, você pode controlar o acesso a grupos de objetos que começam com um [prefixo](https://docs.aws.amazon.com/general/latest/gr/glos-chap.html#keyprefix) ou termine com uma determinada extensão, como `.html`.

### Listas de controle de acesso (ACLs)

Como regra geral, recomendamos o uso de políticas baseadas em recursos do S3 (políticas de bucket e políticas de ponto de acesso) ou políticas do IAM para controle de acesso, em vez de ACLs. ACLs são mecanismos de controle de acesso que antecedem políticas baseadas em recursos e IAM. Para obter mais informações sobre quando você usaria ACLs, em vez de políticas baseadas em recursos ou políticas do IAM, consulte [Diretrizes para políticas de acesso](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/access-policy-alternatives-guidelines.html).

Você pode usar as ACLs para conceder permissões de leitura e gravação para buckets individuais e objetos a usuários autorizados. Cada bucket e objeto tem uma ACL anexada como um sub-recurso. Uma ACL define a quais grupos ou Contas da AWS é concedido acesso, bem como o tipo de acesso. Para obter mais informações, consulte [Visão geral da lista de controle de acesso (ACL)](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/acl-overview.html).

### Pontos de acesso do S3

Os pontos de acesso do Amazon S3 são nomeados endpoints de rede com políticas de acesso dedicadas que descrevem como os dados podem ser acessados usando esse endpoint. Os pontos de acesso simplificam o gerenciamento do acesso a dados em escala para conjuntos de dados compartilhados no Amazon S3. Os pontos de acesso são nomeados endpoints de rede anexados a buckets que você pode usar para executar operações de objeto do S3, como `GetObject` e `PutObject`.

Cada ponto de acesso tem sua própria política do IAM. Você também pode configurar definições de [Bloqueio de acesso público](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/access-control-block-public-access.html) para cada ponto de acesso. Você pode configurar qualquer ponto de acesso para aceitar solicitações somente de uma nuvem virtual privada (VPC) para restringir o acesso a dados do Amazon S3 a uma rede privada.

Para obter mais informações, consulte [Gerenciamento de acesso a dados com pontos de acesso do Amazon S3](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/access-points.html).

### Regions

Você pode escolher a região da Região da AWS geográfica onde o Amazon S3 armazena os buckets criados. É possível escolher uma região para otimizar a latência, minimizar os custos ou atender a requisitos regulatórios. Os objetos armazenados em uma Região da AWS nunca saem dela, a não ser que você os transfira ou os replique explicitamente para outra região. Por exemplo, os objetos armazenados na região da UE (Irlanda) nunca saem dela.

**nota**

Só é possível acessar o Amazon S3 e seus recursos em Regiões da AWS que estão habilitadas para sua conta. Para obter mais informações sobre como habilitar uma região para criar e gerenciar recursos da AWS, consulte [Como gerenciar Regiões da AWS ](https://docs.aws.amazon.com/general/latest/gr/rande-manage.html)na *Referência geral da AWS*.

Para obter uma lista de regiões e endpoints do Amazon S3, consulte [Regiões e endpoints](https://docs.aws.amazon.com/general/latest/gr/s3.html) na *Referência geral da AWS*.

## Modelo de consistência de dados do Amazon S3

O Amazon S3 oferece uma forte consistência de leitura após gravação para solicitações de PUT e DELETE de objetos no bucket do Amazon S3 em todas as Regiões da AWS . Isso se aplica a ambas as gravações em novos objetos, bem como solicitações PUT que sobrescrevem objetos existentes e solicitações DELETE. Além disso, as operações de leitura no Amazon S3 Select, listas de controle de acesso (ACLs) do Amazon S3, etiquetas de objeto do Amazon S3 e metadados de objeto (por exemplo, objeto HEAD) são muito consistentes.

As atualizações em uma única chave são atômicas. Por exemplo, se você executar uma solicitação PUT em uma chave existente de um thread e executar uma solicitação GET na mesma chave de um segundo thread simultaneamente, você obterá os dados antigos ou os novos dados, mas nunca dados parciais ou corrompidos.

O Amazon S3 atinge alta disponibilidade replicando dados entre vários servidores nos datacenters da AWS. Se uma solicitação PUT for bem-sucedida, os dados serão armazenados com segurança. Qualquer leitura (solicitação de GET ou LIST) iniciada após o recebimento de uma resposta PUT bem-sucedida retornará os dados escritos pelo PUT. Veja alguns exemplos desse comportamento:

- Um processo grava um novo objeto no Amazon S3 e imediatamente lista as chaves em seu bucket. O novo objeto aparecerá na lista.
- Um processo substitui um objeto existente e imediatamente tenta lê-lo. O Amazon S3 retorna os novos dados.
- Um processo exclui um objeto existente e imediatamente tenta lê-lo. O Amazon S3 não retorna dados porque o objeto foi excluído.
- Um processo exclui um objeto existente e imediatamente lista as chaves em seu bucket. O objeto não aparecerá na listagem.

**nota**

- O Amazon S3 não oferece suporte ao bloqueio de objetos para escritores simultâneos. Se duas solicitações PUT forem realizadas simultaneamente na mesma chave, a solicitação com o time stamp mais recente será a escolhida. Se isso for um problema, você precisará criar um mecanismo de bloqueio de objetos em sua aplicação.
- As atualizações são baseadas em chave. Não há possibilidade de realizar atualizações atômicas entre chaves. Por exemplo, você não pode tornar a atualização de uma chave dependente da atualização de outra chave a menos que você desenvolva essa funcionalidade em seu aplicativo.

As configurações de bucket têm um modelo de consistência eventual. Especificamente, isso significa que:

- Por exemplo, se você excluir um bucket e listar imediatamente todos os buckets, o bucket excluído ainda poderá ser exibido na lista.
- Se você ativar o versionamento em um bucket pela primeira vez, pode levar um curto período de tempo para que a alteração seja totalmente propagada. Recomendamos que você aguarde 15 minutos após ativar o versionamento antes de emitir operações de gravação (solicitações PUT ou DELETE) em objetos no bucket.

### Aplicações simultâneas

Esta seção fornece exemplos de comportamento a serem esperados do Amazon S3 quando vários clientes estão gravando nos mesmos itens.

Neste exemplo, W1 (gravação 1) e W2 (gravação 2) são concluídas antes do início de R1 (leitura 1) e R2 (leitura 2). Como o S3 é fortemente consistente, R1 e R2 retornam `color = ruby`.

![img](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/images/consistency1.png)

No próximo exemplo, a W2 não é encerrada antes do início da R1. Portanto, R1 pode retornar `color = ruby` ou `color = garnet`. No entanto, como W1 e W2 terminam antes do início do R2, o R2 retorna `color = garnet`.

![img](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/images/consistency2.png)

No último exemplo, o W2 começa antes que o W1 tenha recebido um reconhecimento. Portanto, essas gravações são consideradas simultâneas. O Amazon S3 usa internamente a semântica do último escritor para determinar qual gravação tem precedência. No entanto, a ordem em que o Amazon S3 recebe as solicitações e a ordem em que as aplicações recebem confirmações não podem ser previstas devido a fatores como latência de rede. Por exemplo, o W2 pode ser iniciado por uma instância do Amazon EC2 na mesma região, enquanto o W1 pode ser iniciado por um host que está mais longe. A melhor maneira de determinar o valor final é realizar uma leitura após ambas as gravações terem sido confirmadas.

![img](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/images/consistency3.png)

## Serviços relacionados

Depois de carregar os dados no Amazon S3, você poderá usá-los com outros serviços da AWS. Os serviços a seguir podem ser usados com mais frequência:

- O **[Amazon Elastic Compute Cloud (Amazon EC2)](http://aws.amazon.com/ec2/)** oferece uma capacidade de computação escalável na Nuvem AWS . O uso do Amazon EC2 elimina a necessidade de investir em hardware inicialmente, portanto, você pode desenvolver e implantar aplicativos com mais rapidez. É possível usar o Amazon EC2 para executar quantos servidores virtuais forem necessários, configurar a segurança e as redes e gerenciar o armazenamento.
- **[Amazon EMR](http://aws.amazon.com/elasticmapreduce/)**: ajuda empresas, pesquisadores, analistas de dados e desenvolvedores a processar de maneira fácil e econômica grandes quantidades de dados. O Amazon EMR usa um framework do Hadoop hospedado que é executado na infraestrutura de escala da Web do Amazon EC2 e do Amazon S3.
- **[Família do AWS Snow](http://aws.amazon.com/snow/)**: ajuda os clientes que precisam executar operações em ambientes austeros e não datacenter e em locais onde há falta de conectividade de rede consistente. Você pode usar dispositivos da família do AWS Snow para acesso ao armazenamento localmente e de potência computacional da Nuvem AWS em lugares onde talvez não haja conexão à Internet.
- **[AWS Transfer Family](http://aws.amazon.com/aws-transfer-family/)**: fornece suporte totalmente gerenciado para transferências de arquivos diretamente para dentro e fora do Amazon S3 ou Amazon Elastic File System (Amazon EFS) usando Secure Shell (SSH), File Transfer Protocol (SFTP), File Transfer Protocol over SSL (FTPS) e File Transfer Protocol (FTP).

## Acesso ao Amazon S3

Você pode trabalhar com o Amazon S3 de qualquer uma das seguintes formas:

### AWS Management Console

O console é uma interface de usuário baseada na Web para gerenciar o Amazon S3 e o recursos da AWS. Se você se inscreveu em uma Conta da AWS , pode acessar o console do Amazon S3 fazendo login no AWS Management Console e escolhendo **S3** na página inicial do AWS Management Console.

### AWS Command Line Interface

Você pode usar as ferramentas de linha de comando da AWS para emitir comandos ou criar scripts na linha de comando de seu sistema e executar tarefas da AWS (incluindo o S3).

A [AWS Command Line Interface (AWS CLI)](http://aws.amazon.com/cli/) fornece comandos para um amplo conjunto de Serviços da AWS. A AWS CLI é compatível com Windows, macOS e Linux. Para começar a usar, consulte o [*Manual do usuário do AWS Command Line Interface*](https://docs.aws.amazon.com/cli/latest/userguide/). Para obter mais informações sobre os comandos do Amazon S3, consulte [s3api](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3api/index.html) e [s3control](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3control/index.html) na *Referência de comandos da AWS CLI*.

### AWSSDKs da

A AWS fornece SDKs (kits de desenvolvimento de software) que consistem em bibliotecas e códigos de exemplo para várias linguagens de programação e plataformas (Java, Python, Ruby, .NET, iOS, Android etc.). Os SDKs da AWS constituem uma forma conveniente de criar acesso programático para o S3 e a AWS. O Amazon S3 é um serviço REST. Você pode enviar solicitações para o Amazon S3 usando a API REST ou as bibliotecas SDK da AWS que envolvem a API REST do Amazon S3, simplificando as tarefas de programação. Por exemplo, os SDKs processam tarefas como calcular assinaturas, assinar solicitações de forma criptográfica, gerenciar erros e novas tentativas automáticas de solicitações. Para obter informações sobre os SDKs da AWS, incluindo como baixar e instalá-los, consulte [Ferramentas da AWS](http://aws.amazon.com/tools/).

Cada interação com o Amazon S3 é autenticada ou anônima. Se você estiver usando os SDKs da AWS, as bibliotecas calcularão a assinatura das chaves fornecidas. Para obter mais informações sobre como fazer solicitações ao Amazon S3, consulte [Fazer solicitações](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/MakingRequests.html).

### API REST do Amazon S3

A arquitetura do Amazon S3 foi desenvolvida para ser neutra em termos de linguagem de programação, usando nossas interfaces compatíveis com a AWS para armazenar e recuperar objetos. Você pode acessar o S3 e a AWS de forma programada usando a API REST do Amazon S3. A API REST é uma interface HTTP para o Amazon S3. Usando a API REST, você usa solicitações HTTP padrão para criar, buscar e excluir buckets e objetos.

Você pode usar qualquer toolkit compatível com HTTP para usar a API REST. Você pode até usar um navegador para buscar objetos, desde que eles possam ser lidos anonimamente.

A API REST usa os cabeçalhos padrão e os códigos de status HTTP para que os navegadores e os toolkits padrão funcionem como esperado. Em algumas áreas, adicionamos funcionalidade ao HTTP (por exemplo, adicionamos cabeçalhos para oferecer suporte ao controle de acesso). Nesses casos, fizemos o melhor para adicionar nova funcionalidade de uma forma que correspondesse ao estilo de uso padrão do HTTP.

Se fizer chamadas diretas da API REST na aplicação, você deverá escrever o código para calcular a assinatura e adicioná-la à solicitação. Para obter mais informações sobre como fazer solicitações ao Amazon S3, consulte [Fazer solicitações](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/MakingRequests.html).

**nota**

O suporte da API de SOAP via HTTP está defasado, mas continua disponível via HTTPS. Os novos recursos do Amazon S3 não são compatíveis com o SOAP. Recomendamos usar a API REST ou os AWS SDKs.

## Pagar pelo Amazon S3

A definição de preço para o Amazon S3 foi desenvolvida para que você não precise planejar para os requisitos de armazenamento da aplicação. A maioria dos provedores de armazenamento exige que você adquira uma quantidade predeterminada de armazenamento e capacidade de transferência de rede. Nesse cenário, se você exceder essa capacidade, o serviço é desativado ou você é cobrado por altas taxas excedentes. Se você não exceder essa capacidade, você paga como se tivesse usado tudo.

O Amazon S3 cobra apenas pelo que você realmente usa, sem taxas ocultas e nenhuma taxa excedente. Este modelo fornece a você um serviço com custo variável que pode aumentar com seus negócios enquanto proporciona a você as vantagens de custos de infraestrutura da AWS. Para obter mais informações, consulte [Definição de preço do Amazon S3](http://aws.amazon.com/s3/pricing/).

Ao cadastrar-se na AWS, sua Conta da AWS é automaticamente cadastrada em todos os serviços da AWS incluindo o Amazon S3. Entretanto, você será cobrado apenas pelos serviços que usar. Se você for um novo cliente do Amazon S3, você pode começar a usar o Amazon S3 gratuitamente. Para obter mais informações, consulte [nível gratuito da AWS](http://aws.amazon.com/free).

Para ver sua fatura, acesse o Painel de Billing and Cost Management no [console da AWS Billing and Cost Management](https://console.aws.amazon.com/billing/). Para saber mais sobre o faturamento da Conta da AWS , consulte o [*Manual do usuário doAWS Billing and Cost Management*](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-what-is.html). Se tiver dúvidas sobre o faturamento da AWS e as Contas da AWS , entre em contato com o [AWS Support](http://aws.amazon.com/contact-us/).

## Conformidade do PCI DSS

O Amazon S3 é compatível com o processamento, o armazenamento e a transmissão de dados de cartão de crédito por um comerciante ou um provedor de serviços e foi validada como em conformidade com o Data Security Standard (DSS, Padrão de segurança de dados) da Payment Card Industry (PCI, Padrão de cartão de crédito). Para obter mais informações sobre o PCI DSS, incluindo como solicitar uma cópia do pacote de conformidade com o PCI da AWS, consulte [Nível 1 do PCI DSS](http://aws.amazon.com/compliance/pci-dss-level-1-faqs/).





**Esta página foi útil?**

Sim

Não

[Fornecer feedback](https://docs.aws.amazon.com/forms/aws-doc-feedback?hidden_service_name=S3&topic_url=http://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/Welcome.html)

**Próximo tópico:** [Conceitos básicos](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/userguide/GetStartedWithS3.html)