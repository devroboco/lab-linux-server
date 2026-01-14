# Etapa 09 – Firewall com UFW

## Objetivo da Etapa
Adicionar uma camada de segurança ao servidor por meio de um firewall, controlando explicitamente quais conexões de rede são permitidas.

O foco desta etapa é reduzir a superfície de ataque do servidor, permitindo apenas o tráfego estritamente necessário para o funcionamento dos serviços configurados.

## Conceito de Firewall em Servidores
Um firewall é um mecanismo de controle de tráfego que define quais conexões podem entrar ou sair de um sistema.

Em servidores Linux, a prática recomendada é:
- bloquear todas as conexões de entrada por padrão
- liberar apenas os serviços necessários
- manter o controle centralizado

Essa abordagem segue o princípio do **deny by default**.

## Ferramenta Utilizada: UFW
O UFW (Uncomplicated Firewall) é uma ferramenta de configuração simplificada de firewall baseada no iptables, amplamente utilizada em servidores Ubuntu.

Ele permite gerenciar regras de forma clara e segura, sem necessidade de manipulação direta do iptables.

## Política de Segurança Definida
Para o servidor SFTP, foi adotada a seguinte política:

- Bloquear todo tráfego de entrada por padrão
- Permitir todo tráfego de saída
- Liberar apenas a porta 22 (SSH/SFTP)

Essa política garante que apenas conexões administrativas e de transferência de arquivos sejam aceitas.

## Configuração do Firewall

### Definição das políticas padrão
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

## Liberação do serviço SSH/SFTP
```bash
sudo ufw allow ssh
```
Essa regra permite conexões na porta TCP 22, utilizada tanto pelo SSH quanto pelo SFTP.

## Ativação do firewall
```bash
sudo ufw enable
```
Após a ativação, o firewall passa a filtrar todo o tráfego conforme as regras definidas.

## Verificação do status
```bash
sudo ufw status verbose
```
O resultado esperado é a indicação de que a porta 22 está liberada e o restante bloqueado.

## Testes Realizados
Após a ativação do firewall, foram realizados os seguintes testes:
- Conexão SSH com usuário administrador
- Conexão SFTP com usuários de transferência
- Tentativas de conexão não autorizadas (esperadas falhar)

Os testes confirmaram que o firewall não interferiu nos serviços essenciais e bloqueou acessos indevidos.

## Considerações de Segurança
A utilização do firewall complementa as camadas de segurança já aplicadas no servidor, como autenticação por chave SSH, isolamento de usuários e chroot.

Essa combinação reduz significativamente os riscos de exposição do sistema.

## Conclusão
Ao final desta etapa, o servidor passou a operar com controle explícito de tráfego de rede, alinhando-se às boas práticas de segurança utilizadas em ambientes de produção.
