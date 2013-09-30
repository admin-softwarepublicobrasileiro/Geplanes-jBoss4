## 1. Orientações Gerais

* <b>ATENÇÃO:</b> Essa versão utiliza a metodologia do BSC (Balanced Scorecard) e, portanto, é incompatível com as versões anterioresà versão 3.0, que utilizam a metodologia GPD (Gerenciamento Pelas Diretrizes).

* Caso você não possua nenhuma versão do Geplanes instalada, vá para o item: <b>Instalação do Geplanes - Versão 3.0.3</b>.
* Caso você possua instalada a versão 3.0 do Geplanes, vá para o item: <b>Atualização da Versão 3.0 para a Versão 3.0.3</b>.
* Caso você possua instalada a versão 3.0.1 do Geplanes, vá para o item: <b>Atualização da Versão 3.0.1 para a Versão 3.0.3</b>.
* Caso você possua instalada a versão 3.0.2 do Geplanes, vá para o item: <b>Atualização da Versão 3.0.2 para a Versão 3.0.3</b>.

## 2. Instalação do Geplanes - Versão 3.0.3

## 2.1. Pré-Requisitos

* Java Development Kit: JDK6 (Vide seção 2.1 do Manual de Instalação da Versão 1.0 em http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-gpd/vers-es/geplanes-1-0-0/Manual_de_Instala%c3%a7%c3%a3o_-_Windows%2epdf)

* Banco de Dados: PostgreSQL 8.3.10-1 (Vide seção 2.2do Manual de Instalação da Versão 1.0 em http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-gpd/vers-es/geplanes-1-0-0/Manual_de_Instala%c3%a7%c3%a3o_-_Windows%2epdf)

* Servidor de Aplicação: JBoss 4.0.5 GA (Vide seção 2.3 do Manual de Instalação da Versão 1.0 em http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-gpd/vers-es/geplanes-1-0-0/Manual_de_Instala%c3%a7%c3%a3o_-_Windows%2epdf)

## 2.2. Criação e configuração do Banco de Dados

Inicialmente, crie um banco de dados com o nome <b><i>geplanes_bsc</i></b>.
Para isso, proceda da seguinte forma:

Abra o prompt de comando (<i>cmd.exe</i>) e vá até a pasta <b>bin</b> do diretório onde foi instalado o PostgreSQL.

    c:\> cd "c:\Program Files\PostgreSQL\8.3\bin"

Em seguida, digite o seguinte comando para criar o banco de dados:

    c:\Program Files\PostgreSQL\8.3\bin>createdb.exe -U postgres geplanes_bsc

Entre com a senha do usuário postgres e pronto. Está criado o banco de dados. Veja figura abaixo:




O próximo passo é executar o script para criação das tabelas do geplanes. Para isso, basta executar o seguinte comando:

    c:\Program Files\PostgreSQL\8.3\bin>psql.exe -U pos tgres -f c:\Temp\geplanes-3.0.3_new.sql -d geplanes _bsc

* Aqui, assume-se que o arquivo <b><i>geplanes-3.0.3_new.sql</i></b> (http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-bsc/vers-es/geplanes-3-0-3/geplanes-3.0.3_new.sql.rar) esteja no diretório Temp da Unidade C. Caso esteja em outro local, basta alterar o caminho acima.

## 2.3. Deploy da Versão 3.0.3

Faça o download do arquivo <b><i>geplanes-3.0.3.war.rar</b></i> (http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-bsc/vers-es/geplanes-3-0-3/geplanes_bsc-3%2e0%2e3%2ewar%2erar), descompacte-o e copie a pasta <b><i>geplanes_bsc.war</b></i> para dentro do diretório <b><i>server/default/deploy</b></i> , localizado dentro do diretório de instalação do JBoss.

## 2.4. Configuração do Servidor de Aplicação (JBoss) para acesso ao banco de dados

Faça o download do arquivo <b><i>geplanes_bsc_postgresql-ds.xml.rar</i></b> (http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-bsc/vers-es/geplanes-3-0-3/geplanes_bsc_postgresql-ds%2exml%2erar), descompacte-o e configure (via bloco de notas ou qualquer outro editor de texto) os parâmetros de acesso ao banco de dados. Posteriormente, copie esse arquivo para a pasta <b><i>server/default/deploy</i></b> do diretório de instalação do JBoss.

Caso o Geplanes seja acessado via rede, você precisará criar pelo menos mais um bloco de configuração de acesso ao banco de dados dentro do arquivo <b><i>geplanes _bsc_postgresql-ds.xml</b></i>. Imagine que o Geplanes tenha sido instalado na máquina cujo IP seja <b><i>192.168.1.54</b></i> e cujo nome seja <b><i>srv54</b></i>.

Para que o Geplanes seja acessado pela URL <b><i>http://192.168.1.54:8080/geplanes_bsc</b></i> é necessária a criação do seguinte bloco de código dentro do arquivo geplanes_bsc_postgresql-ds.xml:
    
    <local-tx-datasource>
       <jndi-name>192.168.1.54_geplanes_bsc_PostgreSQLDS</jndi-name>
       <connection-url>jdbc:postgresql://localhost/geplanes_bsc</connection-url>
       <driver-class>org.postgresql.Driver</driver-class>
       <user-name>postgres</user-name>
       <password>postgres</password>
       <metadata>
          <type-mapping>PostgreSQL 7.2</type-mapping>
       </metadata>
    </local-tx-datasource>
    
Para que o Geplanes seja acessado pela URL <b><i>http://srv54:8080/geplanes_bsc</b></i> é necessária a criação do seguinte bloco de código dentro do arquivo geplanes_bsc_postgresql-ds.xml:
 
    <local-tx-datasource>
       <jndi-name>srv54_geplanes_bsc_PostgreSQLDS</jndi-name>
       <connection-url>jdbc:postgresql://localhost/geplanes_bsc</connection-url>
       <driver-class>org.postgresql.Driver</driver-class>
       <user-name>postgres</user-name>
       <password>postgres</password>
       <metadata>
          <type-mapping>PostgreSQL 7.2</type-mapping>
       </metadata>
    </local-tx-datasource>
    
Lembrando que, caso necessário, os parâmetros de acesso tais como nome e senha do usuário devem ser alterados.

Por fim, para que seja possível o Geplanes acessar as informações do banco de dados PostgreSQL, é necessário que o driver JDBC correspondente esteja disponível para o JBoss. Sendo assim, copie o arquivo <b><i>postgresql-8.3-603.jdbc4.jar</b></i> (http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/bibliotecas/postgresql-8%2e3-603%2ejdbc4%2ejar) para a pasta <b><i>server/default/lib</b></i> do diretório de instalação do JBoss.

## 2.5. Execução da Aplicação

* Inicie o JBoss (execute o arquivo <b><i>run.bat</b></i> dentro da pasta <b>bin</b> do diretório de instalação do JBoss)
* Abra o <i>browser</i> (preferencialmente IE7 ou Firefox 3)
* Digite a URL: <b><i>http://localhost:8080/geplanes_bsc</b></i>
* Entre com os dados de usuário (LOGIN/SENHA): (Default: admin/admin)

## 3.Atualização da Versão 3.0 para a Versão 3.0.3

## 3.1. Pré-Requisitos

* Sistema Geplanes 3.0 instalado.

## 3.2. Undeploy da Versão anterior

* Caso o JBoss esteja ligado, desligue-o.
* Remova a pasta <b><i>geplanes_bsc.war</b></i> do diretório <b><i>server/default/deploy</b></i>, localizado dentro do diretório de instalação do JBoss.
* Vá até a pasta <b><i>/server/default/tmp</b></i> do diretório de instalação do JBoss e apague todo o seu conteúdo, deixando-a vazia.
* Vá até a pasta <b><i>/server/default/work</b></i> do diretório de instalação do JBoss e apague todo o seu conteúdo, deixando-a vazia.

## 3.3. Atualização do Banco de Dados

Faça o download do arquivo <b><i>geplanes-3.0_to-3.0.3.sql.rar</b></i> (http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-bsc/vers-es/geplanes-3-0-3/geplanes-3%2e0_to-3%2e0%2e3%2esql%2erar), descompacte-o e execute o script SQL no(s) banco(s) de dados do Geplanes.

## 3.4. Deploy da Versão 3.0.3

Faça o download do arquivo <b><i>geplanes-3.0.3.war.rar</b></i> (http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-bsc/vers-es/geplanes-3-0-3/geplanes_bsc-3%2e0%2e3%2ewar%2erar), descompacte-o e copie a pasta <b><i>geplanes_bsc.war</b></i> para dentro do diretório <b><i>server/default/deploy</b></i>, localizado dentro do diretório deinstalação do JBoss.

## 3.5. Execução da Aplicação

* Inicie o JBoss (execute o arquivo run.bat dentro da pasta bin do diretório de instalação doJBoss)
* Abra o browser (preferencialmente IE7 ou Firefox 3)
* Digite a URL: <b><i>http://localhost:8080/geplanes_bsc</b></i>
* Entre com os dados de usuário (LOGIN/SENHA): (Default: admin/admin)

## 4.Atualização da Versão 3.0.1 para a Versão 3.0.3

## 4.1. Pré-Requisitos

* Sistema Geplanes 3.0.1 instalado.

## 4.2. Undeploy da Versão anterior

* Caso o JBoss esteja ligado, desligue-o.
* Remova a pasta <b><i>geplanes_bsc.war</b></i> do diretório <b><i>server/default/deploy</b></i>, localizado dentro do diretório de instalação do JBoss.
* Vá até a pasta <b><i>/server/default/tmp</b></i> do diretório de instalação do JBoss e apague todo o seu conteúdo, deixando-a vazia.
* Vá até a pasta <b><i>/server/default/work</b></i> do diretório de instalação do JBoss e apague todo o seu conteúdo, deixando-a vazia.

## 4.3. Atualização do Banco de Dados

Faça o download do arquivo <b><i>geplanes-3.0.1_to-3.0.3.sql.rar</b></i> (http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-bsc/vers-es/geplanes-3-0-3/geplanes-3%2e0%2e1_to-3%2e0%2e3%2esql%2erar), descompacte-o e execute o script SQL no(s) banco(s) de dados do Geplanes.

## 4.4. Deploy da Versão 3.0.3
 
Faça o download do arquivo <b><i>geplanes-3.0.3.war.rar</b></i> (http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-bsc/vers-es/geplanes-3-0-3/geplanes_bsc-3%2e0%2e3%2ewar%2erar), descompacte-o e copie a pasta <b><i>geplanes_bsc.war</b></i> para dentro do diretório <b><i>server/default/deploy</b></i>, localizado dentro do diretório de instalação do JBoss.

## 4.5. Execução da Aplicação

* Inicie o JBoss (execute o arquivo <b><i>run.bat</b></i> dentro da pasta <b>bin</b> do diretório de instalação do JBoss)
* Abra o browser (preferencialmente IE7 ou Firefox 3)
* Digite a URL: <b><i>http://localhost:8080/geplanes_bsc</b></i>
* Entre com os dados de usuário (LOGIN/SENHA): (Default: admin/admin)

##5. Atualização da Versão 3.0.2 para a Versão 3.0.3

##5.1. Pré-Requisitos

* Sistema Geplanes 3.0.2 instalado.

##5.2. Undeploy da Versão anterior

* Caso o JBoss esteja ligado, desligue-o.
* Remova a pasta <b><i>geplanes_bsc.war</b></i> do diretório <b><i>server/default/deploy</b></i>, localizado dentro do diretório de instalação do JBoss.
* Vá até a pasta <b><i>/server/default/tmp</b></i> do diretório de instalação do JBoss e apague todo o seu conteúdo, deixando-a vazia.
* Vá até a pasta <b><i>/server/default/work</b></i> do diretório de instalação do JBoss e apague todo o seu conteúdo, deixando-a vazia.

##5.3. Atualização do Banco de Dados

* Não houve atualização do banco de dados.

##5.4. Deploy da Versão 3.0.3

Faça o download do arquivo <b><i>geplanes-3.0.3.war.rar</b></i> (http://www.softwarepublico.gov.br/dotlrn/clubs/geplanes/file-storage/view/metodologia-bsc/vers-es/geplanes-3-0-3/geplanes_bsc-3%2e0%2e3%2ewar%2erar), descompacte-o e copie a pasta <b><i>geplanes_bsc.war</b></i> para dentro do diretório <b><i>server/default/deploy</b></i>, localizado dentro do diretório de instalação do JBoss.

##5.5. Execução da Aplicação

* Inicie o JBoss (execute o arquivo <b><i>run.bat</b></i> dentro da pasta <b>bin</b> do diretório de instalação do JBoss)
* Abra o browser
* Digite a URL: <b><i>http://localhost:8080/geplanes_bsc</b></i>
* Entre com os dados de usuário (LOGIN/SENHA): (Default: admin/admin)
