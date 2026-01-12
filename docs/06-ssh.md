# Etapa 6 – Acesso Remoto Seguro via SSH

## Objetivo da Etapa
Habilitar e validar o acesso remoto ao servidor Linux por meio do protocolo SSH (Secure Shell), permitindo a administração do sistema de forma segura e sem dependência do console da máquina virtual.

Essa etapa simula o método padrão utilizado por profissionais de redes e infraestrutura para gerenciar servidores em ambientes corporativos e em nuvem.

---

## Conceito de SSH
O SSH (Secure Shell) é um protocolo de rede que permite a conexão remota segura entre um cliente e um servidor, utilizando criptografia para proteger os dados transmitidos.  
Por padrão, o SSH opera na porta TCP 22.

Em servidores reais, o SSH é o principal meio de administração remota, substituindo acessos físicos ou interfaces gráficas.

---

## Instalação do Serviço SSH
O pacote responsável pelo serviço SSH no Ubuntu é o `openssh-server`.  
A instalação foi realizada por meio do gerenciador de pacotes do sistema:

```bash
sudo apt install openssh-server
```

## Ativação do Serviço
Após a instalação, o serviço SSH encontrava-se inativo.
Foram executados os seguintes comandos para iniciar o serviço e configurá-lo para inicialização automática no boot do sistema:

```bash
sudo systemctl start ssh
sudo systemctl enable ssh
```
A verificação do estado do serviço foi realizada com:

```bash
systemctl status ssh
```
Confirmando que o serviço se encontra ativo e em execução.

## Testes de Funcionamento
Teste Local
O funcionamento do SSH foi inicialmente validado localmente no próprio servidor:

```bash
ssh localhost
```
Esse teste confirmou que o serviço estava operacional e aceitando conexões.

Teste Remoto
Em seguida, foi realizado o acesso remoto ao servidor a partir do sistema hospedeiro (Windows), utilizando o endereço IP da máquina virtual:

```bash
ssh usuario@IP_DO_SERVIDOR
```
A conexão foi estabelecida com sucesso, validando o acesso remoto seguro ao servidor Linux.

## Conclusão
Ao final desta etapa, o servidor encontra-se acessível remotamente por meio do protocolo SSH, possibilitando sua administração de forma segura, eficiente e alinhada às boas práticas de infraestrutura de redes.
