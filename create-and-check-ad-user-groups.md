## Configuração de autenticação LDAPS 
Requisitos:
- URL do Servidor: Endereço de acesso ao servidor LDAP/AD.
- Diretório Base de Pesquisa as Entradas LDAP/AD: Nome do BASE-DC (Base Domain
Controller) do servidor.
- Usuário padrão de acesso ao LDAPS/AD: Nome do usuário administrador para realizar as
pesquisas ao grupo da BASE-DC e autorizar as autenticações;
- Senha do usuário padrão de acesso LDAPS/AD
- Grupo de Usuários Padrão com Acesso ao Example User
- Grupo de Usuários Administradores com Acesso ao Example User

## Explorar AD:
Windows: 
```bash 
dsquery user -name "Administrator"
```

Linux: 
```bash 
ldapsearch -x -H ldap://nome-do-servidor -b "dc=example,dc=com" -D "cn=Administrator,dc=example,dc=com" -W
```

## Criando usuário 
# Criação do grupo de usuários padrão
```bash 
New-ADGroup -Name "ExampleCorp_Users" -SamAccountName "ExampleCorp_Users" -GroupCategory Security -GroupScope Global -DisplayName "Example Corp Users" -Description "Grupo de usuários padrão para Example Corp" -Path "OU=ExampleCorp,DC=example,DC=com"
```
# Criação do grupo de administradores
```bash 
New-ADGroup -Name "ExampleCorp_Admins" -SamAccountName "ExampleCorp_Admins" -GroupCategory Security -GroupScope Global -DisplayName "Example Corp Admins" -Description "Grupo de usuários padrão para Example Corp" -Path "OU=ExampleCorp,DC=example,DC=com"
```

## Usando Powershell para verificar DN do usuário:
Windows: 
```bash 
Get-ADUser -Identity ExampleCorpUser | Select-Object DistinguishedName
```
```bash 
Linux: ldapsearch -x -H ldap://nome-do-servidor -b "dc=example,dc=com" -D "cn=admin,dc=example,dc=com" -W "(cn=HanditUsers)" dn
```

## Usando Powershell para verificar DN do grupo:
Windows: 
```bash 
Get-ADGroup -Identity ExampleCorpGroup | Select-Object DistinguishedName
```
Linux: 
```bash 
ldapsearch -x -H ldap://nome-do-servidor -b "dc=example,dc=com" -D "cn=admin,dc=example,dc=com" -W "(sAMAccountName=nome_do_usuario)" dn
```


