# db_TaxUser
База данных для хранения информации о налогоплательщика в налоговой испекции.


## Таблица базы данных

### TaxUser
| Поле             | Тип            | Описание                       |
|------------------|----------------|-------------------------------|
| Id_TaxUser           | int (PK)       | Уникальный идентификатор       |
| INN            | nvarchar(60)  | Идентификационный номер налогоплательщика                |
| FIO           | nvarchar(60)  | ФИО налогоплательщика                   |
| Gender            | nvarchar(30)   | Пол налогоплательщика                    |
| birtday  | date            | Дата рождения налогоплательщика                |
| phone             | nvarchar(60)   | Номер телефона налогоплательщика |
| Type_taxUser       | nvarchar(60)            | Тип налогоплательщика(Например Физическое лицо,ИП,Юр лицо)    |
| document           | nvarchar(60)   | Документ подтвержающий личность налогоплательщика |
| Serial_and_number         | int   |  Серия и номер паспорта налогоплательщика                    |
| data_get      | date  | Дата выдачи документа налогоплательщика                |
| Who_get              | nvarchar(150)  | Кем выдан документ налогоплательщика       |
| cod      | int | код подразделения     |
| address      | nvarchar(150) | Адрес фактического проживания     |

### aut_tax
| Поле             | Тип            | Описание                       |
|------------------|----------------|-------------------------------|
| Id_taxAut          | int (PK)       | Уникальный идентификатор       |
| login            | nvarchar(60)  | Логин сотрудника налоговой инспекции               |
| password           | nvarchar(60)  | Пароль сотрудника налоголовой инспекции                   |

```sql
create table taxUser(
	id_taxUser int IDENTITY(1,1) not null,
	INN nvarchar(60) not null,
	FIO nvarchar(60) not null,
	gender nvarchar(30) not null,
	bitrday date not null,
	phone nvarchar(60) not null,
	type_taxUser nvarchar(100),
	document nvarchar(150) not null,
	serial_and_number int not null,
	data_get date not null,
	Who_get nvarchar(150) not null,
	cod int not null,
	adress nvarchar(250) not null,
);

insert into taxUser(INN,FIO,gender,bitrday,phone,type_taxUser,document,serial_and_number,data_get,Who_get,cod,adress) values ('7743013902', 'Иванов иван Иванович','Мужской', '1999-07-15', '89001237932', 'Физическое лицо', 'Паспорт РФ', 031925021, '2018-09-17', 'ГУ МВД', 23017,'662433, Костромская область, город Ногинск, проезд Косиора, 65')

insert into taxUser(INN,FIO,gender,bitrday,phone,type_taxUser,document,serial_and_number,data_get,Who_get,cod,adress) values ('7743013943', 'Иванова Марина Ивановна','Женский', '1999-08-14', '89001237932', 'Физическое лицо', 'Паспорт РФ', 031925064, '2018-09-17', 'ГУ МВД', 30019,'615597, Саратовская область, город Балашиха, наб. Балканская, 94')

insert into taxUser(INN,FIO,gender,bitrday,phone,type_taxUser,document,serial_and_number,data_get,Who_get,cod,adress) values ('7743013957', 'Иванов Петр Генадьевич','Мужской', '1999-07-20', '89001237932', 'Физическое лицо', 'Паспорт РФ', 031925034, '2017-10-10', 'ГУ МВД', 40019,'899407, Сахалинская область, город Можайск, въезд Славы, 84')

create table aut_tax(
 id_taxAyt int IDENTITY(1,1) not null,
 login nvarchar(60) not null,
 password nvarchar(60) not null,
);
insert aut_tax(login,password) values('Tax4', 'tax4');
```