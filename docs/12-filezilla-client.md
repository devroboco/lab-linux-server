# Etapa 12 – Testes com Cliente Gráfico (FileZilla)

## Objetivo da Etapa
Validar o funcionamento do servidor SFTP do ponto de vista do usuário final, utilizando um cliente gráfico amplamente adotado no mercado.

Essa etapa tem como foco demonstrar que o servidor configurado pode ser utilizado por usuários comuns, sem necessidade de acesso ao terminal ou conhecimento técnico sobre protocolos e configurações internas.

---

## Conceito de Cliente SFTP Gráfico
Clientes gráficos de SFTP abstraem toda a complexidade do protocolo SSH e permitem que o usuário interaja com o servidor por meio de uma interface visual.

O FileZilla é um dos clientes mais utilizados em ambientes corporativos para transferência segura de arquivos, oferecendo suporte nativo ao protocolo SFTP.

---

## Ferramenta Utilizada
- **FileZilla Client**

A ferramenta foi utilizada apenas como cliente, conectando-se ao servidor SFTP previamente configurado.

---

## Configuração da Conexão no FileZilla
A conexão foi configurada por meio do Gerenciador de Sites do FileZilla, utilizando os seguintes parâmetros:

- Protocolo: SFTP – SSH File Transfer Protocol
- Servidor: IP do servidor Linux
- Porta: 22
- Tipo de logon: Normal
- Usuário: usuário SFTP (ex.: sftpuser1)
- Senha: senha do usuário SFTP

Na primeira conexão, o cliente solicitou a confirmação da chave do servidor, garantindo a autenticidade da conexão.

---

## Testes de Transferência de Arquivos

### Upload de Arquivos
Foi realizado o envio de arquivos do computador cliente para o servidor por meio de arrastar e soltar, diretamente para o diretório `/files`.

O upload ocorreu com sucesso, confirmando as permissões corretas e o funcionamento do serviço.

---

### Download de Arquivos
Também foi realizado o download de arquivos do servidor para o cliente, validando a leitura dos dados e a integridade da transferência.

---

## Testes com Múltiplos Usuários
A conexão foi testada com usuários diferentes configurados no servidor:

- Cada usuário acessou apenas seu próprio diretório `/files`
- Nenhum usuário conseguiu visualizar ou acessar arquivos de outros usuários
- O isolamento entre usuários foi preservado no cliente gráfico

Esses testes confirmaram que o comportamento observado via terminal também se mantém em interfaces gráficas.


## Testes Negativos
Foram realizados testes adicionais para validar a segurança do serviço:

- Tentativa de conexão com usuário inexistente
- Tentativa de conexão com senha incorreta

Em ambos os casos, o acesso foi negado conforme esperado.


## Considerações de Usabilidade
O uso do FileZilla demonstrou que:
- o servidor pode ser utilizado por usuários sem conhecimento técnico
- a complexidade do SSH/SFTP fica restrita ao administrador
- a experiência do usuário final é simples e intuitiva

Essa abordagem reflete o uso real de servidores de arquivos em ambientes profissionais.


## Conclusão
Ao final desta etapa, o servidor SFTP foi validado com um cliente gráfico amplamente utilizado no mercado, comprovando sua usabilidade, segurança e adequação para uso real.

Essa etapa encerra o ciclo completo do projeto, conectando a configuração de infraestrutura ao uso prático pelo usuário final.
