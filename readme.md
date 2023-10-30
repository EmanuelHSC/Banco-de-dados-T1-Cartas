# TRABALHO 01:  Cartas
Trabalho desenvolvido durante a disciplina de BD1

# Sumário

### 1. COMPONENTES<br>
Integrantes do grupo<br>
Gabriel Barbosa | gblucas180902@gmail.com<br>
Emanuel Hoffmann | emanuelhoffmann0@hotmail.com<br>
Izaque Oliveira | izaqueoliveirap@gmail.com<br>
Victor Emerson | vsiqueiradesouza@gmail.com <br>


### 2.MINI-MUNDO<br>

> O sistema de gestão proposto para jogadores de Trading Card Games (TCG) e colecionadores de cartas é uma solução completa que visa atender às diversas necessidades desses entusiastas. Seu objetivo principal é centralizar e simplificar todas as atividades relacionadas às cartas colecionáveis.A solução terá cadastro de cartas e de jogadores jogadores onde eles poderão adicionar suas cartas facilmente, inserindo informações detalhadas, como <nome da carta, coleção, número, tipo, raridade, desgaste da carta e quantidade disponível> e cada jogadores vai se cadastrar no sistema e deve conter nome, cpf, data de nascimento, endereço e email. Além disso, a qualidade da carta é levada em consideração, com opções que variam de Nova (Mint) a Danificada (Damage) cada jogador pode ter varias cartas cadastradas ou nenhuma, e cada carta cadastrada no site tem que estar ligada a apenas um jogador pois cada carta é unica.Para facilitar a organização de suas coleções, os usuários podem fazer decks que vão constar a carta, o usuario e o tipo de deck varia de acordo com o tema escolhido (ex:pokemon) cada jogador pode ter um ou mais decks mas tambem podem ter nenhum deck, os deck podem conter nenhum ou varias cartas, a mesma carta pode estar em decks diferentes. . As cartas tem valor, que são atribuidas no cadastro caso o jogador quuiser vendela, ou pode dser cadastrado depois. Quando é efetuada uma venda as informações são armazenadas com as informações referente a carta vendida, o horario e a data. Em resumo, a implementação deste sistema proporcionará aos jogadores de TCG e colecionadores de cartas uma plataforma centralizada e abrangente para gerenciar suas coleções, realizar transações de forma segura, interagir com outros jogadores e acessar informações essenciais sobre suas cartas.

### 3.PERGUNTAS A SEREM RESPONDIDAS<br>
#### 3.1 QUAIS PERGUNTAS PODEM SER RESPONDIDAS COM O SISTEMA PROPOSTO?

> A Empresa CARTAS precisa inicialmente dos seguintes relatórios:
* Relatorio que mostre todas as transações feita entre jogadores dizendo o valor, hora, item, quem vendeu e quem comprou.
* Relatorio que mostre todas as informações de perfis cadastrados, com nome, cpf, dataNascimento, endereço, email, login e senha.
* Relatorio com todos os decks feitos, mostrando o jogador que pertence o deck, cartas que estão no deck com seus atributos que são nome da carta, coleção, número, tipo, raridade, desgaste da carta e quantidade disponível.
* Relatorio referente a vendas que vai conter qual usuario que vendeu mais cartas com as informações do usuario e das cartas.
* Relatorio de cartas, onde mostre todas as cartas cadastradas com suas informações agrupando a por quantidade da mesma carta

    
### 5.MODELO CONCEITUAL<br>
        
![image](https://github.com/EmanuelHSC/TemplateBD1/assets/116691668/ce7efa25-b4af-41bf-af58-11747efb9f0f)
    
#### 5.1 Validação do Modelo Conceitual
    
    [Grupo01]: [Rodolfo Oliveira]
    [Grupo02]: [Artur cremasco]

#### 5.2 Descrição dos dados 

    CLIENTE: Tabela que armazena as informações relativas ao cliente<br>
    CARTAS: Tabela que armazena as informações de cada cartas<br>
    ENDEREÇO: Tabela que informa as informações de endereço que são ligadas ao cliente<br>
    DECK: Tabela que contem varias cartas de um mesmo jogador
    

># Marco de Entrega 01: Do item 1 até o item 5.2 (5 PTS) <br> 

### 6	MODELO LÓGICO<br>

![image](https://github.com/EmanuelHSC/TemplateBD1/assets/116691668/dd866d80-b8f4-4280-8070-91c7290e5555)


### 7	MODELO FÍSICO<br>
### falta ajustar ( vou tirar um cochilo ja ja volto ) estou mexendo
	DROP TABLE IF EXISTS estado   CASCADE;
DROP TABLE IF EXISTS status   CASCADE;
DROP TABLE IF EXISTS endereco CASCADE;
DROP TABLE IF EXISTS jogador  CASCADE;
DROP TABLE IF EXISTS carta 	  CASCADE;
DROP TABLE IF EXISTS deck 	  CASCADE;
DROP TABLE IF EXISTS venda 	  CASCADE;

CREATE TABLE estado(
	id_estado SERIAL PRIMARY KEY,
	desc_estd VARCHAR(50),
	sigla VARCHAR(2)
);

CREATE TABLE status(
	id_status SERIAL PRIMARY KEY,
	desc_status VARCHAR(50)
);

CREATE TABLE endereco(
	id_end SERIAL PRIMARY KEY,
	cep NUMERIC,
	FK_id_estado INTEGER,
	FOREIGN KEY(FK_id_estado)
	REFERENCES ESTADO(id_estado)	
);

CREATE TABLE jogador(
	id_jogador SERIAL PRIMARY KEY,
	nome VARCHAR(100),
	cpf NUMERIC,
	dt_nasc DATE,
	email VARCHAR(100),
	FK_id_end INTEGER,
	FOREIGN KEY(FK_id_end)
	REFERENCES ENDERECO(id_end)
);

CREATE TABLE carta(
	id_carta SERIAL PRIMARY KEY,
	nome_card VARCHAR(100),
	preco FLOAT,
	FK_id_jogador INTEGER,
	FOREIGN KEY(FK_id_jogador)
	REFERENCES JOGADOR(id_jogador),
	FK_id_status INTEGER,
	FOREIGN KEY(FK_id_status)
	REFERENCES STATUS(id_status)
);

CREATE TABLE deck(
	cod_table SERIAL PRIMARY KEY,
	id_deck SERIAL,
	nome VARCHAR(50),
	FK_id_carta INTEGER,
	FOREIGN KEY(FK_id_carta)
	REFERENCES CARTA(id_carta),
	FK_id_jogador INTEGER,
	FOREIGN KEY(FK_id_jogador)
	REFERENCES JOGADOR(id_jogador)
);

CREATE TABLE venda(
	id_venda SERIAL PRIMARY KEY,
	dt_venda DATE,
	FK_id_carta INTEGER,
	FOREIGN KEY(FK_id_carta)
	REFERENCES CARTA(id_carta),
	FK_id_jogador INTEGER,
	FOREIGN KEY(FK_id_jogador)
	REFERENCES JOGADOR(id_jogador)
)
      
### 8	INSERT APLICADO NAS TABELAS DO BANCO DE DADOS<br>
        a) Script das instruções relativas a inclusão de dados 
	Requisito mínimo: (Script dev conter: Drop para exclusão de tabelas + create definição de para tabelas e estruturas de dados + insert para dados a serem inseridos)
        OBS
	1) Criar um novo banco de dados para testar a restauracao (em caso de falha na restauração o grupo não pontuará neste quesito)
        2) script deve ser incluso no template em um arquivo no formato .SQL


### 9	TABELAS E PRINCIPAIS CONSULTAS<br>
    Link para o Google Collab: https://colab.research.google.com/drive/10ci9CFayCj2BKYTozd7JU8E9mpNHHzVw?usp=sharing
    OBS: Usa template da disciplina disponibilizado no Colab.<br>
#### 9.1	CONSULTAS DAS TABELAS COM TODOS OS DADOS INSERIDOS (Todas) <br>

#### 9.2	CONSULTAS DAS TABELAS COM FILTROS WHERE (Mínimo 4)<br>

#### 9.3	CONSULTAS QUE USAM OPERADORES LÓGICOS, ARITMÉTICOS E TABELAS OU CAMPOS RENOMEADOS (Mínimo 11)
    a) Criar 5 consultas que envolvam os operadores lógicos AND, OR e Not
    b) Criar no mínimo 3 consultas com operadores aritméticos 
    c) Criar no mínimo 3 consultas com operação de renomear nomes de campos ou tabelas

#### 9.4	CONSULTAS QUE USAM OPERADORES LIKE E DATAS (Mínimo 12) <br>
    a) Criar outras 5 consultas que envolvam like ou ilike
    b) Criar uma consulta para cada tipo de função data apresentada.

># Marco de Entrega 02: Do item 6. até o item 9.1 (5 PTS) <br>

#### 9.5	INSTRUÇÕES APLICANDO ATUALIZAÇÃO E EXCLUSÃO DE DADOS (Mínimo 6)<br>
    a) Criar minimo 3 de exclusão
    b) Criar minimo 3 de atualização

#### 9.6	CONSULTAS COM INNER JOIN E ORDER BY (Mínimo 6)<br>
    a) Uma junção que envolva todas as tabelas possuindo no mínimo 2 registros no resultado
    b) Outras junções que o grupo considere como sendo as de principal importância para o trabalho

#### 9.7	CONSULTAS COM GROUP BY E FUNÇÕES DE AGRUPAMENTO (Mínimo 6)<br>
    a) Criar minimo 2 envolvendo algum tipo de junção

#### 9.8	CONSULTAS COM LEFT, RIGHT E FULL JOIN (Mínimo 4)<br>
    a) Criar minimo 1 de cada tipo

#### 9.9	CONSULTAS COM SELF JOIN E VIEW (Mínimo 6)<br>
        a) Uma junção que envolva Self Join (caso não ocorra na base justificar e substituir por uma view)
        b) Outras junções com views que o grupo considere como sendo de relevante importância para o trabalho

#### 9.10	SUBCONSULTAS (Mínimo 4)<br>
     a) Criar minimo 1 envolvendo GROUP BY
     b) Criar minimo 1 envolvendo algum tipo de junção

># Marco de Entrega 03: Do item 9.2 até o ítem 9.10 (10 PTS)<br>

### 10 RELATÓRIOS E GRÁFICOS

#### a) análises e resultados provenientes do banco de dados desenvolvido (usar modelo disponível)
#### b) link com exemplo de relatórios será disponiblizado pelo professor no AVA
#### OBS: Esta é uma atividade de grande relevância no contexto do trabalho. Mantenha o foco nos 5 principais relatórios/resultados visando obter o melhor resultado possível.

    

### 11	AJUSTES DA DOCUMENTAÇÃO, CRIAÇÃO DOS SLIDES E VÍDEO PARA APRESENTAÇAO FINAL <br>

#### a) Modelo (pecha kucha)<br>
#### b) Tempo de apresentação 6:40 

># Marco de Entrega 04: Itens 10 e 11 (20 PTS) <br>
<br>
<br>




### 12 FORMATACAO NO GIT:<br> 
https://help.github.com/articles/basic-writing-and-formatting-syntax/
<comentario no git>
    
##### About Formatting
    https://help.github.com/articles/about-writing-and-formatting-on-github/
    
##### Basic Formatting in Git
    
    https://help.github.com/articles/basic-writing-and-formatting-syntax/#referencing-issues-and-pull-requests
    
    
##### Working with advanced formatting
    https://help.github.com/articles/working-with-advanced-formatting/
#### Mastering Markdown
    https://guides.github.com/features/mastering-markdown/

    
### OBSERVAÇÕES IMPORTANTES

#### Todos os arquivos que fazem parte do projeto (Imagens, pdfs, arquivos fonte, etc..), devem estar presentes no GIT. Os arquivos do projeto vigente não devem ser armazenados em quaisquer outras plataformas.
1. <strong>Caso existam arquivos com conteúdos sigilosos<strong>, comunicar o professor que definirá em conjunto com o grupo a melhor forma de armazenamento do arquivo.

#### Todos os grupos deverão fazer Fork deste repositório e dar permissões administrativas ao usuário do git "profmoisesomena", para acompanhamento do trabalho.

#### Os usuários criados no GIT devem possuir o nome de identificação do aluno (não serão aceitos nomes como Eu123, meuprojeto, pro456, etc). Em caso de dúvida comunicar o professor.


Link para BrModelo:<br>
http://www.sis4.com/brModelo/download.html
<br>


Link para curso de GIT<br>
![https://www.youtube.com/curso_git](https://www.youtube.com/playlist?list=PLo7sFyCeiGUdIyEmHdfbuD2eR4XPDqnN2?raw=true "Title")


