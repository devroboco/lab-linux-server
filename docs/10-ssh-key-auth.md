# Etapa 10 – Autenticação SSH por Chave

## Objetivo da Etapa
Substituir a autenticação baseada em senha por autenticação via chave SSH para o usuário administrador do servidor, aumentando o nível de segurança do acesso remoto.

Essa etapa tem como foco reduzir riscos de ataques por força bruta, eliminar o uso de senhas em conexões administrativas e alinhar o servidor às práticas adotadas em ambientes corporativos e serviços em nuvem.

## Conceito de Autenticação por Chave SSH
A autenticação por chave SSH utiliza criptografia assimétrica, baseada em um par de chaves:

- Chave privada: permanece no computador do administrador
- Chave pública: armazenada no servidor

Durante a conexão, o servidor valida se o cliente possui a chave privada correspondente à chave pública autorizada, permitindo o acesso sem o uso de senha.

Esse método é amplamente utilizado em servidores de produção e plataformas cloud.

## Geração do Par de Chaves
O par de chaves foi gerado no computador cliente utilizando o algoritmo `ed25519`, recomendado por sua segurança e eficiência.

```bash
ssh-keygen -t ed25519
```
A chave privada foi mantida localmente e a chave pública utilizada para autenticação no servidor.

## Distribuição da Chave Pública
A chave pública foi copiada para o servidor e associada ao usuário administrador, permitindo autenticação sem senha.

Esse processo pode ser realizado manualmente ou utilizando ferramentas específicas do OpenSSH.

Após a configuração, o acesso remoto passou a exigir a posse da chave privada correspondente.

## Desativação da Autenticação por Senha
Para reforçar a segurança, a autenticação por senha foi desativada no serviço SSH.

No arquivo de configuração do SSH `(sshd_config)`, foram aplicadas as seguintes diretivas:

```bash
PasswordAuthentication no
PubkeyAuthentication yes
```
Essa configuração garante que apenas autenticação por chave seja aceita para conexões SSH.

## Restrição de Login do Usuário Root
Como medida adicional de segurança, o login direto do usuário root foi desativado:

```bash
PermitRootLogin no
```
Essa prática evita acessos diretos privilegiados, exigindo que o administrador utilize um usuário comum com permissões elevadas quando necessário.

## Reinicialização do Serviço SSH
Após as alterações de configuração, o serviço SSH foi reiniciado para aplicar as novas regras:

```bash
sudo systemctl restart ssh
```

## Testes Realizados
Foram realizados os seguintes testes:
- Conexão SSH com usuário administrador utilizando chave (acesso permitido)
- Tentativa de acesso SSH utilizando senha (acesso negado)
- Teste de acesso SFTP com usuários de transferência (funcionamento preservado)

Os testes confirmaram que a autenticação por chave está ativa e que a desativação de senha não afetou os serviços configurados.

## Considerações de Segurança
A autenticação por chave elimina a necessidade de senhas em conexões administrativas, reduzindo significativamente riscos de ataques automatizados.

Combinada com firewall e isolamento de usuários, essa abordagem fortalece o modelo de segurança do servidor.

## Conclusão 
Ao final desta etapa, o servidor passou a utilizar autenticação segura por chave SSH para acessos administrativos, alinhando-se às boas práticas de segurança adotadas em ambientes profissionais.
