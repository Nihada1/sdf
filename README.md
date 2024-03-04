/*create trigger update_izmjena
on 
proizvodi
for update
as 
begin
declare @id int
declare @akcija nvarchar(100)
select @id=id from inserted 
if update (id)
set @akcija= 'izmjenjen id '+ cast(getdate()as nvarchar(20))
if update (naziv_proizvoda)
set @akcija='izmjenjen naziv proizvoda '+ cast(getdate()as nvarchar(20))
if update (kolicina)
set @akcija='izmjenjena je kolicina '+ cast(getdate()as nvarchar(20))
insert into izmjene(id, opis_izmjene)
values (@id, @akcija)
end
select*from proizvodi
select*from izmjene
update proizvodi set id ='2' where id ='1'
update proizvodi set naziv_proizvoda='Mlijeko' where naziv_proizvoda='mlijeko'
update proizvodi set kolicina='7' where kolicina='5'*/

/*keirati bazu podataka evidencija kupaca sa tabelom kupac (kupac id ime i prezime kupca
telefon) i tabelom kupaclogs (kupac id status kupca) nad tabelom kupac kreirati okidace 
tkd se u koloni status kupca pise da je aktivan ako je dodan novi kupac u tabelu kupac, 
obrisan ako je izbrisan i ako je izmjenjena neka od kolona da pise da je izmjenjena ta
konkretna kolona*/
/*create database evidencija_kupaca
create table kupac
 (kupac_id int, ime_kupca nvarchar(50), prezime_kupca nvarchar(50), telefon int)
 create table kupaclogs
 (kupac_id int, 
 status_kupca nvarchar(50))*/
 create trigger update_izmjena
 on kupac for update
 as begin
 declare @kupac_id int
 declare @akcija nvarchar(100)
 select @kupac_id=kupac_id from inserted
 if update (kupac_id)
 set @akcija='aktivan'
 if update (ime_kupca)
 set @akcija='aktivan'
 if update (prezime_kupca)
 set @akcija='aktivan'
  if update (telefon)
 set @akcija='aktivan'
 insert into kupaclogs(kupac_id,status_kupca)
 values (@kupac_id,@akcija)
 end

 update kupac
 set kupac_id=1
 where ime_kupca='kemal'
 

 insert into kupac
 values(1,'kemal','hadzic',45674)
 select*from kupaclogs




 CREATE TRIGGER proizvodi_za_update
 on proizvodi
 for update
 as begin
 select*from deleted
 select*from inserted
 end
 select*from proizvodi

 update proizvodi set id=2 where id=5

 CREATE TRIGGER kupac_za_update
 on kupac
 for update
 as begin
 select*from deleted
 select*from inserted
 end

 
 update kupac set kupac_id=1 where kupac_id=1
