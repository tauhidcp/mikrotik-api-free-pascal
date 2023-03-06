# mikrotik-api-free-pascal
Mikrotik API for Free Pascal. Execute Mikrotik / Routeros Command from Free Pascal / Lazarus App.

### How to Use

- Download unit and add it to Free Pascal / Lazarus Project

- Add **mikrotikapi** unit to **uses** 

- Declare global variable 

```
Mikrotik : TMikrotikAPI; 
```

- Example Login 

```
  Mikrotik := TMikrotikAPI.Create;
  Mikrotik.Host := EHost.Text;
  Mikrotik.User := EUser.Text;
  Mikrotik.Pass := EPass.Text;
  Mikrotik.Port := EPort.Text;
  if (Mikrotik.Connect = True)
     then ShowMessage('Success!')
          else ShowMessage('Failed!');  
```

- Example Print Interface List to Memo

```
var
  i : integer;
begin
   Mikrotik.Res := Mikrotik.getResult('/interface/print');
   for i := 1 to Mikrotik.Res.RowsCount do
   begin
     Memo1.Lines.Append('id = '+Mikrotik.Res.ValueByName['.id']);
     Memo1.Lines.Append('Name = '+Mikrotik.Res.ValueByName['name']);
     Memo1.Lines.Append('Mac = '+Mikrotik.Res.ValueByName['mac-address']);
     Memo1.Lines.Append('Type = '+Mikrotik.Res.ValueByName['type']);
     Memo1.Lines.Append('===================');
     Mikrotik.Res.Next;
   end;  
```

- Example Add User (Execute) 

```
var
Status : String;
begin
  Status := Mikrotik.Execute('/user/add name=budi group=full');
  ShowMessage(Status);
end;  
```
