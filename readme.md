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
* Relatorio que mostre de onde são as pessoas que usam o site.
* Relatorio que informa top 5 vendedores de cartas.
* Relatório que mostre quantas cartas do tipo dragão nós temos no sistema e seus respectivos preços.
* Relatório com top 5 vendas do site.
* Relatório de preço das cartas das pessoas.


    
### 5.MODELO CONCEITUAL<br>
        

![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/258fd795-d77e-4cd9-9d09-200ebed0d303)



#### 5.1 Validação do Modelo Conceitual
    
    [Grupo01]: [Rodolfo Oliveira]
    [Grupo02]: [Artur cremasco]

#### 5.2 Descrição dos dados 

	Tabela estado:
	id_estado (Chave primária serial): Identificador único para cada estado.
	desc_estd (VARCHAR(50)): Descrição do estado.
	sigla (VARCHAR(2)): Sigla do estado.
	
 	Tabela status:
	id_status (Chave primária serial): Identificador único para cada status.
	desc_status (VARCHAR(50)): Descrição do status.
	
 
	Tabela endereco:
	id_end (Chave primária serial): Identificador único para cada endereço.
	cep (NUMERIC): Código de Endereçamento Postal (CEP).
	FK_id_estado (INTEGER): Chave estrangeira que se refere ao id_estado na tabela estado.
	
 	Tabela jogador:
	id_jogador (Chave primária serial): Identificador único para cada jogador.
	nome (VARCHAR(100)): Nome do jogador.
	cpf (NUMERIC): Número de CPF do jogador.
	dt_nasc (DATE): Data de nascimento do jogador.
	email (VARCHAR(100)): Endereço de e-mail do jogador.
	FK_id_end (INTEGER): Chave estrangeira que se refere ao id_end na tabela endereco.
	
 	Tabela carta:
	id_carta (Chave primária serial): Identificador único para cada carta.
	nome_card (VARCHAR(100)): Nome da carta.
	preco (FLOAT): Preço da carta.
	FK_id_jogador (INTEGER): Chave estrangeira que se refere ao id_jogador na tabela jogador.
	FK_id_status (INTEGER): Chave estrangeira que se refere ao id_status na tabela status.
	
	Tabela deck:
	cod_table (Chave primária serial): Identificador único para cada registro na tabela deck.
	id_deck (SERIAL): Identificador do deck.
	nome (VARCHAR(50)): Nome do deck.
	FK_id_carta (INTEGER): Chave estrangeira que se refere ao id_carta na tabela carta.
	FK_id_jogador (INTEGER): Chave estrangeira que se refere ao id_jogador na tabela jogador.
	
 	Tabela venda:
	id_venda (Chave primária serial): Identificador único para cada venda.
	dt_venda (DATE): Data da venda.
	FK_id_carta (INTEGER): Chave estrangeira que se refere ao id_carta na tabela carta.
	FK_id_jogador (INTEGER): Chave estrangeira que se refere ao id_jogador na tabela jogador.
    

># Marco de Entrega 01: Do item 1 até o item 5.2 (5 PTS) <br> 

### 6	MODELO LÓGICO<br>

![trabalho_log_final](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/b833c5ba-255b-4001-86b8-49f99c441623)


### 7	MODELO FÍSICO<br>

	DROP TABLE IF EXISTS estado   CASCADE;
	DROP TABLE IF EXISTS status   CASCADE;
	DROP TABLE IF EXISTS endereco CASCADE;
	DROP TABLE IF EXISTS jogador  CASCADE;
	DROP TABLE IF EXISTS carta    CASCADE;
	DROP TABLE IF EXISTS deck     CASCADE;
	DROP TABLE IF EXISTS venda    CASCADE;
	
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
	(04,54414410,01),
	(04,'Minas Gerais','MG'),
	(05,'Bahia','BA'),
	(06,'Paraná','PR'),
	(07,'Ceará','CE'),
	(08,'Amazonas','AM');

	
	INSERT INTO jogador VALUES
	(01,'Victor Emerson',211313,'2001/04/15','vsiqeui@gmail.com',03),
	(02,'Gilberto Souza',451300,'2000/01/01','gilsouza@gmail.com',01),
	(03,'Aluízio Soares',641101,'1999/12/20','alsoares@gmail.com',02),
	(04,'Emanuel Hoffma',656416,'1997/10/03','emnoida@gmail.com',04)
 	(05,'Amanda Silva',987654,'1995/08/20','amanda@gmail.com',05),
	(06,'Lucas Oliveira',123456,'1998/03/12','lucas@gmail.com',06),
	(07,'Juliana Santos',456789,'2002/06/25','juliana@gmail.com',07),
	(08,'Rafael Souza',789012,'1990/12/01','rafael@gmail.com',08),
	(09,'Fernanda Lima',345678,'1997/05/18','fernanda@gmail.com',09);
	(10,'Mariana Costa',33221144556,'1996/12/05','mariana@gmail.com',09),
	(11,'Pedro Lima',11223344556,'1997/04/30','pedro@gmail.com',06);
	
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
	(29,'Bétula Olho de Cobra',60.00,04,01),
	(30,'Cavaleiro do Abismo',80.00,05,03),
	(31,'Espectro Sombrio',45.50,05,01),
	(32,'Fênix Resplandecente',120.75,05,04),
	(33,'Guardião das Estrelas',180.00,06,02),
	(34,'Fúria Flamejante',95.99,06,02),
	(35,'Serpente Venenosa',30.50,06,01),
	(36,'Dragão do Trovão',150.00,07,04),
	(37,'Tormenta Congelante',110.25,07,04),
	(38,'Anjo da Justiça',65.80,07,01),
	(39,'Dragão de Cristal',200.00,08,02),
	(40,'Titã Colossal',250.50,08,04),
	(41,'Leviatã Aquático',120.30,08,01),
	(42,'Demônio Sombrio',70.99,09,01),
	(43,'Arcanjo Radiante',95.60,09,02),
	(44,'Dragão da Tempestade',180.99,09,04),
	(45,'Fera da Selva',40.00,09,01),
	(46,'Elemental da Terra',60.50,10,03),
	(47,'Espírito da Floresta',85.75,10,01),
	(48,'Gigante de Pedra',110.00,10,02),
	(49,'Sombra da Noite',55.25,10,04),
	(50,'Lobo Selvagem',35.80,11,01);

	
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
	(13,04,'Morte Súbita',29,04),
	(14,04,'Deck Magia',30,05),
	(15,05,'Deck Monstros',38,06),
	(16,06,'Deck Épicos',42,07),
	(17,07,'Deck Raros',45,08),
	(18,08,'Deck Lendários',50,09);
	
	INSERT INTO venda VALUES
	(01,'2023-10-31 10:00:00',05,01),
	(02,'2023-11-16 23:21:00',08,02),
	(03,'2022-09-25 15:52:00',11,02),
	(04,'2023-05-21 10:30:00',17,03),
	(05,'2023-05-20 10:30:00',18,03),
	(06,'2023-06-20 10:30:00',24,04),
	(07,'2023-07-15 14:45:00',34,06),
	(08,'2023-08-02 18:20:00',37,07),
	(09,'2023-09-10 11:10:00',41,08),
	(10,'2023-11-01 09:30:00',46,09),
	(11,'2023-11-25 16:05:00',50,09);


### 9	TABELAS E PRINCIPAIS CONSULTAS<br>

Collab: https://colab.research.google.com/drive/10ci9CFayCj2BKYTozd7JU8E9mpNHHzVw#scrollTo=_ptOT_x93l8e

#### 9.1	CONSULTAS DAS TABELAS COM TODOS OS DADOS INSERIDOS (Todas) <br>

![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/e7337ae7-c277-42a0-8ce2-fd3626f0824f)

![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/c7dcc995-e554-4af7-b01f-2f0c1b94ff0e)

![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/c9a3ef15-c74d-4202-b1c9-726ab1460dab)

![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/43eac677-7bdf-4025-90a6-b0cec7fb3085)

![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/7f15c82f-6eac-4432-95fd-fd2e01e29ada)

![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/c32823a8-0f9d-45eb-88d5-51905e0e47c7)

![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/bdc714ba-259f-49c8-bf96-2ac9fee0e21d)



#### 9.2	CONSULTAS DAS TABELAS COM FILTROS WHERE (Mínimo 4)<br>
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/9438d363-3ef2-4100-83da-e5a1b080f2bf)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/5a2f4196-6c59-4dda-8a6b-622d69e4eba4)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/ae373e53-264e-4fa6-8190-e3595d267e96)


#### 9.3	CONSULTAS QUE USAM OPERADORES LÓGICOS, ARITMÉTICOS E TABELAS OU CAMPOS RENOMEADOS (Mínimo 11)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/328f616a-f6b5-4a39-9fbb-4e5ea661e9e1)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/a435ca86-8454-41fd-ad95-67919ea02892)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/adbd184f-cefe-4e32-a694-16ca5ccf1e32)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/c2b2a797-3a46-4af9-85f1-8ef183a62c61)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/87a9c405-9951-42c3-8448-f468440752f9)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/51ce2ca1-c733-462a-9422-256e37f07022)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/c23bc14f-2a51-485d-8b12-9712ac4f9721)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/e8490bd0-c794-493c-adfc-df274e660bee)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/d9685b35-9c56-4e2f-a5ac-76cd3b1a4a31)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/76f0c758-9ded-48b4-b889-bd3667c6afca)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/26df94f0-399d-4691-ac0c-424ec430ce69)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/e6774b39-6a26-42a3-afc0-4fa489781c5b)



#### 9.4	CONSULTAS QUE USAM OPERADORES LIKE E DATAS (Mínimo 12) <br>
    a) Criar outras 5 consultas que envolvam like ou ilike
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/d4baabf4-2cf4-4ae1-8e56-43138a5d2551)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/caed4726-1ae3-4e52-b572-7e9423c424e3)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/65ba4728-f9e0-400d-a6f4-05ee2e849d06)

    b) Criar uma consulta para cada tipo de função data apresentada.
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/9dfef22a-36b6-4378-a5a8-6572b9e95d4a)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/0a8c4b28-76a2-4799-ada0-4a7acceda5fc)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/62f26f99-a4b4-43b1-8be6-8657e43592fd)

># Marco de Entrega 02: Do item 6. até o item 9.1 (5 PTS) <br>

#### 9.5	INSTRUÇÕES APLICANDO ATUALIZAÇÃO E EXCLUSÃO DE DADOS (Mínimo 6)<br>
    a) Criar minimo 3 de exclusão
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/d9816b8c-d0e6-4243-b3e3-6a8ca9e28cdf)

    b) Criar minimo 3 de atualização
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/54148d7b-bbdc-49ac-878a-be0f16bd0236)

#### 9.6	CONSULTAS COM INNER JOIN E ORDER BY (Mínimo 6)<br>
    a) Uma junção que envolva todas as tabelas possuindo no mínimo 2 registros no resultado
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/dc7cd768-0292-4a93-8370-ec5025e55c88)

    b) Outras junções que o grupo considere como sendo as de principal importância para o trabalho
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/6609fa47-c476-45bf-b94d-eb09c86559b9)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/48ed4979-7552-4e21-87a1-e4729475b305)


#### 9.7	CONSULTAS COM GROUP BY E FUNÇÕES DE AGRUPAMENTO (Mínimo 6)<br>
    a) Criar minimo 2 envolvendo algum tipo de junção
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/d04f7e09-9983-4282-83a5-f8d4f6519bc6)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/6968ec92-d786-47b1-ab5f-448b81da4211)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/18874349-6e34-40f5-a726-5d1e4ff65088)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/a99b89e9-140a-4b32-8d86-4c2152b830cf)


#### 9.8	CONSULTAS COM LEFT, RIGHT E FULL JOIN (Mínimo 4)<br>
    a) Criar minimo 1 de cada tipo
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/f8f1d5c0-ce8f-400c-bdb3-9d533ec8d79d)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/12682e14-2a1d-4b51-ab79-87453a6328e2)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/eaaf54e2-aacf-4003-9533-185a5e8cf6ba)


#### 9.9	CONSULTAS COM SELF JOIN E VIEW (Mínimo 6)<br>
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/c2844a83-b86d-4588-a9b1-4e0d1a8f13f5)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/29a85751-51b3-4f0f-aa17-ec2e26cfb347)
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/e08c70a0-e6b9-4f3a-861e-5baa98653292)


#### 9.10	SUBCONSULTAS (Mínimo 4)<br>
     a) Criar minimo 1 envolvendo GROUP BY
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/df0eb230-0056-4583-bce2-b54caffcdaa2)

     b) Criar minimo 1 envolvendo algum tipo de junção
![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/103284616/cd9320a0-1e83-44c1-a7c0-484e4f5efc14)


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


