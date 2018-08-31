
# Configurando Servidor Linux (Amazon Lightsail)
As instruções a seguir apresetam as configurações de um servidor Linux (Ubuntu) para uma aplicação simples construída em Flask.
A aplicação se chama [Catálogo](https://github.com/marshalmori/FlaskApp) e o servidor utilizado é o Amazon Lightsail.


## Especificações do servidor
  * IP público: 18.191.101.227
  * Porta SSH: 2200
  * URLs: http://18.191.101.227/  -  http://www.solariasoft.com.br/


## Sequência das configurações
### Passo 1 - Criar uma instância na Amazon Lightsail
  1. Crie uma conta no [Amazon Lightsail](https://aws.amazon.com/pt/lightsail/)
  2. Clique no botão `Criar Instância`
  3. Com o campo Linux/UNIX selecionado escolha a opção `Somente SO`
  4. Selecione `Ubuntu 16.04 LTS`
  5. Insira o arquivo com a chave SSH pública
  6. Escolha seu plano de Instância
  7. Finalize clicando no botão `Criar`

### Passo 2 - Acessar a instância criada
Para acessar a instância criada digite a linha abaixo no seu terminal.

`$ ssh ubuntu@<IP público> -i ~/.ssh/<nome-do-arquivo-com-sua-chave-privada`

### Passo 3 - Fazendo Update e Upgrade
Depois de acessar o servido com o passo anterior agora vamos atualizá-lo com os seguintes comandos:

`$ sudo apt-get update`

`$ sudo apt-get upgrade`

### Passo 4 - Criando o usuário `grader`
Para criar o usuário `grader` basta executar o seguinte comando:

`$ sudo adduser grader`

Ele vai pedir para inserir uma senha e confirmar e na sequência solicitará o preenchimento de alguns dados que não são obrigatórios podendo continuar apertando o `ENTER`.


### Passo 5 - Transformando `grader` em super usuário
Para fazer isso basta criar um arquivo com o nome grader no seguinte caminho:

`$ sudo nano /etc/sudoers.d/grader`

Cole o conteúdo abaixo nesse arquivo.

`grader ALL=(ALL:ALL) ALL`

### Passo 6 - Mude para o usuário `grader`
Digite a linha abaixo para alterar o usuário de ubuntu para grader e insira a senha que configurou no Passo 4.

`$ su - grader`


### Passo 7 - Inserindo a chave pública
Inserindo a chave pública para acessar como grader. Siga a sequência abaixo para obter isso:

`$ mkdir .ssh`

`$ nano .ssh/authorized_keys`

cole a chave pública no arquivo authorized_keys e salve.

### Passo 8 - Configurando as permissões
A configuração das permissões são dadas pelos comandos a seguir:

`chmod 700 .ssh/`

`chmod 600 .ssh/authorized_keys`

`exit` para sair do usuário grader

`exit` para sair do servidor


## Licença
O projeto Mapa do Bairro foi lançado com a licença [MIT
license](https://github.com/atom-community/markdown-preview-plus/blob/master/LICENSE.md).
