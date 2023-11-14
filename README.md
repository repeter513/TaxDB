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
| idType_tax     | int | Вторичный ключ   |
| idTaxPaymets     | int |  Вторичный ключ     |

### aut_tax
| Поле             | Тип            | Описание                       |
|------------------|----------------|-------------------------------|
| Id_taxAut          | int (PK)       | Уникальный идентификатор       |
| login            | nvarchar(60)  | Логин сотрудника налоговой инспекции               |
| password           | nvarchar(60)  | Пароль сотрудника налоголовой инспекции                   |

### types_tax
| Поле             | Тип            | Описание                       |
|------------------|----------------|-------------------------------|
|idType_tax          | int (PK)       | Уникальный идентификатор       |
| code_Type           | int  | Код налогоплательщика               |
| name_Type          | nvarchar(60)  | Название типа налогоплательщика                  |

### taxPayments
| Поле             | Тип            | Описание                       |
|------------------|----------------|-------------------------------|
|idTaxPayments          | int (PK)       | Уникальный идентификатор       |
|idType_tax          | int  | Код типа налогоплательщика               |
| id_taxUser         | int  | Индефикатор налогоплательщика                 |
| price        | nvarchar(60)  | Сумма налога                |
| status         | nvarchar(60)  | Статус оплаты(Пример: Не оплаченно, в процессе, оплаченно)                |


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
	idType_tax int not null,
	idTaxPayments int null,
	PRIMARY KEY (id_taxUser)
);
create table aut_tax(
 id_taxAyt int IDENTITY(1,1) not null,
 login nvarchar(60) not null,
 password nvarchar(60) not null,
 PRIMARY KEY (id_taxAyt)
);
create table types_tax(
idType_tax int IDENTITY(1,1) not null,
code_Type int not null,
name_Type nvarchar(80) not null,
PRIMARY KEY (idType_tax)
);
create table taxPayments(
idTaxPayments int IDENTITY(1,1) not null,
idType_tax int not null,
id_taxUser int not null,
price nvarchar(60) not null,
status nvarchar(60) not null,
PRIMARY KEY (idTaxPayments)
);
ALTER TABLE taxUser ADD CONSTRAINT tax_user_fk0 FOREIGN KEY (IdType_tax) REFERENCES types_tax(idType_tax);
ALTER TABLE taxUser ADD CONSTRAINT tax_user_fk1 FOREIGN KEY (idTaxPaymets) REFERENCES taxPayments(idTaxPayments);
ALTER TABLE taxPayments ADD CONSTRAINT tax_Payments_fk0 FOREIGN KEY (idType_tax) REFERENCES types_tax(idType_tax);
ALTER TABLE taxPayments ADD CONSTRAINT tax_Payments_fk1 FOREIGN KEY (id_taxUser) REFERENCES taxUser(id_taxUser);

insert into taxUser(INN,FIO,gender,bitrday,phone,type_taxUser,document,serial_and_number,data_get,Who_get,cod,adress,idType_tax) values ('7743013902', 'Иванов иван Иванович','Мужской', '1999-07-15', '89001237932', 'Физическое лицо', 'Паспорт РФ', 031925021, '2018-09-17', 'ГУ МВД', 23017,'662433, Костромская область, город Ногинск, проезд Косиора, 65',1)

insert into taxUser(INN,FIO,gender,bitrday,phone,type_taxUser,document,serial_and_number,data_get,Who_get,cod,adress,idType_tax) values ('7743013943', 'Иванова Марина Ивановна','Женский', '1999-08-14', '89001237932', 'Физическое лицо', 'Паспорт РФ', 031925064, '2018-09-17', 'ГУ МВД', 30019,'615597, Саратовская область, город Балашиха, наб. Балканская, 94',3)

insert into taxUser(INN,FIO,gender,bitrday,phone,type_taxUser,document,serial_and_number,data_get,Who_get,cod,adress,idType_tax) values ('7743013957', 'Иванов Петр Генадьевич','Мужской', '1999-07-20', '89001237932', 'Физическое лицо', 'Паспорт РФ', 031925034, '2017-10-10', 'ГУ МВД', 40019,'899407, Сахалинская область, город Можайск, въезд Славы, 84',4)

insert into types_tax (code_Type,name_Type) values(720,'физическое лицо, зарегистрированное в качестве индивидуального предпринимателя');
insert into types_tax (code_Type,name_Type) values(730,'нотариус, занимающийся частной практикой, и другие лица, занимающиеся в установленном законодательством Российской Федерации порядке частной практикой');
insert into types_tax (code_Type,name_Type) values(740,'адвокат, учредивший адвокатский кабинет');
insert into types_tax (code_Type,name_Type) values(750,'арбитражный управляющий');
insert into types_tax (code_Type,name_Type) values(760,'иное физическое лицо, декларирующее доходы в соответствии со статьями 227.1 и 228 Налогового кодекса Российской Федерации (далее - Кодекс)');
insert into types_tax (code_Type,name_Type) values(770,'физическое лицо, зарегистрированное в качестве индивидуального предпринимателя и являющееся главой крестьянского (фермерского) хозяйства');
insert into taxPayments(idType_tax,id_taxUser,price,status) values(1,1,'5000₽','Не оплачен');
insert into taxPayments(idType_tax,id_taxUser,price,status) values(3,2,'7000₽','В процессе');
insert into taxPayments(idType_tax,id_taxUser,price,status) values(4,3,'10000₽','Оплачен');
insert aut_tax(login,password) values('Tax1', 'tax1');
insert aut_tax(login,password) values('Tax2', 'tax2');
insert aut_tax(login,password) values('Tax3', 'tax3');
insert aut_tax(login,password) values('Tax3', 'tax3');

```