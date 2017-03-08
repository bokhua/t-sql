# t-sql
T-SQL used for projects
#### update user email domain
```sql
declare @id as int, @email as varchar(255)

select @id=min(id) from mdl_user where email like '%@%'

while (@id>0)
begin
	select @email = email from mdl_user where id=@id
	
	set @email = substring(@email, 1, charindex('@', @email)-1) + '@noreply.com'
	
	print 'userid: ' + convert(varchar(50), @id) + ' new email: ' + @email

	update mdl_user set email = @email where id=@id

	select @id=min(id) from mdl_user where email like '%@%' and id>@id 
end
```
