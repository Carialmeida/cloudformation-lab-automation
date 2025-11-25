🌩️ Laboratório — Automação com AWS CloudFormation

Este laboratório demonstra como implantar infraestrutura na AWS de forma consistente, automatizada e reproduzível usando CloudFormation, o serviço de IaC (Infraestrutura como Código) da AWS.

O objetivo é:

Criar uma stack com uma VPC e Security Group

Atualizar essa stack adicionando um bucket S3

Atualizar novamente adicionando uma instância EC2

Encerrar a stack e destruir toda a infraestrutura automaticamente

🧭 Visão Geral da Arquitetura

A arquitetura final do laboratório é composta pelos seguintes componentes:

Uma VPC (10.0.0.0/16)

Subnet pública (10.0.0.0/24)

Internet Gateway + Route Table pública

Security Group para App

Bucket Amazon S3

Instância EC2 Amazon Linux 2 (t3.micro)

Na subnet pública

Com IP público

Com SG liberando porta 80

📘 Diagrama da Arquitetura
⏱️ Duração

Aproximadamente 45 minutos.

🟦 Pré-requisitos

Nenhum conhecimento prévio avançado é necessário.
O ambiente AWS é fornecido pelo laboratório.

🚀 Acessando o Console da AWS

Clique em Iniciar Laboratório

Aguarde o status Lab status: ready

Clique no botão AWS para abrir o console

O login é feito automaticamente

Não altere a região durante todo o laboratório

🧩 Tarefa 1 — Implantar a Primeira Stack (VPC + Security Group)

Nesta tarefa, você fará o deploy inicial de uma stack que cria:

Uma VPC

Uma Subnet pública

Um Security Group

⚙️ Passos:

No console da AWS, vá para CloudFormation

Clique em Criar stack

Escolha Carregar um arquivo de modelo

Faça upload do arquivo task1.yaml fornecido pelo lab

Nome da stack: Lab

Deixe os parâmetros padrão (CIDRs)

Avance até a tela de revisão

Marque a caixa de confirmação para recursos com nomes personalizados

Clique em Criar stack

Acompanhe:

Aba Events → criação dos recursos

Aba Resources → ordem planejada pelo CloudFormation

📌 Resultado da Tarefa 1:

VPC criada

Subnet pública criada

Security group criado

Internet Gateway + Route Table (com rota para 0.0.0.0/0)

🧩 Tarefa 2 — Adicionar um Bucket S3 à Stack Existente

Agora você irá modificar o modelo existente e adicionar um novo recurso:

Bucket AWS S3

🛠️ O que foi adicionado ao template:
  LabBucket:
    Type: AWS::S3::Bucket


Nenhuma propriedade adicional é necessária.

⚙️ Passos:

Edite seu task1.yaml e adicione o bucket na seção Resources

No CloudFormation, clique em Update stack

Escolha Replace current template

Faça upload do template atualizado

Avance até o final e clique em Update stack

A pré-visualização (“Changeset”) deve mostrar:

Action: Add  
Resource type: AWS::S3::Bucket  
Logical ID: LabBucket  

📌 Resultado da Tarefa 2:

Novo bucket S3 criado

Nenhuma modificação nos demais recursos

🧩 Tarefa 3 — Adicionar uma Instância EC2 à Stack

Agora você irá adicionar uma instância EC2 usando:

AMI mais recente do Amazon Linux 2

Security Group do App

Subnet pública existente

🛠️ 1. Adicionar o parâmetro da AMI (em Parameters):
  AmazonLinuxAMIID:
    Type: AWS::SSM::Parameter::Value<AWS::EC2::Image::Id>
    Default: /aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2

🛠️ 2. Adicionar a instância EC2 em Resources:
  AppServer:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: !Ref AmazonLinuxAMIID
      InstanceType: t3.micro
      SecurityGroupIds:
        - !Ref AppSecurityGroup
      SubnetId: !Ref PublicSubnet
      Tags:
        - Key: Name
          Value: App Server

⚙️ Passos:

Atualize o arquivo YAML com as novas seções

Vá em Update stack → Replace current template

Faça upload do template atualizado

Avance até a revision e clique em Update stack

A prévia deverá mostrar:

Add — AWS::EC2::Instance — AppServer

📌 Resultado da Tarefa 3:

Instância EC2 criada e visível no console

🧩 Tarefa 4 — Excluir a Stack

Para concluir o laboratório:

Selecione a stack Lab

Clique em Delete

Confirme

Acompanhe o status: DELETE_IN_PROGRESS → desaparece da lista

📌 Resultado da Tarefa 4:

Todos os recursos criados foram removidos:

VPC

Subnet

Internet Gateway

Route Table

Security Groups

Bucket S3

Instância EC2

🏁 Laboratório concluído!

Após deletar a stack:

Clique em Finalizar Laboratório

Confirme em Sim

Aguarde a mensagem “A exclusão foi iniciada...”

Feche o painel

🎉 Parabéns!

Você concluiu o laboratório de Automação com AWS CloudFormation e agora entende como:

Criar recursos via IaC

Modificar stacks incrementalmente

Adicionar EC2, S3 e componentes de rede

E destruir tudo de forma segura e automatizada

Se quiser, posso gerar:

📌 Um README com imagens embedadas
📌 Um PDF
📌 Uma versão profissional para GitHub com sumário automático
📌 Ou transformar isso num notebook para estudo

O que prefere?

Você disse:
QUERO EM formato Markdown para GitHub
O ChatGPT disse:

Perfeito, Isa! Aqui está o README em Markdown, totalmente formatado e pronto para colar no GitHub — com seções, headings, listas, blocos de código, imagens (usando placeholders), sumário e estrutura profissional.

🌩️ Laboratório — Automação com AWS CloudFormation

Este laboratório demonstra como implantar recursos de infraestrutura na AWS de maneira consistente, automatizada e repetível usando AWS CloudFormation.

O objetivo é:

Criar uma stack com uma VPC e Security Group

Atualizar a stack e adicionar um bucket S3

Atualizar novamente e adicionar uma instância EC2

Encerrar a stack e apagar todos os recursos

📚 Sumário

Visão Geral da Arquitetura

Duração

Pré-requisitos

Acessando o Console da AWS

Tarefa 1 — Implantar a Stack Inicial

Tarefa 2 — Adicionar um Bucket S3

Tarefa 3 — Adicionar uma Instância EC2

Tarefa 4 — Excluir a Stack

Conclusão

🧭 Visão Geral da Arquitetura

A arquitetura final deste laboratório inclui:

VPC (10.0.0.0/16)

Subnet pública (10.0.0.0/24)

Internet Gateway

Route Table pública com rota para 0.0.0.0/0

Security Group do App (libera porta 80)

Bucket Amazon S3

Instância EC2 Amazon Linux 2 (t3.micro)

📘 Diagrama (placeholder)
[DIAGRAMA AQUI]

⏱️ Duração

Aproximadamente 45 minutos.

🟦 Pré-requisitos

Nenhum conhecimento avançado é necessário.
O ambiente AWS é temporário e fornecido pelo laboratório.

🚀 Acessando o Console da AWS

Clique em Iniciar Laboratório

Aguarde o status Lab status: ready

Clique no botão AWS para abrir o console

O login será automático

Não altere a região durante o laboratório

🧩 Tarefa 1 — Implantar a Stack Inicial

Nesta primeira parte, você irá criar:

Uma VPC

Uma Subnet pública

Um Security Group

📄 Passos

Abra o console → CloudFormation

Clique em Criar pilha

Escolha Carregar um arquivo de modelo

Envie o arquivo task1.yaml inicial

Nome da stack: Lab

Use os valores padrão

Avance até a tela de revisão

Marque a confirmação de recursos com nomes personalizados

Clique Criar pilha

🔍 Acompanhe

Events → atividades de criação

Resources → ordem dos recursos

Quando chegar em CREATE_COMPLETE, a stack está pronta.

🧩 Tarefa 2 — Adicionar um Bucket S3

Agora você irá atualizar o modelo para adicionar:

Um bucket S3 simples (apenas 2 linhas de YAML)

🛠️ Código adicionado no template
  LabBucket:
    Type: AWS::S3::Bucket

📄 Passos

Edite o task1.yaml adicionando o bloco acima em Resources

Vá em Update stack

Escolha Replace current template

Faça upload do arquivo atualizado

Clique em Next → Next

Veja o “Changeset” exibindo:

Action: Add  
Resource type: AWS::S3::Bucket  


Clique em Update stack

✔️ Resultado

Bucket S3 criado

Nenhum recurso existente é modificado

🧩 Tarefa 3 — Adicionar uma Instância EC2

Agora você irá adicionar uma instância EC2 configurada corretamente.

1️⃣ Adicionar parâmetro da AMI (em Parameters)
  AmazonLinuxAMIID:
    Type: AWS::SSM::Parameter::Value<AWS::EC2::Image::Id>
    Default: /aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2

2️⃣ Adicionar instância EC2 (em Resources)
  AppServer:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: !Ref AmazonLinuxAMIID
      InstanceType: t3.micro
      SecurityGroupIds:
        - !Ref AppSecurityGroup
      SubnetId: !Ref PublicSubnet
      Tags:
        - Key: Name
          Value: App Server

📄 Passos

Atualize o task1.yaml com as seções acima

Vá em Update stack → Replace current template

Envie o arquivo atualizado

Confirme a pré-visualização:

Add — AWS::EC2::Instance — AppServer


Clique em Update stack

✔️ Resultado

Instância EC2 criada

A EC2 estará visível no console com o nome App Server

🧩 Tarefa 4 — Excluir a Stack

Para remover toda a infraestrutura:

Selecione a stack Lab

Clique em Delete

Confirme

Aguarde até desaparecer da lista

✔️ Recursos removidos automaticamente:

VPC

Subnet

IGW

Route Table

Security Groups

EC2

Bucket S3

🏁 Conclusão

Parabéns! 🎉
Você concluiu o laboratório de Automação com CloudFormation, aprendendo a:

Criar infraestrutura como código (IaC)

Modificar stacks incrementalmente

Adicionar EC2, S3 e componentes de rede

Destruir recursos automaticamente

Esse é um dos pilares fundamentais de DevOps/Cloud, e você já deu um passo sólido rumo à automação profissional.# cloudformation-lab-automation
