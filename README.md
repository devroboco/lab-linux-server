# lab-linux-server

Laboratório prático de redes e infraestrutura com servidor Linux em máquina virtual.

Este projeto documenta a criação, configuração e administração de um servidor Linux em ambiente virtualizado, com foco em fundamentos de redes, serviços de infraestrutura, segurança e troubleshooting, simulando cenários reais enfrentados por profissionais da área de redes e sistemas.

## Objetivos do Projeto
- Compreender o funcionamento de um servidor Linux em ambiente controlado
- Validar conectividade de rede (endereçamento IP, gateway e DNS)
- Configurar e administrar serviços de transferência de arquivos via SFTP
- Aplicar boas práticas de segurança (firewall, autenticação e isolamento)
- Simular um servidor multiusuário com controle de acesso
- Documentar práticas reais de administração de sistemas

## Tecnologias Utilizadas
- **VMware Workstation Player**
- **Linux Server (imagem pré-configurada)**
- **OpenSSH (SSH e SFTP)**
- **UFW (Uncomplicated Firewall)**
- **Terminal Linux**
- **Git e GitHub**

## Estrutura do Projeto
```bash
lab-linux-server/
├── docs/
│ ├── 01-introducao.md
│ ├── 02-ambiente.md
│ ├── 03-vm-linux.md
│ ├── 04-rede.md
│ ├── 05-servicos.md
│ ├── 06-ssh.md
│ ├── 07-sftp.md
│ ├── 08-sftp-hardening.md
│ ├── 09-firewall-ufw.md
│ ├── 10-ssh-key-auth.md
│ ├── 11-multiusuarios-sftp.md
│ └── 12-filezilla-client.md
│
└── images/
```

## Principais Funcionalidades Implementadas
- Acesso remoto seguro via SSH
- Autenticação SSH por chave (sem uso de senha para administração)
- Serviço SFTP configurado sobre SSH
- Isolamento de usuários utilizando chroot
- Servidor multiusuário com diretórios individuais
- Controle de permissões e propriedade de arquivos
- Firewall configurado permitindo apenas serviços essenciais
- Testes de acesso via cliente gráfico (FileZilla)

## Conceitos Praticados
- Arquitetura cliente-servidor
- Endereçamento IP e comunicação em rede
- Gerenciamento de usuários e grupos no Linux
- Permissões de arquivos e diretórios
- Segurança em camadas (defense in depth)
- Hardening de serviços
- Troubleshooting em ambientes Linux

## Observações
Este projeto tem caráter educacional e foi desenvolvido com foco no aprendizado prático de redes e infraestrutura, reproduzindo situações reais encontradas em ambientes corporativos e laboratórios de TI.

Toda a configuração foi realizada manualmente, sem uso de ferramentas de automação, visando o entendimento profundo do funcionamento dos serviços.

## Possíveis Extensões Futuras
- Implementação de diretórios compartilhados
- Monitoramento e logs de acesso
- Exposição controlada do servidor para acesso externo
