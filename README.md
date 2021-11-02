# DESAFIO DIO SCRIPTS DATA BASE STARWARS

## nesse desafio temos que entregar os script para criação do banco de dados de um gerenciador de naves do starwars pelo própio README.md

## ESTRUTURA DO BANCO DE DADOS
## TABELA PILOTOS
## TABELA PLANETAS
## TABELA NAVES
## TABELA HISTORICOVIAGENS
## TABELA PILOTOSNAVES

# SCRIPT DA TABELA PLANETAS
## esse script cria a tabela planetas e adiciona a coluna IdPlaneta como chave primaria para ser referênciada nas demais tabelas.

## CREATE TABLE Planetas(
##    IdPlaneta int NOT NULL,
##    Nome varchar (50) NOT NULL,
##    Rotacao float NOT NULL,
##    Orbita float NOT NULL,
##    Diametro float NOT NULL,
##    Clima varchar (50) NOT NULL,
##    Populacao int NOT NULL,
##

## GO
## ALTER TABLE Planetas ADD CONSTRAINT PK_Planetas PRIMARY KEY (IdPlaneta);

# SCRIPT DA TABELA NAVES
## esse script cria a tabela naves e adiciona a coluna IdNave como chave primaria para ser referênciada nas demais tabelas.

## CREATE TABLE Naves(
##    IdNave int NOT NULL,
##    Nome varchar (100) NOT NULL,
##    Modelo varchar (150) NOT NULL,
##    Passageiros int NOT NULL,
##    Carga float NOT NULL,
##    Classe varchar (100) NOT NULL,
## )

## GO
## ALTER TABLE Naves ADD CONSTRAINT PK_Naves PRIMARY KEY (IdNave);

# SCRIPT DA TABELA PILOTOS
## esse script cria a tabela Pilotos e adiciona a coluna IdPiloto como chave primaria para ser referênciada nas demais tabelas e adiciona uma FOREIGN KEY (chave estrangeira) IdPlaneta que faz referência a coluna IdPlaneta da Tabela PLanetas, essa chave compara o IdPlaneta da tabela Planetas com a coluna IdPlaneta da tabela Pilotos.

## CREATE TABLE Pilotos(
##    IdPiloto int NOT NULL,
##    Nome varchar (200) NOT NULL,
##    AnoNascimento varchar (10) NOT NULL,
##    IdPlaneta int NOT NULL,
## )

## GO
## ALTER TABLE Pilotos ADD CONSTRAINT PK_Pilotos PRIMARY KEY (IdPiloto);
## GO
## ALTER TABLE Pilotos ADD CONSTRAINT FK_Pilotos_Planetas FOREIGN KEY ( IdPlaneta) REFERENCES Planetas(IdPlaneta); 


# SCRIPT DA TABELA PILOTOSNAVES

## esse script cria a tabela PILOTOSNAVES utilizando o IdPiloto e IdNave como chave primária para que a tabela possa ser referênciada em outra e utiliza as mesmas colunas individualmente como chaves estrangeiras fazendo referência as tabelas Pilotos e Naves comparando assim se os Id's existentes na tabela PilotosNaves existem nas outras tabelas.

## CREATE TABLE PilotosNaves(
##    IdPiloto int NOT NULL,
##    IdNave int NOT NULL,
##    FlagAutorizado bit NOT NULL,
## )

## GO
## ALTER TABLE PilotosNaves ADD CONSTRAINT PK_PilotosNaves PRIMARY KEY (IdPiloto,IdNave);
## GO
## ALTER TABLE PilotosNaves ADD CONSTRAINT FK_PilotosNaves_Pilotos FOREIGN KEY ( IdPiloto) REFERENCES Pilotos (IdPiloto); 
## GO
## ALTER TABLE PilotosNaves ADD CONSTRAINT FK_PilotosNaves_Naves FOREIGN KEY ( IdNave) REFERENCES Naves(IdNave);
## GO
## ALTER TABLE PilotosNaves ADD CONSTRAINT DF_PilotosNaves_FlagAutorizado DEFAULT (1) FOR FlagAutorizado


# SCRIPT DA TABELA HISTORICOVIAGENS
## esse script cria a tabela HistoricoViagens utilizando como chave estrangeira as Colunas Idpiloto e IdNave para se refenricar a tabelas Pilotosnaves e registrar assim o Hitorico de saida e chegada das naves com seus respectivos Pilotos.


## CREATE TABLE HistoricoViagens(
##    IdPiloto int NOT NULL,
##    Dtsaida datetime NOT NULL,
##    DtChegada datetime NOT NULL,
## )

## GO
## ALTER TABLE HistoricoViagens ADD CONSTRAINT FK_HistoricoViagens_PilotosNaves  FOREIGN KEY (IdPiloto,IdNave) REFERENCES PilotosNaves (IdPiloto, IdNave)

## GO
## ALTER TABLE HistoricoViagens CHECK CONSTRAINT FK_HistoricoViagens_PilotosNaves
