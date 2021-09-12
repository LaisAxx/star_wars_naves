# star_wars_ships

### SQL for creating a template

```
USE StarOfDeath

--****** PLANETS
CREATE TABLE Planets(
	IdPlanet int NOT NULL,
	Name varchar(50) NOT NULL,
	Rotation float NOT NULL,
	Orbit float NOT NULL,
	Diameter float NOT NULL,
	Climate varchar(50) NOT NULL,
	Population int NOT NULL,
)
GO
ALTER TABLE Planet ADD CONSTRAINT PK_Planet PRIMARY KEY (IdPlanet);
GO
--****************************************************************************************
--****** SpaceShips ***************************************************************************
CREATE TABLE SpaceShips(
	IdShip int NOT NULL,
	Name varchar(100) NOT NULL,
	Model varchar(150) NOT NULL,
	Passager int NOT NULL,
	Load float NOT NULL,
	Class varchar(100) NOT NULL,
)
GO
ALTER TABLE SpaceShips ADD CONSTRAINT PK_SpaceShip PRIMARY KEY (IdShip);
GO
--****** PILOTS ****************************************************************************
--******************************************************************************************
CREATE TABLE Pilots(
	IdPilot int NOT NULL,
	Name varchar(200) NOT NULL,
	BirthYear varchar(10) NOT NULL,
	IdPlanet int NOT NULL,
)
GO
ALTER TABLE Pilots ADD CONSTRAINT PK_Pilots PRIMARY KEY (IdPilot);
GO
ALTER TABLE Pilots  ADD  CONSTRAINT FK_Pilot_Planet FOREIGN KEY(IdPlanet)
REFERENCES Planet (IdPlanet)
GO
ALTER TABLE Pilots CHECK CONSTRAINT FK_Pilot_Planet
GO
--******************************************************************************************
--****** PILOTS NAVES *********************************************************************
CREATE TABLE PilotsShips(
	IdPilot int NOT NULL,
	IdNave int NOT NULL,
	AuthorizedFlag bit NOT NULL,
)
GO
ALTER TABLE PilotosNaves ADD CONSTRAINT PK_PilotosNaves PRIMARY KEY (IdPilot, IdShip);
GO
ALTER TABLE PilotsShips  ADD CONSTRAINT FK_PilotsShips_Pilots FOREIGN KEY(IdPilot)
REFERENCES Pilots (IdPilot)
GO
ALTER TABLE PilotsShips  ADD CONSTRAINT FK_PilotsShips_Ships FOREIGN KEY(IdShips)
REFERENCES SpaceShips (IdNave)
GO
ALTER TABLE PilotsShips  ADD CONSTRAINT DF_PilotsShips_AuthorizedFlag  DEFAULT (1) FOR AuthorizedFlag
GO
--****************************************************************************************************
--******History of rides************************************************************************
CREATE TABLE RidesHistory(
	IdShip int NOT NULL,
	IdPilot int NOT NULL,
	DtExit datetime NOT NULL,
	DtEntry datetime NULL
)
GO

ALTER TABLE RidesHistory  ADD  CONSTRAINT FK_RidesHistory_PilotsShips FOREIGN KEY(IdPilot, IdShip)
REFERENCES PilotsShips (IdPilot, IdShip)
GO

ALTER TABLE RidesHistory CHECK CONSTRAINT FK_RidesHistory_PilotsShips
GO
```

