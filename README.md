# DesAWSDIO
Repositorio para atividade (Gerado no Claude)

# Laboratório Prático: Gerenciamento de Instâncias Amazon EC2

Análise, práticas e insights adquiridos durante o módulo de computação em nuvem da AWS na plataforma DIO (Digital Innovation One). Este repositório serve como documentação técnica e material de apoio para futuras implementações.

## 📌 Objetivos do Laboratório
* Compreender o ciclo de vida e o funcionamento das instâncias Amazon EC2.
* Praticar a criação, configuração e conexão a servidores virtuais na nuvem.
* Documentar boas práticas de segurança, custos e gerenciamento de infraestrutura AWS.

---

## 🛠️ Conceitos Chave Aprendidos

### 1. O que é o Amazon EC2?
O **Amazon Elastic Compute Cloud (EC2)** é um serviço web que fornece capacidade de computação segura e redimensionável na nuvem. Ele elimina a necessidade de investir em hardware antecipadamente, permitindo lançar servidores virtuais (instâncias) rapidamente.

### 2. Tipos e Famílias de Instâncias
A escolha da instância correta equilibra custo e desempenho:
* **Uso Geral (General Purpose):** Equilíbrio entre computação, memória e rede (ex: `t3.micro`, usada no Free Tier).
* **Otimizadas para Computação (Compute Optimized):** Para processos que exigem muito poder de processamento.
* **Otimizadas para Memória (Memory Optimized):** Ideal para grandes bancos de dados.

### 3. Precificação e Modelos de Compra
* **On-Demand (Sob Demanda):** Paga-se por segundo ou hora de uso, sem compromisso de longo prazo.
* **Instâncias Spot:** Permitem usar a capacidade ociosa da AWS com até 90% de desconto, mas a AWS pode interromper a instância com um aviso prévio de 2 minutos se precisar da capacidade de volta.
* **Instâncias Reservadas / Savings Plans:** Descontos significativos em troca de um compromisso de uso de 1 ou 3 anos.

---

## 🚀 Passo a Passo da Implementação Prática

Abaixo está o fluxo seguido para o lançamento e gerenciamento da instância durante as aulas:

### Passo 1: Escolha da AMI e Tipo de Instância
* **AMI (Amazon Machine Image):** Selecionado o sistema operacional (ex: *Amazon Linux 2023* ou *Ubuntu Server*).
* **Tipo:** Selecionada a instância `t2.micro` / `t3.micro` para elegibilidade na Camada Gratuita (Free Tier).

### Passo 2: Configuração de Segurança (Security Groups)
* O **Security Group** funciona como um firewall virtual para a instância.
* Configuração de regras de entrada (*Inbound Rules*):
  * **Porta 22 (SSH):** Liberada apenas para o meu IP atual para garantir acesso seguro via terminal.
  * **Porta 80 (HTTP) / 443 (HTTPS):** Liberadas para qualquer IP (`0.0.0.0/0`) caso a instância armazene um servidor web.

### Passo 3: Criação do Par de Chaves (Key Pair)
* Download do arquivo `.pem` (ou `.ppk` para Putty) para autenticação criptográfica via SSH.
* *Nota de segurança:* Definição de permissões restritas no arquivo de chave local (`chmod 400 chave.pem` no Linux/Mac).

### Passo 4: Conexão e Armazenamento (EBS)
* Conexão realizada com sucesso à instância via terminal SSH ou *EC2 Instance Connect*.
* Entendimento do **Amazon EBS (Elastic Block Store)** como o disco rígido virtual da máquina, que permite expansão de tamanho (upgrade) em tempo real caso falte espaço.

---

## 💡 Insights e Melhores Práticas Adquiridas

1. **Princípio do Menor Privilégio (IAM):** Nunca devemos utilizar a conta Root no dia a dia. Para gerenciar ou acessar o EC2 via AWS CLI (Linha de Comando), é vital criar usuários com permissões estritamente necessárias e configurar as credenciais `Access Key` e `Secret Access Key` de forma segura.
2. **Evitando Surpresas Financeiras:** A AWS não desliga seus serviços automaticamente quando o limite do Free Tier acaba. A melhor prática é configurar alertas no **AWS Budgets (Billing)** para receber notificações por e-mail assim que os custos atingirem o limite estabelecido.
3. **Persistência de Dados:** Ao desligar uma instância Spot ou terminar uma instância comum, os dados salvos no volume EBS podem ser perdidos se a opção "Delete on Termination" estiver ativa. Dados importantes devem ser salvos no Amazon S3 ou ter snapshots (backups) agendados.
