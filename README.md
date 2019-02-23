# sewamobil
cd..
cd..
cd xampp\mysql\bin
mysql -u root
create table mobil
(kode varchar (4) primary key,
jenis varchar (6) not null,
merk varchar (10) not null,
tarif varchar (8) not null,
nopol varchar (8) not null);

desc mobil;

insert into mobil
(kode, jenis, merk, tarif, nopol)
values
('M001', 'SEDAN', 'BMW E5', '500000', 'GB1234AA'),
('M002', 'SEDAN', 'HONDA CRV', '350000', 'BG2345BB'),
('M003', 'BUS', 'MERCEDEZ', '1000000', 'BG3456CC'),
('M004', 'BUS', 'DYNA', '800000', 'BG8443DD'),
('M005', 'TRUCK', 'HYNO ZX', '1500000', 'BG4638EE'),
('M006', 'TRUCK', 'DYNA X1', '1500000', 'BG8473FF');

select * from mobil;

create table sewa
(kode varchar (4) primary key,
nama varchar (15) not null,
kontak varchar (8) not null,
alamat varchar (25) not null,
kota varchar (10) not null,
kodepos int (5) not null,
telepon varchar (8) not null );

desc sewa;

insert into sewa
(kode, nama, kontak, alamat, kota, kodepos, telepon)
values
('P001', 'PT FOX RIVER', 'HENDRA', 'JL.JEND. SUDIRMAN 657', 'BENGKULU', '30245', '1234567'),
('P002', 'CV FOXCON', 'IWAN', 'JL. WAHID HASYIM 743', 'JAKARTA', '73429', '234567'),
('P003', 'PT FARMACOM', 'YANI', 'JL. AHMAD DAHLAN 45', 'LAMPUNG', '28349', '3334445');

select * from sewa;

create table pelanggan
(nofaktursewa varchar (4) not null,
kodepelanggan varchar (4) not null,
tglsewa varchar (10) not null,
kodemobil varchar (4) not null,
lamasewa varchar (2) not null,
uangmuka varchar (8) not null);

desc pelanggan;

insert into pelanggan
(nofaktursewa, kodepelanggan, tglsewa, kodemobil, lamasewa, uangmuka)
values
('F001', 'P001', '2008-12-01', 'M001', '2', '200000'),
('F001', 'P001', '2008-12-01', 'M003', '2', '200000'),
('F002', 'P002', '2008-12-02', 'M002', '1', '100000');

select * from pelanggan;

select mobil. kode, jenis, merk, pelanggan. nofaktursewa, tglsewa, lamasewa
from mobil
left join pelanggan
on mobil.kode = pelanggan.kodemobil;

select pelanggan.nofaktursewa, sewa.nama, pelanggan.tglsewa, mobil.jenis, merk, pelanggan.lamasewa, uangmuka
from ( mobil inner join pelanggan  on mobil.kode = pelanggan.kodemobil ) 
inner join sewa on sewa.kode = pelanggan.kodepelanggan;

select sewa.nama, kota, pelanggan.nofaktursewa, tglsewa, kodemobil, lamasewa, uangmuka
from sewa
left join pelanggan
on sewa.kode = pelanggan.kodepelanggan
order by kota;


