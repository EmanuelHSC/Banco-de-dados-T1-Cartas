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

> 
O sistema de gestão proposto para jogadores de Trading Card Games (TCG) e colecionadores de cartas é uma solução completa que visa atender à necessidade que os jogadores tem de vender suas cartas e da organização de seus 'decks' que é um conjunto de cartas que pode ou não ser do mesmo tema das cartas, esse tema é de qual nicho a carta é como por ex: pokemon, magic, etc... então nosso sistema permite o jogador possa brincar com seus decks juntando cartas de pokemon com magic para poder ter por exemplo um deck de suas cartas preferidas. O sistema propões que seja possivel cadastras jogadores com as informações de nome, dt_nasc, email e onde ele reside com as informações de endereço, estado, cidade, bairro, rua, logradouro e cep, todos essas informações devem ser preenchidas pelo jogador. O jogador pode cadastrar nenhum ou varios cartões para efetuar os pagamentos, e para as vendas temos que armazenar quem vendeu, quem comprou, hora e preço, sempre que um jogador quiser vender uma carta ela deve sair do deck e ficar marcada como a venda até que a negociação seja conluida. O jogador pode cadastrar nenhuma ou varias cartas mas essa carta só pertence a um jogador por vez e os dados que devem ser cadastrados da carta são nome, preço, tema e número de colecionador que é o quão raro é a carta, quanto mais proximo de 1 mais rara ela é o range varia de 1 a 100000, e com isso podemos ter uma mesma carta que se diferencia pela sua raridade. O jogador tambem pode cadastrar decks no sistema, sendo que ele pode ter zero ou varios decks e as informações de cadastros são do deck são nome do deck que fica a escolha do jogador o nome que ele quiser,  o tema do deck e as cartas que estão nele.

### 3.PERGUNTAS A SEREM RESPONDIDAS<br>
#### 3.1 QUAIS PERGUNTAS PODEM SER RESPONDIDAS COM O SISTEMA PROPOSTO?

> A Empresa CARTAS precisa inicialmente dos seguintes relatórios:
* Relatorio que mostre qual região tem mais gente.
* Relatorio que informa quantidade de cartas vendidas por vendedor.
* Relatório que mostre quantas cartas do tipo dragão nós temos no sistema e seus respectivos preços.
* Relatório com top 5 vendas do site.
* Relatório de preço das cartas somadas das pessoas.


    
### 5.MODELO CONCEITUAL<br>


![image](https://github.com/EmanuelHSC/Banco-de-dados-T1-Cartas/assets/116691668/5f5e5a48-e921-489b-a832-89b8406d93bb)



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

	CREATE TABLE IF NOT EXISTS STATUS(
	id_status   SERIAL PRIMARY KEY,
	desc_status VARCHAR(50)
	);
	
	CREATE TABLE IF NOT EXISTS STATUS_CARTAO(
		id_status_cartao SERIAL PRIMARY KEY,
		desc_status      VARCHAR(50)
	);
	
	CREATE TABLE IF NOT EXISTS ENDERECO(
		id_end     SERIAL PRIMARY KEY,
		estado     VARCHAR(155),
		cidade 	   VARCHAR(155),
		bairro     VARCHAR(155),
		rua        VARCHAR(155),
		logradouro VARCHAR(155),
		cep        VARCHAR(8)
	);
	
	CREATE TABLE IF NOT EXISTS JOGADOR(
		id_pessoa  SERIAL PRIMARY KEY,
		nome       VARCHAR(100),
		dt_nasc    DATE,
		email      VARCHAR(100),
		id_end     INTEGER,
		FOREIGN KEY(id_end)
		REFERENCES ENDERECO(id_end)
	);
	
	CREATE TABLE IF NOT EXISTS CARTAO(
		id_cartao  SERIAL PRIMARY KEY,
		num_cartao VARCHAR(16),
		id_status  INTEGER,
		FOREIGN KEY(id_status)
		REFERENCES STATUS_CARTAO(id_status_cartao),
		cvv        VARCHAR(3),
		dt_venc    DATE,
		id_pessoa  INTEGER,
		FOREIGN KEY(id_pessoa)
		REFERENCES JOGADOR(id_pessoa)
	);
	
	CREATE TABLE IF NOT EXISTS TEMA_CARTA(
		id_tema_carta SERIAL PRIMARY KEY,
		descricao     VARCHAR(50)
	);
	
	CREATE TABLE IF NOT EXISTS TEMA_DECK(
		id_tema_deck SERIAL PRIMARY KEY,
		descricao    VARCHAR(50)
	);
	
	CREATE TABLE IF NOT EXISTS CARTA(
		id_carta         SERIAL PRIMARY KEY,
		nome_card        VARCHAR(100),
		preco            FLOAT,
		num_colecionador VARCHAR(6),
		id_tema          INTEGER,
		FOREIGN KEY(id_tema)
		REFERENCES TEMA_CARTA(id_tema_carta),
		id_pessoa        INTEGER,
		FOREIGN KEY(id_pessoa)
		REFERENCES JOGADOR(id_pessoa),
		id_status        INTEGER,
		FOREIGN KEY(id_status)
		REFERENCES STATUS(id_status)
	);
	
	CREATE TABLE IF NOT EXISTS DECK(
		cod_table SERIAL,
		id_deck   INTEGER,
		PRIMARY KEY(cod_table, id_deck),
		id_tema   INTEGER,
		FOREIGN KEY(id_tema)
		REFERENCES TEMA_DECK(id_tema_deck),
		id_carta INTEGER,
		FOREIGN KEY(id_carta)
		REFERENCES CARTA(id_carta),
		id_pessoa INTEGER,
		FOREIGN KEY(id_pessoa)
		REFERENCES JOGADOR(id_pessoa)
	);
	
	CREATE TABLE IF NOT EXISTS NOME_DECK(
		id_nome_deck INTEGER PRIMARY KEY,
		FOREIGN KEY(id_deck)
		REFERENCES  DECK(id_deck),
		descricao VARCHAR(50)
	);
	
	CREATE TABLE IF NOT EXISTS VENDA(
		id_venda SERIAL PRIMARY KEY,
		dt_venda DATE,
		preco_venda FLOAT,
		id_carta INTEGER        REFERENCES CARTA(id_carta),
		id_pessoa INTEGER       REFERENCES JOGADOR(id_pessoa),
		id_comprador INTEGER    REFERENCES JOGADOR(id_pessoa),
		id_cartao_usado INTEGER REFERENCES CARTAO(id_cartao)
	);
      
### 8	INSERT APLICADO NAS TABELAS DO BANCO DE DADOS<br>
       
	INSERT INTO STATUS(desc_status) VALUES
	   ('Em deck'),
	   ('Em venda'),
	   ('Vendido'),
	   ('Sem deck');
	
	INSERT INTO TEMA_CARTA (descricao) VALUES
	   ('Pokemon'),
	   ('Digimon'),
	   ('Magic');
	
	INSERT INTO TEMA_DECK (descricao) VALUES
	   ('Ofensivo'),
	   ('Defensivo'),
	   ('Equilibrado');
	
	INSERT INTO STATUS_CARTAO(desc_status) VALUES
	   ('Ativo'),
	   ('Inativo');
	
	INSERT INTO ENDERECO (estado, cidade, bairro, rua, logradouro, cep) VALUES
	    ('São Paulo', 'São Paulo', 'Moema', 'Avenida Ibirapuera', 'Edifício Alpha', '04029020'),
	    ('Rio de Janeiro', 'Rio de Janeiro', 'Ipanema', 'Rua Visconde de Pirajá', 'Apartamento 501', '22410002'),
	    ('Minas Gerais', 'Belo Horizonte', 'Lourdes', 'Avenida Bias Fortes', 'Casa 102', '30170010'),
	    ('Rio Grande do Sul', 'Porto Alegre', 'Moinhos de Vento', 'Rua Padre Chagas', 'Conjunto Residencial Beta', '90470150'),
	    ('Bahia', 'Salvador', 'Barra', 'Avenida Oceânica', 'Apartamento 303', '40170010'),
	    ('Ceará', 'Fortaleza', 'Meireles', 'Avenida Beira Mar', 'Casa Amarela', '60160120'),
	    ('Pernambuco', 'Recife', 'Boa Viagem', 'Rua dos Navegantes', 'Edifício Delta', '51021330'),
	    ('Paraná', 'Curitiba', 'Batel', 'Alameda Dr. Carlos de Carvalho', 'Apartamento 801', '80430180'),
	    ('Santa Catarina', 'Florianópolis', 'Centro', 'Rua Felipe Schmidt', 'Sala 1001', '88010001'),
	    ('Goiás', 'Goiânia', 'Setor Marista', 'Avenida 136', 'Casa Verde', '74180040'),
	    ('Espírito Santo', 'Vitória', 'Praia do Canto', 'Rua Aleixo Netto', 'Apartamento 1203', '29055250'),
	    ('Pará', 'Belém', 'Nazaré', 'Travessa Dom Romualdo de Seixas', 'Edifício Gamma', '66035220'),
	    ('Amazonas', 'Manaus', 'Adrianópolis', 'Rua Belo Horizonte', 'Casa Azul', '69057110'),
	    ('Alagoas', 'Maceió', 'Ponta Verde', 'Avenida Álvaro Otacílio', 'Apartamento 202', '57035180'),
	    ('Maranhão', 'São Luís', 'Renascença', 'Avenida Colares Moreira', 'Casa Rosa', '65075441'),
	    ('Mato Grosso', 'Cuiabá', 'Alvorada', 'Avenida Historiador Rubens de Mendonça', 'Casa Amarela', '78049912'),
	    ('Mato Grosso do Sul', 'Campo Grande', 'Jardim dos Estados', 'Rua da Paz', 'Apartamento 1501', '79020250'),
	    ('Amapá', 'Macapá', 'Central', 'Avenida FAB', 'Edifício Ômega', '68908876'),
	    ('Roraima', 'Boa Vista', 'Centro', 'Avenida Major Williams', 'Casa Verde', '69301030'),
	    ('Tocantins', 'Palmas', 'Plano Diretor Sul', 'Quadra 104 Sul', 'Casa 21', '77020008');
	
	INSERT INTO JOGADOR (nome, dt_nasc, email, id_end) VALUES
	    ('João Silva', '1990-05-15', 'joao.silva@email.com', 1),
	    ('Maria Oliveira', '1985-08-20', 'maria.oliveira@email.com', 2),
	    ('Pedro Santos', '1992-03-08', 'pedro.santos@email.com', 3),
	    ('Ana Costa', '1988-10-12', 'ana.costa@email.com', 4),
	    ('Lucas Pereira', '1995-12-25', 'lucas.pereira@email.com', 5),
	    ('Juliana Lima', '1980-07-30', 'juliana.lima@email.com', 6),
	    ('Fernando Souza', '1998-02-03', 'fernando.souza@email.com', 7),
	    ('Camila Martins', '1983-06-18', 'camila.martins@email.com', 8),
	    ('Rodrigo Almeida', '1991-01-05', 'rodrigo.almeida@email.com', 9),
	    ('Isabela Oliveira', '1987-06-10', 'isabela.oliveira@email.com', 10),
	    ('Gustavo Santos', '1994-12-01', 'gustavo.santos@email.com', 11),
	    ('Amanda Costa', '1982-08-22', 'amanda.costa@email.com', 12),
	    ('Carlos Pereira', '1996-06-14', 'carlos.pereira@email.com', 13),
	    ('Luiza Oliveira', '1989-09-27', 'luiza.oliveira@email.com', 14),
	    ('Rafael Lima', '1984-03-05', 'rafael.lima@email.com', 15),
	    ('Viviane Souza', '1993-07-17', 'viviane.souza@email.com', 16),
	    ('Leandro Almeida', '1981-11-08', 'leandro.almeida@email.com', 17),
	    ('Natália Martins', '1997-04-19', 'natalia.martins@email.com', 18),
	    ('Thiago Oliveira', '1986-01-02', 'thiago.oliveira@email.com', 19),
	    ('Bianca Costa', '1990-05-30', 'bianca.costa@email.com', 20),
	    ('Eduardo Oliveira', '1987-09-14', 'eduardo.oliveira@email.com', 2),
	    ('Larissa Santos', '1994-02-28', 'larissa.santos@email.com', 3),
	    ('Ricardo Pereira', '1981-07-03', 'ricardo.pereira@email.com', 4),
	    ('Fernanda Lima', '1998-11-16', 'fernanda.lima@email.com', 5),
	    ('Gabriel Costa', '1986-04-21', 'gabriel.costa@email.com', 6),
	    ('Carolina Almeida', '1992-10-08', 'carolina.almeida@email.com', 7),
	    ('Vinícius Souza', '1989-03-25', 'vinicius.souza@email.com', 8),
	    ('Isabela Martins', '1996-08-09', 'isabela.martins@email.com', 9),
	    ('Roberto Silva', '1984-12-12', 'roberto.silva@email.com', 10),
	    ('Tatiane Oliveira', '1990-06-05', 'tatiane.oliveira@email.com', 11);
	
	INSERT INTO CARTAO (num_cartao, id_status, cvv, dt_venc, id_pessoa) VALUES
	    ('1234567890123456', 1, '123', '2023-12-01', 1),
	    ('2345678901234567', 2, '456', '2024-01-15', 2),
	    ('3456789012345678', 1, '789', '2023-11-05', 3),
	    ('4567890123456789', 2, '012', '2024-02-28', 4),
	    ('5678901234567890', 1, '345', '2023-10-10', 5),
	    ('6789012345678901', 2, '678', '2024-05-20', 6),
	    ('7890123456789012', 1, '901', '2023-09-08', 7),
	    ('8901234567890123', 2, '234', '2024-04-03', 8),
	    ('9012345678901234', 1, '567', '2023-07-18', 9),
	    ('0123456789012345', 2, '890', '2024-03-12', 10),
	    ('1234567890123456', 1, '123', '2023-12-01', 11),
	    ('2345678901234567', 2, '456', '2024-01-15', 12),
	    ('9012345678901234', 1, '012', '2023-09-28', 3),
	    ('3456789012345678', 1, '789', '2023-11-05', 13),
	    ('4567890123456789', 2, '012', '2024-02-28', 14),
	    ('5678567890123456', 1, '678', '2024-06-18', 2),
	    ('5678901234567890', 1, '345', '2023-10-10', 15),
	    ('3456123456789012', 1, '567', '2023-10-01', 1),
	    ('6789012345678901', 2, '678', '2024-05-20', 16),
	    ('7890123456789012', 1, '901', '2023-09-08', 17),
	    ('8901234567890123', 2, '234', '2024-04-03', 18),
	    ('9012345678901234', 1, '567', '2023-07-18', 19),
	    ('0123456789012345', 2, '890', '2024-03-12', 20),
	    ('7890123456789012', 1, '901', '2023-12-15', 1),
	    ('7890123456789012', 2, '789', '2024-04-03', 4),
	    ('2345234567890123', 2, '345', '2024-03-05', 2),
	    ('1234567890123456', 2, '123', '2024-02-10', 3),
	    ('4567890123456789', 1, '456', '2023-11-20', 4),
	    ('2345123456789012', 1, '234', '2023-08-10', 5),
	    ('5678123456789012', 2, '567', '2024-01-23', 5);
	
	INSERT INTO CARTA (nome_card, preco, num_colecionador, id_tema, id_pessoa, id_status) VALUES
	    ('Dragão de Fogo',50.00, '045923',3,1,1),
	    ('Ressonador da Alma',150.65, '078541',3,1,1),
	    ('Casulo Vermelho',37.80, '023674',3,1,1),
	    ('Gaia Carmesim',200.00, '000054',3,4,1),
	    ('Dragão Vermelho',77.99, '000289',3,1,2),
	    ('Abrasador Dragão',64.64, '000067',3,1,1),
	    ('Comandar Ressonador',98.31, '034501',3,1,1),
	    ('Destruição do Ressonante',365.12, '007890',3,2,2),
	    ('Motor do Ressonador',99.99, '019034',3,4,4),
	    ('Rei Supremo',50.00, '067890',3,1,1),
	    ('Rei Celestial Supremo',45.98, '000731',3,2,1),
	    ('Dragão Arcray',64.65, '000012',3,4,4),
	    ('Alma do Rei',74.64, '000089',3,4,4),
	    ('Dragão Pêndulo',14.99, '034501',3,4,4),
	    ('Anciã Norden',64.30, '000015',3,1,1),
	    ('Trapezoedro Proibido',241.12, '021345',3,4,4),
	    ('Salamandra Foguete',303.63, '056780',3,2,2),
	    ('Atordoamento Sônico',65.99, '023489',3,2,2),
	    ('Canhão Alabarda',71.99, '000019',3,1,1),
	    ('Destruidor Laminado',25.12, '078935',3,1,1),
	    ('Dragão Catapulta',98.65, '004421',3,1,1),
	    ('Esqueleto de Metal',100.00, '004022',3,1,1),
	    ('Explosão Estelar',126.63, '000753',3,1,1),
	    ('Gladiador Poderoso',98.32, '000075',3,2,2),
	    ('Destruidor Laminado',65.64, '000045',3,4,4),
	    ('Visas Samsara',35.99, '001076',3,4,4),
	    ('Abscisão Mannadium',31.40, '007027',3,4,4),
	    ('Riumheart',50.00, '004028',3,4,4),
	    ('Bétula Olho de Cobra',60.00, '017029',3,1,1),
	    ('Cavaleiro do Abismo',80.00, '000030',3,3,3),
	    ('Espectro Sombrio',145.50, '000031',3,1,1),
	    ('Fênix Resplandecente',120.75, '000772',3,4,4),
	    ('Guardião das Estrelas',180.00, '001033',3,2,2),
	    ('Fúria Flamejante',95.99, '001037',3,2,2),
	    ('Serpente Venenosa',30.50, '007075',3,1,1),
	    ('Dragão do Trovão',150.00, '007106',3,4,4),
	    ('Tormenta Congelante',110.25, '000337',3,4,4),
	    ('Anjo da Justiça',65.80, '007438',3,1,1),
	    ('Dragão de Cristal',200.00, '000179',3,2,2),
	    ('Titã Colossal',250.50, '071040',3,4,4),
	    ('Leviatã Aquático',120.30, '001441',3,1,1),
	    ('Demônio Sombrio',70.99, '097802',3,1,1),
	    ('Arcanjo Radiante',95.60, '000456',3,2,2),
	    ('Dragão da Tempestade',180.99, '004564',3,4,4),
	    ('Fera da Selva',40.00, '000023',3,1,1),
	    ('Elemental da Terra',60.50, '000034',3,3,3),
	    ('Espírito da Floresta',85.75, '000567',3,1,1),
	    ('Gigante de Pedra',110.00, '000834',3,2,2),
	    ('Sombra da Noite',55.25, '003204',3,4,4),
	    ('Lobo Selvagem',35.80, '000054',3,1,1),
	    ('Lâmina do Destino', 15.0, '010001', 1, 1, 1),
	    ('Espectro Sombrio', 77.0, '010002', 3, 1, 2),
	    ('Guardião da Aurora', 25.0, '010003', 1, 1, 3),
	    ('Vórtice de Chamas', 18.0, '010004', 2, 1, 1),
	    ('Arauto da Tempestade', 22.0, '010005', 2, 1, 2),
	    ('Cavaleiro da Lua', 77.0, '010006', 2, 1, 3),
	    ('Fênix Radiante', 30.0, '010007', 1, 1, 1),
	    ('Mestre das Sombras', 35.0, '010008', 1, 1, 2),
	    ('Serpente Celestial', 40.0, '010009', 1, 1, 3),
	    ('Alquimista das Estrelas', 32.0, '010010', 2, 1, 1),
	    ('Guardiã das Flores', 12.0, '020001', 1, 2, 1),
	    ('Espírito da Floresta', 18.0, '020002', 3, 2, 2),
	    ('Luz do Crepúsculo', 24.0, '020003', 1, 2, 3),
	    ('Caçadora Noturna', 16.0, '020004', 2, 2, 1),
	    ('Dama do Lago', 20.0, '020005', 2, 2, 2),
	    ('Sombra Silenciosa', 26.0, '020006', 2, 2, 3),
	    ('Mestre da Cura', 28.0, '020007', 1, 2, 1),
	    ('Vigia das Estrelas', 32.0, '020008', 1, 2, 2),
	    ('Mago da Lua Cheia', 38.0, '020009', 1, 2, 3),
	    ('Fúria Selvagem', 30.0, '020010', 2, 2, 1),
	    ('Espadachim Relâmpago', 15.0, '030001', 1, 3, 1),
	    ('Guardião do Abismo', 20.0, '030002', 1, 3, 2),
	    ('Líder da Vanguarda', 25.0, '030003', 1, 3, 3),
	    ('Fera Selvagem', 18.0, '030004', 2, 3, 1),
	    ('Arcano Misterioso', 22.0, '030005', 2, 3, 2),
	    ('Necromante Sombrio', 28.0, '030006', 2, 3, 3),
	    ('Lutador Reluzente', 30.0, '030007', 1, 3, 1),
	    ('Mestre da Ilusão', 35.0, '030008', 1, 3, 2),
	    ('Cavaleiro da Tempestade', 40.0, '030009', 1, 3, 3),
	    ('Guardião da Fronteira', 32.0, '030010', 2, 3, 1),
	    ('Dama da Lua', 12.0, '040001', 1, 4, 1),
	    ('Caçadora Celestial', 18.0, '040002', 1, 4, 2),
	    ('Mestre das Sombras', 24.0, '040003', 1, 4, 3),
	    ('Guardiã da Noite', 16.0, '040004', 2, 4, 1),
	    ('Serpente da Escuridão', 20.0, '040005', 2, 4, 2),
	    ('Arqueira Estelar', 26.0, '040006', 2, 4, 3),
	    ('Fada Lunar', 28.0, '040007', 1, 4, 1),
	    ('Líder da Aurora', 32.0, '040008', 1, 4, 2),
	    ('Cavaleira da Alvorada', 38.0, '040009', 1, 4, 3),
	    ('Mago do Crepúsculo', 30.0, '040010', 2, 4, 1),
	    ('Fênix Alada', 15.0, '050001', 1, 5, 1),
	    ('Mago das Estrelas', 20.0, '050002', 1, 5, 2),
	    ('Guardião Celestial', 25.0, '050003', 1, 5, 3),
	    ('Caçador de Sombras', 18.0, '050004', 1, 5, 1),
	    ('Cavaleiro da Aurora', 62.0, '050005', 1, 5, 2),
	    ('Serpente de Fogo', 28.0, '050006', 2, 5, 3),
	    ('Arqueiro Sombrio', 30.0, '050007', 1, 5, 1),
	    ('Dama do Crepúsculo', 35.0, '050008', 1, 5, 2),
	    ('Líder das Sombras', 40.0, '050009', 1, 5, 3),
	    ('Guardião da Fronteira', 32.0, '050010', 2, 5, 1),
	    ('Feiticeira das Estrelas', 12.0, '060001', 1, 6, 1),
	    ('Lutador Místico', 18.0, '060002', 1, 6, 2),
	    ('Guardião da Noite', 24.0, '060003', 1, 6, 3),
	    ('Cavaleiro da Lua', 56.0, '060004', 2, 6, 1),
	    ('Arqueira da Aurora', 20.0, '060005', 2, 6, 2),
	    ('Fada Lunar', 26.0, '060006', 1, 6, 3),
	    ('Mestre do Vento', 28.0, '060007', 1, 6, 1),
	    ('Cavaleira da Tempestade', 32.0, '060008', 1, 6, 2),
	    ('Mago do Crepúsculo', 38.0, '060009', 2, 6, 3),
	    ('Sombra Silenciosa', 30.0, '060010', 2, 6, 1),
	    ('Lutador Flamejante', 15.0, '070001', 1, 7, 1),
	    ('Mago do Trovão', 20.0, '070002', 1, 7, 2),
	    ('Cavaleiro da Tempestade', 25.0, '070003', 1, 7, 3),
	    ('Feiticeira Lunar', 18.0, '070004', 2, 7, 1),
	    ('Guardião da Aurora', 22.0, '070005', 1, 7, 2),
	    ('Sombra Misteriosa', 28.0, '070006', 2, 7, 3),
	    ('Cavaleiro do Crepúsculo', 30.0, '070007', 1, 7, 1),
	    ('Mestre das Sombras', 35.0, '070008', 1, 7, 2),
	    ('Espectro Noturno', 40.0, '070009', 1, 7, 3),
	    ('Guardião da Fronteira', 32.0, '070010', 2, 7, 1),
	    ('Fada Estelar', 35.0, '080001', 2, 8, 1),
	    ('Lutador da Noite', 18.0, '080002', 1, 8, 2),
	    ('Mago das Sombras', 24.0, '080003', 1, 8, 3),
	    ('Guardião do Crepúsculo', 16.0, '080004', 2, 8, 1),
	    ('Caçador Celestial', 20.0, '080005', 2, 8, 2),
	    ('Cavaleiro da Lua', 26.0, '080006', 2, 8, 3),
	    ('Sombra Sutil', 28.0, '080007', 1, 8, 1),
	    ('Arqueira Noturna', 32.0, '080008', 1, 8, 2),
	    ('Líder das Estrelas', 38.0, '080009', 1, 8, 3),
	    ('Fera Selvagem', 30.0, '080010', 2, 8, 1),
	    ('Cavaleiro da Aurora', 36.0, '090001', 1, 9, 1),
	    ('Mago do Trovão', 20.0, '090002', 1, 9, 2),
	    ('Guardião das Sombras', 25.0, '090003', 1, 9, 3),
	    ('Sombra Misteriosa', 18.0, '090004', 2, 9, 1),
	    ('Fada Estelar', 26.0, '090005', 2, 9, 2),
	    ('Líder da Fronteira', 28.0, '090006', 2, 9, 3),
	    ('Lutador Flamejante', 30.0, '90007', 1, 9, 1),
	    ('Espectro Noturno', 17.0, '090008', 1, 9, 2),
	    ('Mestre das Trevas', 40.0, '090009', 1, 9, 3),
	    ('Guardião Celestial', 32.0, '090010', 1, 9, 1),
	    ('Sombra Sutil', 12.0, '010401', 1, 10, 1),
	    ('Arqueira Noturna', 18.0, '000002', 1, 10, 2),
	    ('Líder das Estrelas', 24.0, '000003', 1, 10, 3),
	    ('Fera Selvagem', 16.0, '000004', 2, 10, 1),
	    ('Lutador da Noite', 20.0, '000005', 1, 10, 2),
	    ('Mago das Sombras', 26.0, '000006', 1, 10, 3),
	    ('Guardião do Crepúsculo', 28.0, '000007', 2, 10, 1),
	    ('Caçador Celestial', 32.0, '000008', 2, 10, 2),
	    ('Cavaleiro da Lua', 106.56, '000009', 2, 10, 3),
	    ('Sombra Sutil', 30.0, '000010', 1, 10, 1),
	    ('Guardião da Fronteira', 15.0, '010001', 2, 11, 1),
	    ('Fada Estelar', 120.0, '010002', 2, 11, 2),
	    ('Mago do Trovão', 25.0, '010003', 1, 11, 3),
	    ('Lutador Flamejante', 18.0, '010004', 1, 11, 1),
	    ('Espectro Noturno', 63.0, '010005', 1, 11, 2),
	    ('Guardião Celestial', 28.0, '010006', 1, 11, 3),
	    ('Sombra Sutil', 30.0, '010007', 1, 11, 1),
	    ('Líder das Estrelas', 35.0, '010008', 1, 11, 2),
	    ('Fera Selvagem', 40.0, '010009', 2, 11, 3),
	    ('Cavaleiro da Aurora', 116.0, '010010', 1, 11, 1),
	    ('Mestre das Trevas', 12.0, '020001', 1, 12, 1),
	    ('Guardião Celestial', 18.0, '020002', 1, 12, 2),
	    ('Lutador da Noite', 24.0, '020003', 1, 12, 3),
	    ('Mago das Sombras', 16.0, '020004', 1, 12, 1),
	    ('Sombra Sutil', 20.0, '020005', 1, 12, 2),
	    ('Arqueira Noturna', 26.0, '020006', 1, 12, 3),
	    ('Líder das Estrelas', 28.0, '020007', 1, 12, 1),
	    ('Fera Selvagem', 32.0, '020008', 2, 12, 2),
	    ('Lutador Flamejante', 38.0, '020009', 1, 12, 3),
	    ('Guardião da Fronteira', 30.0, '020010', 2, 12, 1),
	    ('Cavaleiro da Aurora', 95.0, '030001', 1, 13, 1),
	    ('Mago do Trovão', 20.0, '030002', 1, 13, 2),
	    ('Guardião das Sombras', 25.0, '030003', 1, 13, 3),
	    ('Sombra Misteriosa', 18.0, '030004', 2, 13, 1),
	    ('Fada Estelar', 86.0, '030005', 2, 13, 2),
	    ('Líder da Fronteira', 28.0, '030006', 2, 13, 3),
	    ('Lutador Flamejante', 30.0, '030007', 1, 13, 1),
	    ('Espectro Noturno', 46.0, '030008', 1, 13, 2),
	    ('Mestre das Trevas', 40.0, '030009', 1, 13, 3),
	    ('Guardião Celestial', 32.0, '030010', 1, 13, 1),
	    ('Fera Selvagem', 12.0, '040001', 2, 14, 1),
	    ('Lutador da Noite', 18.0, '040002', 1, 14, 2),
	    ('Mago das Sombras', 24.0, '040003', 1, 14, 3),
	    ('Guardião do Crepúsculo', 16.0, '040004', 2, 14, 1),
	    ('Caçador Celestial', 20.0, '040005', 2, 14, 2),
	    ('Cavaleiro da Lua', 61.0, '040006', 2, 14, 3),
	    ('Sombra Sutil', 28.0, '040007', 1, 14, 1),
	    ('Arqueira Noturna', 32.0, '040008', 1, 14, 2),
	    ('Líder das Estrelas', 38.0, '040009', 1, 14, 3),
	    ('Fera Selvagem', 30.0, '040010', 2, 14, 1),
	    ('Cavaleiro da Aurora', 71.0, '050001', 1, 15, 1),
	    ('Mago do Trovão', 20.0, '050002', 1, 15, 2),
	    ('Guardião das Sombras', 25.0, '050003', 1, 15, 3),
	    ('Sombra Misteriosa', 18.0, '050004', 2, 15, 1),
	    ('Fada Estelar', 62.0, '050005', 2, 15, 2),
	    ('Líder da Fronteira', 28.0, '050006', 2, 15, 3),
	    ('Lutador Flamejante', 30.0, '050007', 1, 15, 1),
	    ('Espectro Noturno', 33.0, '050008', 1, 15, 2),
	    ('Mestre das Trevas', 40.0, '050009', 1, 15, 3),
	    ('Guardião Celestial', 32.0, '050010', 1, 15, 1),
	    ('Fera Selvagem', 12.0, '060001', 2, 16, 1),
	    ('Lutador da Noite', 18.0, '060002', 1, 16, 2),
	    ('Mago das Sombras', 24.0, '060003', 1, 16, 3),
	    ('Guardião do Crepúsculo', 16.0, '060004', 2, 16, 1),
	    ('Caçador Celestial', 20.0, '060005', 2, 16, 2),
	    ('Cavaleiro da Lua', 51.0, '060006', 2, 16, 3),
	    ('Sombra Sutil', 28.0, '060007', 1, 16, 1),
	    ('Arqueira Noturna', 32.0, '060008', 1, 16, 2),
	    ('Líder das Estrelas', 38.0, '060009', 1, 16, 3),
	    ('Fera Selvagem', 30.0, '060010', 2, 16, 1),
	    ('Cavaleiro da Aurora', 53.0, '070001', 1, 17, 1),
	    ('Mago do Trovão', 20.0, '070002', 1, 17, 2),
	    ('Guardião das Sombras', 25.0, '070003', 1, 17, 3),
	    ('Sombra Misteriosa', 18.0, '070004', 2, 17, 1),
	    ('Fada Estelar', 43.0, '070005', 2, 17, 2),
	    ('Líder da Fronteira', 28.0, '070006', 2, 17, 3),
	    ('Lutador Flamejante', 30.0, '070007', 1, 17, 1),
	    ('Espectro Noturno', 27.35, '070008', 1, 17, 2),
	    ('Mestre das Trevas', 40.0, '070009', 1, 17, 3),
	    ('Guardião Celestial', 32.0, '070010', 1, 17, 1),
	    ('Fera Selvagem', 12.0, '080001', 2, 18, 1),
	    ('Lutador da Noite', 18.0, '080002', 1, 18, 2),
	    ('Mago das Sombras', 24.0, '080003', 1, 18, 3),
	    ('Guardião do Crepúsculo', 16.0, '080004', 2, 18, 1),
	    ('Caçador Celestial', 20.0, '080005', 2, 18, 2),
	    ('Cavaleiro da Lua', 26.0, '080006', 2, 18, 3),
	    ('Sombra Sutil', 28.0, '080007', 1, 18, 1),
	    ('Arqueira Noturna', 32.0, '080008', 1, 18, 2),
	    ('Líder das Estrelas', 38.0, '080009', 1, 18, 3),
	    ('Fera Selvagem', 30.0, '080010', 2, 18, 1),
	    ('Cavaleiro da Aurora', 36.0, '090001', 1, 19, 1),
	    ('Mago do Trovão', 20.0, '090002', 1, 19, 2),
	    ('Guardião das Sombras', 25.0, '090003', 1, 19, 3),
	    ('Sombra Misteriosa', 18.0, '090004', 2, 19, 1),
	    ('Fada Estelar', 26.0, '090005', 2, 19, 2),
	    ('Líder da Fronteira', 28.0, '090006', 2, 19, 3),
	    ('Lutador Flamejante', 30.0, '090007', 1, 19, 1),
	    ('Espectro Noturno', 17.0, '090008', 1, 19, 2),
	    ('Mestre das Trevas', 40.0, '090009', 1, 19, 3),
	    ('Guardião Celestial', 32.0, '090010', 1, 19, 1),
	    ('Fera Selvagem', 12.0, '003001', 2, 20, 1),
	    ('Lutador da Noite', 18.0, '032002', 1, 20, 2),
	    ('Mago das Sombras', 24.0, '030003', 1, 20, 3),
	    ('Guardião do Crepúsculo', 16.0, '002004', 2, 20, 1),
	    ('Caçador Celestial', 20.0, '002005', 2, 20, 2),
	    ('Cavaleiro da Lua', 88.0, '005206', 2, 20, 3),
	    ('Sombra Sutil', 28.0, '005107', 1, 20, 1),
	    ('Arqueira Noturna', 32.0, '000023', 1, 20, 2),
	    ('Líder das Estrelas', 38.0, '000015', 1, 20, 3),
	    ('Fera Selvagem', 30.0, '003213', 2, 20, 1),
	    ('Espada Reluzente', 95.0, '001011', 2, 1, 1),
	    ('Lutador Sombrio', 30.0, '001012', 1, 1, 2),
	    ('Mago Elemental', 40.0, '001013', 1, 1, 3),
	    ('Líder da Tempestade', 35.0, '001014', 2, 1, 1),
	    ('Fada da Floresta', 77.0, '001015', 1, 1, 2),
	    ('Guardião da Luz', 28.0, '001016', 1, 1, 3),
	    ('Caçador de Sombras', 145.0, '001017', 1, 1, 1),
	    ('Sombra Veloz', 18.0, '001018', 2, 1, 2),
	    ('Fênix Flamejante', 100.0, '001019', 1, 1, 3),
	    ('Espectro Gélido', 32.0, '001020', 2, 1, 1),
	    ('Guardião da Fronteira', 15.0, '001021', 2, 1, 2),
	    ('Líder do Abismo', 38.0, '001022', 2, 1, 3),
	    ('Cavaleiro Celestial', 128.0, '001023', 2, 1, 1),
	    ('Fera do Trovão', 42.0, '001024', 2, 1, 2),
	    ('Lutador da Aurora', 33.0, '001025', 1, 1, 3),
	    ('Guardião da Fronteira', 15.0, '002011', 2, 2, 1),
	    ('Lutador da Aurora', 33.0, '002012', 1, 2, 2),
	    ('Fera do Trovão', 42.0, '002013', 2, 2, 3),
	    ('Cavaleiro Celestial', 102.0, '002014', 2, 2, 1),
	    ('Líder do Abismo', 38.0, '002015', 2, 2, 2),
	    ('Guardião da Luz', 28.0, '002016', 1, 2, 3),
	    ('Caçador de Sombras', 110.0, '002017', 1, 2, 1),
	    ('Sombra Veloz', 18.0, '002018', 2, 2, 2),
	    ('Fênix Flamejante', 90.0, '002019', 1, 2, 3),
	    ('Espada Reluzente', 85.0, '002020', 2, 2, 1),
	    ('Lutador Sombrio', 30.0, '002021', 1, 2, 2),
	    ('Mago Elemental', 40.0, '002022', 1, 2, 3),
	    ('Líder da Tempestade', 35.0, '002023', 2, 2, 1),
	    ('Fada da Floresta', 63.0, '002024', 1, 2, 2),
	    ('Guardião da Luz', 28.0, '002025', 1, 2, 3),
	    ('Guardião da Fronteira', 15.0, '003011', 2, 3, 1),
	    ('Lutador da Aurora', 33.0, '003012', 1, 3, 2),
	    ('Fera do Trovão', 42.0, '003013', 2, 3, 3),
	    ('Cavaleiro Celestial', 93.0, '003014', 2, 3, 1),
	    ('Líder do Abismo', 38.0, '003015', 2, 3, 2),
	    ('Guardião da Luz', 28.0, '003016', 1, 3, 3),
	    ('Caçador de Sombras', 95.0, '003017', 1, 3, 1),
	    ('Sombra Veloz', 18.0, '003018', 2, 3, 2),
	    ('Fênix Flamejante', 80.0, '003019', 1, 3, 3),
	    ('Espada Reluzente', 75.0, '003020', 2, 3, 1),
	    ('Lutador Sombrio', 30.0, '003021', 1, 3, 2),
	    ('Mago Elemental', 40.0, '003022', 1, 3, 3),
	    ('Líder da Tempestade', 35.0, '003023', 2, 3, 1),
	    ('Fada da Floresta', 54.0, '003024', 1, 3, 2),
	    ('Guardião da Luz', 28.0, '003025', 1, 3, 3),
	    ('Fênix Flamejante', 70.0, '004011', 1, 4, 1),
	    ('Espada Reluzente', 65.0, '004012', 2, 4, 2),
	    ('Lutador Sombrio', 30.0, '004013', 1, 4, 3),
	    ('Mago Elemental', 40.0, '004014', 1, 4, 1),
	    ('Líder da Tempestade', 35.0, '004015', 2, 4, 2),
	    ('Fada da Floresta', 43.0, '004016', 1, 4, 3),
	    ('Guardião da Luz', 28.0, '004017', 1, 4, 1),
	    ('Caçador de Sombras', 79.0, '004018', 1, 4, 2),
	    ('Sombra Veloz', 18.0, '004019', 2, 4, 3),
	    ('Cavaleiro Celestial', 83.0, '004020', 2, 4, 1),
	    ('Líder do Abismo', 38.0, '004021', 2, 4, 2),
	    ('Guardião da Fronteira', 15.0, '004022', 2, 4, 3),
	    ('Lutador da Aurora', 33.0, '004023', 1, 4, 1),
	    ('Fera do Trovão', 42.0, '004024', 2, 4, 2),
	    ('Cavaleiro Celestial', 80.0, '004025', 2, 4, 3),
	    ('Lutador Sombrio', 30.0, '005011', 1, 5, 1),
	    ('Líder da Tempestade', 35.0, '005012', 2, 5, 2),
	    ('Fada da Floresta', 32.0, '005013', 1, 5, 3),
	    ('Guardião da Luz', 28.0, '005014', 1, 5, 1),
	    ('Caçador de Sombras', 64.0, '005015', 1, 5, 2),
	    ('Sombra Veloz', 18.0, '005016', 2, 5, 3),
	    ('Fênix Flamejante', 80.0, '005017', 1, 5, 1),
	    ('Espada Reluzente', 55.0, '005018', 2, 5, 2),
	    ('Lutador da Aurora', 33.0, '005019', 1, 5, 3),
	    ('Mago Elemental', 40.0, '005020', 1, 5, 1),
	    ('Líder do Abismo', 38.0, '005021', 2, 5, 2),
	    ('Guardião da Fronteira', 15.0, '005022', 2, 5, 3),
	    ('Fera do Trovão', 42.0, '005023', 2, 5, 1),
	    ('Cavaleiro Celestial', 71.0, '005024', 2, 5, 2),
	    ('Mago Elemental', 40.0, '005025', 1, 5, 3),
	    ('Fada da Floresta', 22.0, '006011', 1, 6, 1),
	    ('Guardião da Luz', 28.0, '006012', 1, 6, 2),
	    ('Caçador de Sombras', 56.0, '006013', 1, 6, 3),
	    ('Sombra Veloz', 18.0, '006014', 2, 6, 1),
	    ('Fênix Flamejante', 50.0, '006015', 1, 6, 2),
	    ('Espada Reluzente', 35.0, '006016', 2, 6, 3),
	    ('Lutador Sombrio', 30.0, '006017', 1, 6, 1),
	    ('Líder da Tempestade', 35.0, '006018', 2, 6, 2),
	    ('Fada da Floresta', 20.75, '006019', 1, 6, 3),
	    ('Guardião da Luz', 28.0, '006020', 1, 6, 1),
	    ('Caçador de Sombras', 45.0, '006021', 1, 6, 2),
	    ('Sombra Veloz', 18.0, '006022', 2, 6, 3),
	    ('Fênix Flamejante', 50.0, '006023', 1, 6, 1),
	    ('Espada Reluzente', 25.0, '006024', 2, 6, 2),
	    ('Lutador da Aurora', 33.0, '006025', 1, 6, 3),
	    ('Lâmina da Tempestade', 30.0, '007011', 1, 7, 1),
	    ('Mago das Ilusões', 40.0, '007012', 2, 7, 2),
	    ('Fera das Sombras', 25.0, '007013', 1, 7, 3),
	    ('Guardião do Vento', 35.0, '007014', 2, 7, 1),
	    ('Lutador do Trovão', 45.0, '007015', 1, 7, 2),
	    ('Fada do Crepúsculo', 63.0, '007016', 2, 7, 3),
	    ('Caçador Celestial', 48.0, '007017', 2, 7, 1),
	    ('Sombra Veloz', 18.0, '007018', 2, 7, 2),
	    ('Líder da Noite', 38.0, '007019', 1, 7, 3),
	    ('Cavaleiro das Estrelas', 89.0, '007020', 1, 7, 1),
	    ('Guardião da Luz', 32.0, '007021', 1, 7, 2),
	    ('Lutador Alado', 40.0, '007022', 2, 7, 3),
	    ('Espada Divina', 125.0, '007023', 3, 7, 1),
	    ('Fênix Flamejante', 50.0, '007024', 1, 7, 2),
	    ('Líder do Abismo', 35.0, '007025', 2, 7, 3),
	    ('Sombra Veloz', 18.0, '008011', 2, 8, 1),
	    ('Líder da Noite', 38.0, '008012', 1, 8, 2),
	    ('Cavaleiro das Estrelas', 71.0, '008013', 1, 8, 3),
	    ('Guardião da Luz', 32.0, '008014', 1, 8, 1),
	    ('Lutador Alado', 40.0, '008015', 2, 8, 2),
	    ('Espada Divina', 85.0, '008016', 3, 8, 3),
	    ('Fênix Flamejante', 50.0, '008017', 1, 8, 1),
	    ('Líder do Abismo', 35.0, '008018', 2, 8, 2),
	    ('Lâmina da Tempestade', 30.0, '008019', 1, 8, 3),
	    ('Mago das Ilusões', 40.0, '008020', 2, 8, 1),
	    ('Fera das Sombras', 25.0, '008021', 1, 8, 2),
	    ('Guardião do Vento', 35.0, '008022', 2, 8, 3),
	    ('Lutador do Trovão', 45.0, '008023', 1, 8, 1),
	    ('Fada do Crepúsculo', 52.0, '008024', 2, 8, 2),
	    ('Caçador Celestial', 48.0, '008025', 2, 8, 3),
	    ('Líder da Noite', 38.0, '009011', 1, 9, 1),
	    ('Cavaleiro das Estrelas', 62.0, '009012', 1, 9, 2),
	    ('Guardião da Luz', 32.0, '009013', 1, 9, 3),
	    ('Lutador Alado', 40.0, '009014', 2, 9, 1),
	    ('Espada Divina', 65.0, '009015', 3, 9, 2),
	    ('Fênix Flamejante', 50.0, '009016', 1, 9, 3),
	    ('Líder do Abismo', 35.0, '009017', 2, 9, 1),
	    ('Lâmina da Tempestade', 30.0, '009018', 1, 9, 2),
	    ('Mago das Ilusões', 40.0, '009019', 2, 9, 3),
	    ('Fera das Sombras', 25.0, '009020', 1, 9, 1),
	    ('Guardião do Vento', 35.0, '009021', 2, 9, 2),
	    ('Lutador do Trovão', 45.0, '009022', 1, 9, 3),
	    ('Fada do Crepúsculo', 42.0, '009023', 2, 9, 1),
	    ('Caçador Celestial', 48.0, '009024', 2, 9, 2),
	    ('Sombra Veloz', 18.0, '009025', 2, 9, 3),
	    ('Fera das Sombras', 25.0, '010011', 1, 10, 1),
	    ('Guardião do Vento', 35.0, '010012', 2, 10, 2),
	    ('Lutador do Trovão', 45.0, '010013', 1, 10, 3),
	    ('Fada do Crepúsculo', 36.0, '010014', 2, 10, 1),
	    ('Caçador Celestial', 48.0, '010015', 2, 10, 2),
	    ('Sombra Veloz', 18.0, '010016', 2, 10, 3),
	    ('Líder da Noite', 38.0, '010017', 1, 10, 1),
	    ('Cavaleiro das Estrelas', 49.0, '010018', 1, 10, 2),
	    ('Guardião da Luz', 32.0, '010019', 1, 10, 3),
	    ('Lutador Alado', 40.0, '010020', 2, 10, 1),
	    ('Espada Divina', 55.0, '010021', 3, 10, 2),
	    ('Fênix Flamejante', 50.0, '010022', 1, 10, 3),
	    ('Líder do Abismo', 35.0, '010023', 2, 10, 1),
	    ('Lâmina da Tempestade', 30.0, '010024', 1, 10, 2),
	    ('Mago das Ilusões', 40.0, '010025', 2, 10, 3),
	    ('Guardião do Vento', 35.0, '011011', 2, 11, 1),
	    ('Lutador do Trovão', 45.0, '011012', 1, 11, 2),
	    ('Fada do Crepúsculo', 24.75, '011013', 2, 11, 3),
	    ('Caçador Celestial', 48.0, '011014', 2, 11, 1),
	    ('Sombra Veloz', 18.0, '011015', 2, 11, 2),
	    ('Líder da Noite', 38.0, '011016', 1, 11, 3),
	    ('Cavaleiro das Estrelas', 47.0, '011017', 1, 11, 1),
	    ('Guardião da Luz', 32.0, '011018', 1, 11, 2),
	    ('Lutador Alado', 40.0, '011019', 2, 11, 3),
	    ('Espada Divina', 45.0, '011020', 3, 11, 1),
	    ('Fênix Flamejante', 50.0, '011021', 1, 11, 2),
	    ('Líder do Abismo', 35.0, '011022', 2, 11, 3),
	    ('Lâmina da Tempestade', 30.0, '011023', 1, 11, 1),
	    ('Mago das Ilusões', 40.0, '011024', 2, 11, 2),
	    ('Fera das Sombras', 25.0, '011025', 1, 11, 3),
	    ('Líder da Noite', 38.0, '012011', 1, 12, 1),
	    ('Cavaleiro das Estrelas', 43.0, '012012', 1, 12, 2),
	    ('Guardião da Luz', 32.0, '012013', 1, 12, 3),
	    ('Lutador Alado', 40.0, '012014', 2, 12, 1),
	    ('Espada Divina', 35.0, '012015', 3, 12, 2),
	    ('Fênix Flamejante', 50.0, '012016', 1, 12, 3),
	    ('Líder do Abismo', 35.0, '012017', 2, 12, 1),
	    ('Lâmina da Tempestade', 30.0, '012018', 1, 12, 2),
	    ('Mago das Ilusões', 40.0, '012019', 2, 12, 3),
	    ('Fera das Sombras', 25.0, '012020', 1, 12, 1),
	    ('Guardião do Vento', 35.0, '012021', 2, 12, 2),
	    ('Lutador do Trovão', 45.0, '012022', 1, 12, 3),
	    ('Fada do Crepúsculo', 22.03, '012023', 2, 12, 1),
	    ('Caçador Celestial', 48.0, '012024', 2, 12, 2),
	    ('Sombra Veloz', 18.0, '012025', 2, 12, 3),
	    ('Guardião do Vento', 35.0, '013011', 2, 13, 1),
	    ('Lutador do Trovão', 45.0, '013012', 1, 13, 2),
	    ('Fada do Crepúsculo', 21.50, '013013', 2, 13, 3),
	    ('Caçador Celestial', 48.0, '013014', 2, 13, 1),
	    ('Sombra Veloz', 18.0, '013015', 2, 13, 2),
	    ('Líder da Noite', 38.0, '013016', 1, 13, 3),
	    ('Cavaleiro das Estrelas', 39.0, '013017', 1, 13, 1),
	    ('Guardião da Luz', 32.0, '013018', 1, 13, 2),
	    ('Lutador Alado', 40.0, '013019', 2, 13, 3),
	    ('Espada Divina', 30.50, '013020', 3, 13, 1),
	    ('Fênix Flamejante', 50.0, '013021', 1, 13, 2),
	    ('Líder do Abismo', 35.0, '013022', 2, 13, 3),
	    ('Lâmina da Tempestade', 30.0, '013023', 1, 13, 1),
	    ('Mago das Ilusões', 40.0, '013024', 2, 13, 2),
	    ('Fera das Sombras', 25.0, '013025', 1, 13, 3),
	    ('Espada Divina', 25.0, '014011', 3, 14, 1),
	    ('Fênix Flamejante', 50.0, '014012', 1, 14, 2),
	    ('Líder do Abismo', 35.0, '014013', 2, 14, 3),
	    ('Lâmina da Tempestade', 30.0, '014014', 1, 14, 1),
	    ('Mago das Ilusões', 40.0, '014015', 2, 14, 2),
	    ('Fera das Sombras', 25.0, '014016', 1, 14, 3),
	    ('Guardião do Vento', 35.0, '014017', 2, 14, 1),
	    ('Lutador do Trovão', 45.0, '014018', 1, 14, 2),
	    ('Fada do Crepúsculo', 19.75, '014019', 2, 14, 3),
	    ('Caçador Celestial', 48.0, '014020', 2, 14, 1),
	    ('Sombra Veloz', 18.0, '014021', 2, 14, 2),
	    ('Líder da Noite', 38.0, '014022', 1, 14, 3),
	    ('Cavaleiro das Estrelas', 35.0, '014023', 1, 14, 1),
	    ('Guardião da Luz', 32.0, '014024', 1, 14, 2),
	    ('Lutador Alado', 40.0, '014025', 2, 14, 3),
	    ('Líder do Abismo', 35.0, '015011', 2, 15, 1),
	    ('Lâmina da Tempestade', 30.0, '015012', 1, 15, 2),
	    ('Mago das Ilusões', 40.0, '015013', 2, 15, 3),
	    ('Fera das Sombras', 25.0, '015014', 1, 15, 1),
	    ('Guardião do Vento', 35.0, '015015', 2, 15, 2),
	    ('Lutador do Trovão', 45.0, '015016', 1, 15, 3),
	    ('Fada do Crepúsculo', 17.5, '015017', 2, 15, 1),
	    ('Caçador Celestial', 48.0, '015018', 2, 15, 2),
	    ('Sombra Veloz', 18.0, '015019', 2, 15, 3),
	    ('Líder da Noite', 38.0, '015020', 1, 15, 1),
	    ('Cavaleiro das Estrelas', 31.0, '015021', 1, 15, 2),
	    ('Guardião da Luz', 32.0, '015022', 1, 15, 3),
	    ('Lutador Alado', 40.0, '015023', 2, 15, 1),
	    ('Espada Divina', 23.75, '015024', 3, 15, 2),
	    ('Fênix Flamejante', 50.0, '015025', 1, 15, 3),
	    ('Caçador Celestial', 48.0, '016011', 2, 16, 1),
	    ('Sombra Veloz', 18.0, '016012', 2, 16, 2),
	    ('Líder da Noite', 38.0, '016013', 1, 16, 3),
	    ('Cavaleiro das Estrelas', 29.0, '016014', 1, 16, 1),
	    ('Guardião da Luz', 32.0, '016015', 1, 16, 2),
	    ('Lutador Alado', 40.0, '016016', 2, 16, 3),
	    ('Fada do Crepúsculo', 15.0, '016017', 2, 16, 1),
	    ('Caçador Celestial', 48.0, '016018', 2, 16, 2),
	    ('Líder do Abismo', 35.0, '016019', 2, 16, 3),
	    ('Lâmina da Tempestade', 30.0, '016020', 1, 16, 1),
	    ('Mago das Ilusões', 40.0, '016021', 2, 16, 2),
	    ('Fera das Sombras', 25.0, '016022', 1, 16, 3),
	    ('Guardião do Vento', 35.0, '016023', 2, 16, 1),
	    ('Lutador do Trovão', 45.0, '016024', 1, 16, 2),
	    ('Fada do Crepúsculo', 14.25, '016025', 2, 16, 3),
	    ('Fênix Flamejante', 50.0, '017011', 1, 17, 1),
	    ('Líder do Abismo', 35.0, '017012', 2, 17, 2),
	    ('Lâmina da Tempestade', 30.0, '017013', 1, 17, 3),
	    ('Mago das Ilusões', 40.0, '017014', 2, 17, 1),
	    ('Fera das Sombras', 25.0, '017015', 1, 17, 2),
	    ('Guardião do Vento', 35.0, '017016', 2, 17, 3),
	    ('Lutador do Trovão', 45.0, '017017', 1, 17, 1),
	    ('Fada do Crepúsculo', 12.12, '017018', 2, 17, 2),
	    ('Caçador Celestial', 48.0, '017019', 2, 17, 3),
	    ('Sombra Veloz', 18.0, '017020', 2, 17, 1),
	    ('Líder da Noite', 38.0, '017021', 1, 17, 2),
	    ('Cavaleiro das Estrelas', 23.0, '017022', 1, 17, 3),
	    ('Guardião da Luz', 32.0, '017023', 1, 17, 1),
	    ('Lutador Alado', 40.0, '017024', 2, 17, 2),
	    ('Espada Divina', 20.35, '017025', 3, 17, 3),
	    ('Lâmina da Tempestade', 30.0, '018011', 1, 18, 1),
	    ('Mago das Ilusões', 40.0, '018012', 2, 18, 2),
	    ('Fera das Sombras', 25.0, '018013', 1, 18, 3),
	    ('Guardião do Vento', 35.0, '018014', 2, 18, 1),
	    ('Lutador do Trovão', 45.0, '018015', 1, 18, 2),
	    ('Fada do Crepúsculo', 11.5, '018016', 2, 18, 3),
	    ('Caçador Celestial', 48.0, '018017', 2, 18, 1),
	    ('Sombra Veloz', 18.0, '018018', 2, 18, 2),
	    ('Líder da Noite', 38.0, '018019', 1, 18, 3),
	    ('Cavaleiro das Estrelas', 19.0, '018020', 1, 18, 1),
	    ('Guardião da Luz', 32.0, '018021', 1, 18, 2),
	    ('Lutador Alado', 40.0, '018022', 2, 18, 3),
	    ('Espada Divina', 19.25, '018023', 3, 18, 1),
	    ('Fênix Flamejante', 50.0, '018024', 1, 18, 2),
	    ('Líder do Abismo', 35.0, '018025', 2, 18, 3),
	    ('Guardião do Vento', 35.0, '019011', 2, 19, 1),
	    ('Lutador do Trovão', 45.0, '019012', 1, 19, 2),
	    ('Fada do Crepúsculo', 9.15, '019013', 2, 19, 3),
	    ('Caçador Celestial', 48.0, '019014', 2, 19, 1),
	    ('Sombra Veloz', 18.0, '019015', 2, 19, 2),
	    ('Líder da Noite', 38.0, '019016', 1, 19, 3),
	    ('Cavaleiro das Estrelas', 15.0, '019017', 1, 19, 1),
	    ('Guardião da Luz', 32.0, '019018', 1, 19, 2),
	    ('Lutador Alado', 40.0, '019019', 2, 19, 3),
	    ('Espada Divina', 17.0, '019020', 3, 19, 1),
	    ('Fênix Flamejante', 50.0, '019021', 1, 19, 2),
	    ('Líder do Abismo', 35.0, '019022', 2, 19, 3),
	    ('Lâmina da Tempestade', 30.0, '019023', 1, 19, 1),
	    ('Mago das Ilusões', 40.0, '019024', 2, 19, 2),
	    ('Fera das Sombras', 25.0, '019025', 1, 19, 3),
	    ('Fada do Crepúsculo', 7.5, '020011', 2, 20, 1),
	    ('Caçador Celestial', 48.0, '020012', 2, 20, 2),
	    ('Sombra Veloz', 18.0, '020013', 2, 20, 3),
	    ('Líder da Noite', 38.0, '020014', 1, 20, 1),
	    ('Cavaleiro das Estrelas', 13.5, '020015', 1, 20, 2),
	    ('Guardião da Luz', 32.0, '020016', 1, 20, 3),
	    ('Lutador Alado', 40.0, '020017', 2, 20, 1),
	    ('Espada Divina', 13.75, '020018', 3, 20, 2),
	    ('Fênix Flamejante', 50.0, '020019', 1, 20, 3),
	    ('Líder do Abismo', 35.0, '020020', 2, 20, 1),
	    ('Lâmina da Tempestade', 30.0, '020021', 1, 20, 2),
	    ('Mago das Ilusões', 40.0, '020022', 2, 20, 3),
	    ('Fera das Sombras', 25.0, '020023', 1, 20, 1),
	    ('Guardião do Vento', 35.0, '020024', 2, 20, 2),
	    ('Lutador do Trovão', 45.0, '020025', 1, 20, 3);


### 9	TABELAS E PRINCIPAIS CONSULTAS<br>

Collab: https://colab.research.google.com/drive/10ci9CFayCj2BKYTozd7JU8E9mpNHHzVw#scrollTo=_ptOT_x93l8e

#### 9.1	CONSULTAS DAS TABELAS COM TODOS OS DADOS INSERIDOS (Todas) <br>


#### 9.2	CONSULTAS DAS TABELAS COM FILTROS WHERE (Mínimo 4)<br>


#### 9.3	CONSULTAS QUE USAM OPERADORES LÓGICOS, ARITMÉTICOS E TABELAS OU CAMPOS RENOMEADOS (Mínimo 11) <br>
	a) Criar 5 consultas que envolvam os operadores lógicos AND, OR e Not
	b) Criar no mínimo 3 consultas com operadores aritméticos 
	c) Criar no mínimo 3 consultas com operação de renomear nomes de campos ou tabelas

#### 9.4	CONSULTAS QUE USAM OPERADORES LIKE E DATAS (Mínimo 12) <br>
    a) Criar outras 5 consultas que envolvam like ou ilike

    b) Criar uma consulta para cada tipo de função data apresentada.


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


