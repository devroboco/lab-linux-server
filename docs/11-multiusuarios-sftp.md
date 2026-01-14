# Etapa 11 – Configuração de Múltiplos Usuários SFTP

## Objetivo da Etapa
Configurar o servidor para suportar múltiplos usuários SFTP simultaneamente, garantindo que cada usuário tenha acesso apenas aos seus próprios arquivos, de forma isolada e segura.

Essa etapa tem como foco simular um ambiente real de servidor de arquivos, no qual diferentes usuários utilizam o mesmo serviço sem interferir nos dados uns dos outros.

## Conceito de Servidor Multiusuário
Um servidor de arquivos multiusuário permite que diversos usuários utilizem o mesmo serviço, mantendo isolamento lógico entre seus dados.

No contexto do SFTP, esse isolamento é alcançado por meio de:
- criação de usuários distintos
- uso de diretórios dedicados
- aplicação de permissões de sistema
- utilização de chroot para confinamento

Esse modelo é amplamente utilizado em ambientes corporativos, educacionais e de hospedagem.

## Estratégia de Implementação
Foi adotada uma estratégia baseada em grupo para facilitar a escalabilidade da configuração:

- criação de um grupo específico para usuários SFTP
- aplicação de regras SSH utilizando `Match Group`
- uso de variáveis dinâmicas para definir o diretório de chroot

Essa abordagem permite adicionar novos usuários sem necessidade de modificar o arquivo de configuração do SSH a cada inclusão.

## Criação dos Usuários
Foram criados múltiplos usuários dedicados à transferência de arquivos, por exemplo:

- `sftpuser1`
- `sftpuser2`

Esses usuários foram configurados exclusivamente para acesso via SFTP.

## Criação do Grupo SFTP
Foi criado um grupo específico para usuários de transferência de arquivos:

```bash
sudo groupadd sftpusers
```

Em seguida, os usuários SFTP foram adicionados a esse grupo:
```bash
sudo usermod -aG sftpusers sftpuser1
sudo usermod -aG sftpusers sftpuser2
```

## Estrutura de Diretórios
Para cada usuário, foi criada uma estrutura de diretórios dedicada:
```bash
/srv/sftp/
├── sftpuser1/
│   └── files/
└── sftpuser2/
    └── files/
```
Cada usuário possui seu próprio diretório de trabalho, evitando qualquer acesso cruzado.

## Permissões e Propriedade
As permissões foram configuradas conforme as exigências do OpenSSH para uso com chroot:
- Diretórios de chroot `(/srv/sftp/usuario)` pertencem ao usuário root
- Diretórios de arquivos `(files)` pertencem ao respectivo usuário

Essa separação garante que o usuário não consiga modificar o ambiente de chroot.

## Configuração do SSH para Múltiplos Usuários
No arquivo de configuração do SSH, foi utilizado um bloco `Match Group` para aplicar regras aos usuários do grupo SFTP:
```bash
Match Group sftpusers
    ChrootDirectory /srv/sftp/%u
    ForceCommand internal-sftp
    AllowTcpForwarding no
    X11Forwarding no
```
A variável `%u` permite que o diretório de chroot seja definido dinamicamente com base no nome do usuário.

## Testes Realizados
Foram realizados testes para validar o isolamento entre usuários:
- Cada usuário conseguiu acessar apenas seu diretório /files
- Usuários não conseguiram visualizar arquivos de outros usuários
- Tentativas de acesso fora do diretório permitido foram bloqueadas

Esses testes confirmaram o correto funcionamento do isolamento multiusuário.

## Considerações de Segurança
A configuração multiusuário aplicada:
- evita vazamento de dados entre usuários
- mantém o controle centralizado pelo administrador
- facilita a adição e remoção de usuários
- segue práticas utilizadas em servidores reais

Essa abordagem garante escalabilidade sem comprometer a segurança.

## Conclusão
Ao final desta etapa, o servidor passou a suportar múltiplos usuários SFTP de forma segura e isolada, consolidando o modelo de servidor de arquivos multiusuário e aproximando o projeto de um ambiente de produção real.
