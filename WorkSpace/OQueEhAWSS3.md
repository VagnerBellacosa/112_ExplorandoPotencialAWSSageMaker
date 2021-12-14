# O que é AWS S3?

Nesse artigo vamos conhecer o AWS S3, um serviço de armazenamento de arquivos na nuvem da Amazon. Vamos conhecer suas vantagens, suas aplicações mais comuns e quando não utilizá-lo.

 cerca de 1 ano atrás

[Artigos](https://www.treinaweb.com.br/blog)O que é AWS S3?

O [AWS](https://www.treinaweb.com.br/blog/introducao-a-amazon-web-services-aws/) S3 (Simple Storage Service) é um serviço de armazenamento de arquivos, também chamados de objetos ou blobs, com foco em escalabilidade, disponibilidade, segurança e performance, tudo isso com um custo extremamente acessível.

O AWS S3 é um serviço distribuído globalmente dentro da sua conta da AWS, com uma organização em buckets regionais. Isso quer dizer que, diferente das EC2, VPC, e RDS, ao acessar o S3 pelo console da AWS, teremos uma visão global do nosso ambiente, ao invés de uma visão de uma única região.

Como comentado anteriormente, o AWS S3 se destaca pelo seu custo extremamente acessível. Você só paga pelo armazenamento e transferência de saída dos seus arquivos, com um custo aproximado de cinco centavos para cada gigabyte armazenado, o que é muito mais barato se comparado com o custo de disco EBS de uma [EC2](https://www.treinaweb.com.br/blog/criando-instancias-no-amazon-ec2/) tradicional.



![Amazon Web Services (AWS) - Fundamentos](https://d2knvm16wkt3ia.cloudfront.net/assets/svg-icon/aws.svg)

##### CursoAmazon Web Services (AWS) - Fundamentos

[Conhecer o curso](https://www.treinaweb.com.br/curso/amazon-web-services-aws-fundamentos)

## Quando usar o S3?

O S3 é um serviço de armazenamento bastante flexível, que suporta diversos casos de uso, como por exemplo:

- *Armazenamento de arquivos para aplicações web*: como arquivos CSS e JavaScript do frontend da sua aplicação, e imagens enviadas pelos seus usuários via upload.
- *Arquivos de backups e logs*: você pode armazenar arquivos privados, como logs de alguma aplicação, ou até mesmo backups de longo prazo do seu banco de dados, usados para fins legais.
- *Archive para um grande volume de dados*: é possível armazenar muita coisa no S3. É possível armazenar objetos com até 5 terabytes e um bucket suporta um número ilimitado de objetos. Para grandes volumes de dados você pode utilizar o S3 Glacier e economizar ainda mais o custo de armazenamento.
- *Replicação de dados entre diferentes regiões*: para aplicações distribuídas globalmente, você pode replicar buckets inteiros em diferentes regiões da AWS com um Batch Operation.
- *Hospedagem de sites estáticos*: se você tem uma aplicação web que consiste só em arquivos estáticos, ou uma [Single Page Applications (SPA)](https://www.treinaweb.com.br/blog/o-que-sao-aplicacoes-spa/), você pode utilizar somente o S3 para hospedar essa aplicação em completo.



![Amazon Web Services (AWS) - Ferramentas de Rede e Distribuição de Conteúdo – Fundamentos]()

##### CursoAmazon Web Services (AWS) - Ferramentas de Rede e Distribuição de Conteúdo – Fundamentos

[Conhecer o curso](https://www.treinaweb.com.br/curso/aws-ferramentas-de-rede-e-distribuicao-de-conteudo-fundamentos)

## O que o S3 não faz

Embora seja um serviço flexível, o S3 não é indicado para todos os casos de uso. Existem serviços mais apropriados dentro da própria AWS para alguns cenários.

Com o S3 não temos uma hierarquia de arquivos. Isso é a principal diferença ao comparar o S3 com nosso disco local. Imagine que no S3 todos os arquivos são salvos em um único diretório. Não é possível distinguir se os seus arquivos estavam armazenados numa determinada pasta ou não.

Visualmente você até acha que existe uma organização por pastas, mas na verdade o que você está vendo é um separador lógico no nome do seu arquivo. Se a sua aplicação depende de operações em diretórios, como listar ou mover diretórios inteiros, o S3 pode não ser a melhor alternativa.

Você também não tem suporte direto ao Hadoop ou HDFS. Essas são soluções muito utilizadas em Big Data e você não consegue fazer a ingestão de dados do S3 para um cluster Hadoop com HDFS. Para isso você pode utilizar o [Amazon EMR](https://aws.amazon.com/pt/emr/), um serviço especializado para data lakes com suporte a HDFS e hierarquia de diretórios. Uma curiosidade, o EMR utiliza o S3 por debaixo dos panos, entregando uma camada de compatibilidade com HDFS, mantendo um preço bem acessível.

Com o S3 você também não pode montar um bucket como um disco numa EC2 ou utilizá-lo como um compartilhamento de arquivos de rede. Para usar o S3 você pode utilizar APIs REST, o [AWS CLI](https://www.treinaweb.com.br/blog/como-instalar-e-configurar-o-aws-cli/), ou até mesmo as [SDKs disponíveis para diversas linguagens](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingAWSSDK.html). Para esses casos de uso, prefira outros serviços, como o [EBS](https://aws.amazon.com/pt/ebs/) para montagem de discos, ou o [EFS](https://aws.amazon.com/pt/efs/) para o compartilhamento de arquivos em rede.



![Amazon Web Services (AWS) - EC2 - Fundamentos]()

##### CursoAmazon Web Services (AWS) - EC2 - Fundamentos

[Conhecer o curso](https://www.treinaweb.com.br/curso/amazon-web-services-aws-ec2-elastic-compute-cloud-fundamentos)

## Conclusão

Essa foi uma breve introdução sobre o AWS S3. Vimos aqui algumas vantagens e quando utilizar esse serviço que é um dos principais da AWS.

Confira o curso AWS S3 Fundamentos para conhecer com muito mais detalhes esse serviço.



![Amazon Web Services (AWS) - S3 - Fundamentos]()

##### CursoAmazon Web Services (AWS) - S3 - Fundamentos

[Conhecer o curso](https://www.treinaweb.com.br/curso/amazon-web-services-aws-simple-storage-service-s3-fundamentos)

Fiquem ligados e nos sigam nas nossas redes sociais, como [Twitter](https://twitter.com/treinaweb), [Instagram](https://www.instagram.com/treinaweb/), [Facebook](https://www.facebook.com/TreinaWeb/) e [LinkedIn](https://www.linkedin.com/company/treinaweb/), para receber dicas e saber em primeira mão quando novos cursos forem lançados!

- [#AWS](https://www.treinaweb.com.br/blog/tag/aws)
- [#Amazon](https://www.treinaweb.com.br/blog/tag/amazon)
- [#S3](https://www.treinaweb.com.br/blog/tag/s3)
- [#Storage](https://www.treinaweb.com.br/blog/tag/storage)