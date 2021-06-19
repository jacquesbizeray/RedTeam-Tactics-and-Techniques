---
description: 'https://blueteamlabs.online/home/challenge/19'
---

# Reverse Engineering - Another Injection

**1 - What is the language the program is written?**

GoLang

Para descobrir é só usar o DiE ou bintext ou qualquer outro software para fazer a leitura de strings do binário. Logo no começo ele nos mostra o Go build id que é o hash dos arquivos compilados + a versão do compilador. Padrão de todos softwares compilados para linguagem Go.

**2 - What is the build id?**

eck19EyXq\_9c975RxNJ1/QkbhfvYWoTcAeJreFwhX/q3HwQW17YdD3iMlLFCzB/1ZpNy-9ah0QEvzlOTFcq



**3 - What is the dependency package the sample uses for invoking windows APIs \(1 points\)**

{% embed url="https://github.com/TheTitanrain/w32" %}

Find using strings

**4 - What is the victim process? \(Hint: 32bit\)**

Find using strings

notepad.exe

**5 - What is the process invoked from the shellcode?**

powershell.exe Find using strings

**6 - What is the name of the created file?**

C:\Windows\Temp\change.ps1

É só fazer o decode do base64 do powershell no CYberchef e achar os paths

**7- What is the name of the actual tool executed?**

Invoke-Phant0m

Script powershell carregado na linha de comando já decodado para achar a resposta acima 







