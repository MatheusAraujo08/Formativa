# Formativa
create database formativa;
create database ok;
use ok;
use formativa;

create table user(
	id_user bigint not null auto_increment,
	nome varchar(200) not null,
	birth datetime not null,
	password varchar(11) not null,
	register_date datetime not null default now(),
	cpf varchar (15) not null,
	gender enum('M','F') not null,
	primary key (id)
);

create table application_level(
	id bigint not null auto_increment,
	nome varchar(200) not null,
	primary key (id)
);

create table occupation(
	id bigint not null auto_increment,
	employee bigint not null,
	job bigint not null,
	start_date datetime not null default now(),
	end_date date not null,
	primary key (id),
	foreign key (employee)  references user(id),
	foreign key (job)  references application_level(id)
);

create table local(
	id_local bigint not null auto_increment,
	local varchar(200) not null,
	blocks enum('A','B','C','D') not null,
	resources_FK bigint not null,
	primary key (id),
	foreign key (resources_FK) references infrastructure(id)
);

create table infrastructure(
	id bigint not null auto_increment,
	projetor enum('yes','no'),
	tv_smart enum('yes','no'),
	ar_condicionado enum('yes','no'),
	internet enum('yes','no'),
	banheiros enum('yes','no'),
	coffee_break enum('yes','no'),
	acessibilidade enum('yes','no'),
	bebedouros enum('yes','no'),
	primary key(id)
);

create table event(
	id_event bigint not null auto_increment,
    date_event datetime not null,
    name_event varchar(150) not null,
    description varchar(500),
    primary key (id_event)
);

create table details(
	id_details bigint not null auto_increment,
    idLocal_FK bigint not null,
	idEvent_FK bigint not null,
    primary key (id_details),
    foreign key (idLocal_FK) references local(id_local),
    foreign key (idEvent_FK) references event(id_event)
 );
 
 create table checkIn(
	id_checkIn bigint not null auto_increment,
    check_date datetime not null,
    status enum('active','disable'),
    idUser bigint not null,
    idEvent bigint not null,
    primary key (id_checkIn),
    foreign key (idEvent) references event(id_event),
    foreign key (idUser) references user(id_user)
 );
