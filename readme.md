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
        

![trabalho_ct_final](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/f2d56cb9-c425-4e4b-b8a4-e57be31353c6)

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

![trabalho_log_final](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/b833c5ba-255b-4001-86b8-49f99c441623)


### 7	MODELO FÍSICO<br>

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
       
	INSERT INTO estado VALUES
	(01,'Rio de Janeiro','RJ'),
	(02,'Espírito Santo','ES'),
	(03,'São Paulo','SP');
	
	INSERT INTO status VALUES
	(01,'Em deck'),
	(02,'Em venda'),
	(03,'Vendido'),
	(04,'Sem deck');
	
	INSERT INTO endereco VALUES
	(01,29156579,02),
	(02,37456302,03),
	(03,32121251,03),
	(04,54414410,01);
	
	INSERT INTO jogador VALUES
	(01,'Victor Emerson',211313,'2001/04/15','vsiqeui@gmail.com',03),
	(02,'Gilberto Souza',451300,'2000/01/01','gilsouza@gmail.com',01),
	(03,'Aluízio Soares',641101,'1999/12/20','alsoares@gmail.com',02),
	(04,'Emanuel Hoffma',656416,'1997/10/03','emnoida@gmail.com',04);
	
	INSERT INTO carta VALUES
	(01,'Dragão de Fogo',50.00,01,01),
	(02,'Ressonador da Alma',150.65,01,01),
	(03,'Casulo Vermelho',37.80,01,01),
	(04,'Gaia Carmesim',200.00,01,04),
	(05,'Dragão Vermelho',77.99,01,02),
	(06,'Abrasador Dragão',64.64,02,01),
	(07,'Comandar Ressonador',98.31,02,01),
	(08,'Destruição do Ressonante',365.12,02,02),
	(09,'Motor do Ressonador',99.99,02,04),
	(10,'Rei Supremo',50.00,02,01),
	(11,'Rei Celestial Supremo',45.98,02,02),
	(12,'Dragão Arcray',64.65,03,04),
	(13,'Alma do Rei',74.64,03,04),
	(14,'Dragão Pêndulo',14.99,03,04),
	(15,'Anciã Norden',64.30,03,01),
	(16,'Trapezoedro Proibido',241.12,03,04),
	(17,'Salamandra Foguete',303.63,03,02),
	(18,'Atordoamento Sônico',65.99,03,02),
	(19,'Canhão Alabarda',71.99,03,01),
	(20,'Destruidor Laminado',65.12,03,01),
	(21,'Dragão Catapulta',98.65,03,01),
	(22,'Esqueleto de Metal',100.00,04,01),
	(23,'Explosão Estelar',126.63,04,01),
	(24,'Gladiador Poderoso',98.32,04,02),
	(25,'Destruidor Laminado',65.64,04,04),
	(26,'Visas Samsara',35.99,04,04),
	(27,'Abscisão Mannadium',31.40,04,04),
	(28,'Riumheart',50.00,04,04),
	(29,'Bétula Olho de Cobra',60.00,04,01);
	
	INSERT INTO deck VALUES
	(01,01,'Ataque',01,01),
	(02,01,'Ataque',02,01),
	(03,01,'Ataque',03,01),
	(04,02,'Defesa Grande',06,02),
	(05,02,'Defesa Grande',07,02),
	(06,02,'Defesa Grande',10,02),
	(07,03,'Neutro',15,03),
	(08,03,'Neutro',19,03),
	(09,03,'Neutro',20,03),
	(10,03,'Neutro',21,03),
	(11,04,'Morte Súbita',22,04),
	(12,04,'Morte Súbita',23,04),
	(13,04,'Morte Súbita',29,04);
	
	INSERT INTO venda VALUES
	(01,'2023-10-31 10:00:00',05,01),
	(02,'2023-11-16 23:21:00',08,02),
	(03,'2022-09-25 15:52:00',11,02),
	(04,'2023-05-21 10:30:00',17,03),
	(05,'2023-05-20 10:30:00',18,03),
	(06,'2023-06-20 10:30:00',24,04);


### 9	TABELAS E PRINCIPAIS CONSULTAS<br>

#### 9.1	CONSULTAS DAS TABELAS COM TODOS OS DADOS INSERIDOS (Todas) <br>

![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/e7337ae7-c277-42a0-8ce2-fd3626f0824f)

![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/c7dcc995-e554-4af7-b01f-2f0c1b94ff0e)

![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/c9a3ef15-c74d-4202-b1c9-726ab1460dab)

![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/43eac677-7bdf-4025-90a6-b0cec7fb3085)

![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/7f15c82f-6eac-4432-95fd-fd2e01e29ada)

![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/c32823a8-0f9d-45eb-88d5-51905e0e47c7)

![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/bdc714ba-259f-49c8-bf96-2ac9fee0e21d)



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


