# E_shop
create table loginUser(
	idUser int primary key,
	emailUser varchar(80),
	passwdUser varchar(80)
);

create table customer(
	IdCustomer int primary key references loginUser(idUser),
	nameCustomer varchar(80),
	firstnameCustomer varchar(80),
	billingAddress varchar(80),
	deliveryAddress varchar(80),
	CPCustomer varchar(80),
);

create table commercial(
	IdCommercial int primary key references loginUser(idUser)
);

create table stockController(
	idSC int primary key references loginUser(idUser)
);

create table orderCust(
	idOrder int primary key,
	dateOrder varchar(80),
	totalAmount decimal(7,2),
	deliveryCost decimal(7,2),
	deliveryDate varchar(80),
	paymentDate varchar(80),
	Refcustomer int references customer(IdCustomer) 
		
);

create table discount(
	idDiscount int primary key, 
	startingDate varchar(80),
	endingDate varchar(80),
	pourcentage float check(pourcentage >= 0 AND pourcentage < 1)

);


create table product(
	idProduct int primary key,
	priceProduct decimal(7,2),
	stockLevel int, 
	brand varchar(80),
	descriptionProduct varchar(80),
	refDiscount int references discount(idDiscount)
);

create table computer(
	idComputer int primary key references product(idProduct),
	CPU varchar(80),
	RAM varchar(80),
	OS varchar(80)
);

create table screen(
	idScreen int primary key references product(idProduct),
	size varchar(30),
	definitionScreen varchar(80)
);

create table accessory(
	idAccessory int primary key references product(idProduct),
	typeProduct varchar(80)
);

create table orderLine(
	idOrderLine int primary key,
	refOrder int references orderCust(idOrder),
	refProduct int references product(idProduct),
	quantity int,
	priceLine decimal(7,2)
);

