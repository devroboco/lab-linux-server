# Etapa 7 – Serviço de Transferência de Arquivos com SFTP

## Objetivo da Etapa
Implementar e compreender o funcionamento do SFTP (SSH File Transfer Protocol) como serviço de transferência de arquivos seguro, utilizando o mesmo canal criptografado do SSH.

Esta etapa tem como foco o entendimento do fluxo cliente-servidor, autenticação de usuários e transferência de arquivos entre o host e o servidor Linux.

---

## Conceito de SFTP
O SFTP é um protocolo de transferência de arquivos que opera como um subsistema do SSH.  
Diferentemente do FTP tradicional, o SFTP utiliza criptografia, garantindo confidencialidade e integridade dos dados transferidos.

O SFTP utiliza a mesma porta TCP 22 do SSH e compartilha os mesmos mecanismos de autenticação.

---

## Criação de Usuário para Transferência de Arquivos
Foi criado um usuário específico para operações de transferência de arquivos, seguindo a boa prática de não utilizar usuários administrativos para serviços:

```bash
sudo adduser ftpuser
```
Esse usuário foi utilizado exclusivamente para acesso via SFTP.

## Funcionamento do Acesso SFTP
O acesso ao serviço foi realizado a partir do sistema hospedeiro (Windows), utilizando o cliente SFTP:

```bash
sftp ftpuser@IP_DO_SERVIDOR
```
Após a autenticação, o usuário foi posicionado automaticamente em seu diretório HOME, conforme comportamento padrão do OpenSSH.

## Transferência de Arquivos
Foram realizados testes de upload e download de arquivos entre o host e o servidor.

Comandos utilizados no cliente SFTP:
- lpwd – exibe o diretório local (host)
- lcd – altera o diretório local
- pwd – exibe o diretório remoto (servidor)
- cd – altera o diretório remoto
- put – envia arquivos do host para o servidor
- get – baixa arquivos do servidor para o host

Esses testes validaram o funcionamento correto da transferência de arquivos via SFTP.

## Conclusão
Ao final desta etapa, o servidor foi capaz de oferecer um serviço funcional de transferência de arquivos via SFTP, permitindo a comunicação segura entre cliente e servidor e consolidando os conceitos fundamentais do protocolo.
