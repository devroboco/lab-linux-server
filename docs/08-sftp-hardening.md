# Etapa 8 – SFTP Profissional: Isolamento e Hardening

## Objetivo da Etapa
Aplicar técnicas de segurança (hardening) ao serviço SFTP, transformando a configuração básica em um ambiente controlado e alinhado às boas práticas utilizadas em servidores de produção.

O foco desta etapa é restringir o usuário de transferência de arquivos, garantindo isolamento do sistema, controle de permissões e redução da superfície de ataque.

## Conceito de Hardening em Servidores
Hardening é o conjunto de práticas aplicadas a um sistema com o objetivo de reduzir riscos de segurança, limitando acessos, removendo funcionalidades desnecessárias e aplicando o princípio do menor privilégio.

Em servidores de arquivos, isso envolve:
- isolamento de usuários
- restrição de comandos
- controle rigoroso de permissões
- limitação do acesso ao sistema operacional

## Uso de Chroot no SFTP
Foi utilizado o mecanismo de `ChrootDirectory` do OpenSSH para isolar o usuário de arquivos em um diretório específico.

Com o chroot configurado, o usuário passa a enxergar esse diretório como se fosse a raiz do sistema (`/`), não sendo possível acessar outros caminhos do servidor.

Essa técnica é amplamente utilizada em ambientes corporativos para serviços de arquivos.

## Estrutura de Diretórios
Foi criada a seguinte estrutura no servidor:
```bash
/srv/sftp/
└── ftpuser/
└── files/
```

- `/srv/sftp` e `/srv/sftp/ftpuser` são diretórios protegidos, pertencentes ao usuário root.
- `/srv/sftp/ftpuser/files` é o diretório destinado à gravação de arquivos pelo usuário `ftpuser`.

Essa separação é necessária para atender às exigências de segurança do OpenSSH.

## Permissões e Propriedade
As permissões foram configuradas conforme as boas práticas do OpenSSH para ambientes chroot:

- Diretórios de chroot: propriedade do `root` e sem permissão de escrita para o usuário
- Diretório de arquivos: propriedade do usuário de transferência (`ftpuser`)

Essa configuração impede que o usuário modifique a estrutura do chroot ou escape do ambiente isolado.

## Restrição de Shell
O usuário `ftpuser` teve seu shell desabilitado:

```bash
sudo usermod -s /usr/sbin/nologin ftpuser
```
Com isso:
- conexões via SSH com shell são bloqueadas
- apenas o acesso via SFTP é permitido

Essa prática reduz significativamente os riscos de acesso indevido ao sistema.

## Configuração do OpenSSH
O serviço SSH foi configurado para utilizar o subsistema interno de SFTP:
```bash
Subsystem sftp internal-sftp
```
E foi adicionado um bloco de regras específico para o usuário de arquivos:
```bash
Match User ftpuser
    ChrootDirectory /srv/sftp/ftpuser
    ForceCommand internal-sftp
    AllowTcpForwarding no
    X11Forwarding no
```

Essas diretivas garantem que o usuário:
- utilize exclusivamente o SFTP
- permaneça confinado ao diretório definido
- não utilize recursos adicionais do SSH

## Testes Realizados
Teste de Acesso SSH
```bash
ssh ftpuser@IP_DO_SERVIDOR
```

Resultado esperado:
- acesso negado ao shell

Esse comportamento confirma a restrição correta do usuário.

Teste de Acesso SFTP

```bash
sftp ftpuser@IP_DO_SERVIDOR
```

Após a conexão:
- o diretório inicial exibido foi `/`
- a transferência de arquivos foi realizada com sucesso apenas dentro do diretório `files`

Esse resultado confirma o funcionamento correto do chroot e das permissões configuradas.

## Considerações de Segurança
A configuração aplicada nesta etapa:
- impede acesso ao sistema operacional
- limita a escrita a diretórios específicos
- utiliza criptografia para transferência de dados
- segue práticas comuns em servidores corporativos
  
Essa abordagem reduz riscos e aumenta a confiabilidade do serviço de arquivos.

## Conclusão
Ao final desta etapa, o servidor passou a oferecer um serviço SFTP seguro, isolado e alinhado às boas práticas de infraestrutura.

O ambiente está preparado para uso em cenários reais de transferência de arquivos, com controle de acesso, isolamento de usuários e segurança reforçada.
