---
external help file: ProMail-help.xml
Module Name: ProMail
online version: 
schema: 2.0.0
---

# Get-Rule

## SYNOPSIS
Obtiene las reglas registradas.

## SYNTAX

```
Get-Rule [[-ObjectEmailAccount] <Object>] [[-IdRule] <String>] [[-Name] <String>]
```

## DESCRIPTION
Obtiene las reglas registradas.

## EXAMPLES

### -------------------------- EXAMPLE 1 --------------------------
```powershell
Get-Rule
```

### -------------------------- EXAMPLE 2 --------------------------
```powershell
Get-Rule -Name Regla
```

### -------------------------- EXAMPLE 3 --------------------------
```powershell
Get-Rule -idRule 7
```

### -------------------------- EXAMPLE 4 --------------------------
```powershell
Get-EmailAccount | Get-Rule
```

### -------------------------- EXAMPLE 5 --------------------------
```powershell
Get-EmailAccount -EmailAddress 'preuba@prueba.com' | Get-Rule
```

### -------------------------- EXAMPLE 6 --------------------------
```powershell
Get-EmailAccount -EmailAddress 'preuba@prueba.com' | Get-Rule -IdRule 2
```

## PARAMETERS

### -ObjectEmailAccount
Objeto con las cuentas de correo para determinar las cuentas asociadas.

```yaml
Type: Object
Parameter Sets: (All)
Aliases: 

Required: False
Position: 1
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -IdRule
Identificador de la regla que se buscara.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: 2
Default value: *
Accept pipeline input: False
Accept wildcard characters: True
```

### -Name
Nombre de la regla que se buscara.

```yaml
Type: String
Parameter Sets: (All)
Aliases: 

Required: False
Position: 3
Default value: *
Accept pipeline input: False
Accept wildcard characters: True
```

## INPUTS

## OUTPUTS

### Información de las reglas registradas, filtrada de acuerdo a los parámetros ingresados.

## NOTES
Autor: \<Jarodriguezc\>

## RELATED LINKS

[Register-Rule](Register-Rule.md)

[Update-RuleTemplate](Update-RuleTemplate.md)
