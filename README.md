1. Orientações Gerais

* ATENÇÃO: Essa versão utiliza a metodologia do BSC (Balanced Scorecard) e,portanto, é incompatível com as versões anterioresà versão 3.0, que utilizam a metodologia GPD (Gerenciamento Pelas Diretrizes).

* Caso você não possua nenhuma versão do Geplanes instalada, vá para o item: Instalação do Geplanes - Versão 3.0.3.
 
* Caso você possua instalada a versão 3.0 do Geplanes, vá para o item: Atualização da Versão 3.0 para a Versão 3.0.3.

* Caso você possua instalada a versão 3.0.1 do Geplanes, vá para o item: Atualização da Versão 3.0.1 para a Versão 3.0.3

* Caso você possua instalada a versão 3.0.2 do Geplanes, vá para o item: Atualização da Versão 3.0.2 para a Versão 3.0.3

2. Instalação do Geplanes - Versão 3.0.3

2.1. Pré-Requisitos

•Java Development Kit: JDK6 (Vide seção 2.1 do Manual de Instalação da Versão 1.0 em http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-gpd/vers-es/geplanes-1-0-0/Manual_de_Instala%c3%a7%c3%a3o_-_Windows%2epdf)

•Banco de Dados: PostgreSQL 8.3.10-1 (Vide seção 2.2do Manual de Instalação da Versão 1.0 em http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-gpd/vers-es/geplanes-1-0-0/Manual_de_Instala%c3%a7%c3%a3o_-_Windows%2epdf)

•Servidor de Aplicação: JBoss 4.0.5 GA (Vide seção 2.3 do Manual de Instalação da Versão 1.0 em http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-gpd/vers-es/geplanes-1-0-0/Manual_de_Instala%c3%a7%c3%a3o_-_Windows%2epdf)

2.2. Criação e configuração do Banco de Dados

Inicialmente, crie um banco de dados com o nome geplanes_bsc.

Para isso, proceda da seguinte forma:

Abra o prompt de comando (cmd.exe) e vá até a pasta bin do diretório onde foi instalado o PostgreSQL. c:\> cd "c:\Program Files\PostgreSQL\8.3\bin".

Em seguida, digite o seguinte comando para criar o banco de dados: c:\Program Files\PostgreSQL\8.3\bin>createdb.exe -U postgres geplanes_bsc.

Entre com a senha do usuário postgres e pronto. Está criado o banco de dados. Veja figura abaixo:




O próximo passo é executar o script para criação das tabelas do geplanes. Para isso, basta executar o seguinte comando: c:\Program Files\PostgreSQL\8.3\bin>psql.exe -U pos tgres -f c:\Temp\geplanes-3.0.3_new.sql -d geplanes _bsc

* Aqui, assume-se que o arquivo geplanes-3.0.3_new.sql (http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-bsc/vers-es/geplanes-3-0-3/geplanes-3.0.3_new.sql.rar) esteja no diretório Temp da Unidade C. Caso
esteja em outro local, basta alterar o caminho acim
a.
2.3. Deploy da Versão 3.0.3
Faça o download do arquivo
geplanes-3.0.3.war.rar
(
http://www.softwarepublico.gov.br/dotlrn/clubs/gepl
anes/file-storage/view/metodologia-bsc/vers-
es/geplanes-3-0-3/geplanes_bsc-3%2e0%2e3%2ewar%2era
r
), descompacte-o e copie a pasta
geplanes_bsc.war
para dentro do diretório
server/default/deploy
, localizado dentro do diretório de
instalação do JBoss.
2.4. Configuração do Servidor de Aplicação (JBoss)
para acesso ao banco de dados
Faça o download do arquivo
geplanes_bsc_postgresql-ds.xml.rar
(
http://www.softwarepublico.gov.br/dotlrn/clubs/gepl
anes/file-storage/view/metodologia-bsc/vers-
es/geplanes-3-0-3/geplanes_bsc_postgresql-ds%2exml%
2erar
), descompacte-o e configure (via bloco de
notas ou qualquer outro editor de texto) os parâmet
ros de acesso ao banco de dados. Posteriormente, co
pie
esse arquivo para a pasta
server/default/deploy
do diretório de instalação do JBoss.
Caso o Geplanes seja acessado via rede, você precis
ará criar pelo menos mais um bloco de configuração
de
acesso ao banco de dados dentro do arquivo geplanes
_bsc_postgresql-ds.xml. Imagine que o Geplanes
tenha sido instalado na máquina cujo IP seja
192.168.1.54
e cujo nome seja
srv54
.
Para que o Geplanes seja acessado pela URL
http://192.168.1.54:8080/geplanes_bsc
é necessária a criação
do seguinte bloco de código dentro do arquivo gepla
nes_bsc_postgresql-ds.xml:
<local-tx-datasource>
<jndi-name>192.168.1.54_geplanes_bsc_PostgreSQL
DS</jndi-name>
<connection-url>jdbc:postgresql://localhost/gep
lanes_bsc</connection-url>
<driver-class>org.postgresql.Driver</driver-cla
ss>
<user-name>postgres</user-name>
<password>postgres</password>
<metadata>
<type-mapping>PostgreSQL 7.2</type-mapping>
</metadata>
</local-tx-datasource>
5
Para que o Geplanes seja acessado pela URL
http://srv54:8080/geplanes_bsc
é necessária a criação do
seguinte bloco de código dentro do arquivo geplanes
_bsc_postgresql-ds.xml:
<local-tx-datasource>
<jndi-name>srv54_geplanes_bsc_PostgreSQLDS</jnd
i-name>
<connection-url>jdbc:postgresql://localhost/gep
lanes_bsc</connection-url>
<driver-class>org.postgresql.Driver</driver-cla
ss>
<user-name>postgres</user-name>
<password>postgres</password>
<metadata>
<type-mapping>PostgreSQL 7.2</type-mapping>
</metadata>
</local-tx-datasource>
Lembrando que, caso necessário, os parâmetros de ac
esso tais como nome e senha do usuário devem ser
alterados.
Por fim, para que seja possível o Geplanes acessar
as informações do banco de dados PostgreSQL, é
necessário que o driver JDBC correspondente esteja
disponível para o JBoss. Sendo assim, copie o arqui
vo
postgresql-8.3-603.jdbc4.jar
(
http://www.softwarepublico.gov.br/dotlrn/clubs/gepl
anes/file-
storage/view/bibliotecas/postgresql-8%2e3-603%2ejdb
c4%2ejar
) para a pasta
server/default/lib
do
diretório de instalação do JBoss.
2.5. Execução da Aplicação
•
Inicie o JBoss (execute o arquivo run.bat dentro d
a pasta bin do diretório de instalação do
JBoss)
•
Abra o browser (preferencialmente IE7 ou Firefox 3)
•
Digite a URL:
http://localhost:8080/geplanes_bsc
•
Entre com os dados de usuário (LOGIN/SENHA): (Defau
lt: admin/admin)
