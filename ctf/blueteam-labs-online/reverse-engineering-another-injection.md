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

github.com/TheTitanrain/w32

