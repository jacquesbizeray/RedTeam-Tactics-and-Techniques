---
description: 'https://blueteamlabs.online/home/challenge/1'
---

# Memory Analysis Ransomware

## Tools:

**Volatility** - memory analysis tool for inspecting memory dumps

The first step when running Volatility is trying to detect the profile that the tool is going to use. For a high level summary of the memory sample you’re analyzing, use the imageinfo command. Most often this command is used to identify the operating system, service pack, and hardware architecture \(32 or 64 bit\), but it also contains other useful information such as the DTB address and time the sample was collected.

```
$ volatility -f infected.vmem  imageinfo

```

As we can see the result for our memory dump we were suggested to use the **Win7SP1x86** profile for our analysis.

![Volatility profile suggestion](../../.gitbook/assets/image%20%282%29.png)

## Run “vol.py -f infected.vmem --profile=Win7SP1x86 psscan” that will list all processes. What is the name of the suspicious process? 

Answer: **@WanaDecryptor**

![psscan plugin output](../../.gitbook/assets/image%20%288%29.png)

## What is the parent process ID for the suspicious process?

Answer: **2732**

{% hint style="info" %}
**Basic Process Architecture**
{% endhint %}

![](../../.gitbook/assets/image%20%2811%29.png)

{% hint style="info" %}
 **Processos e Thread**: Basicamente o processo é uma instância de um programa em execução em memória. Um programa pode executar N processos para diferentes tarefas e todos esses subprocessos são conhecidos como **processos filhos** que são iniciados por um **processo pai**. Todos esses processos com área de memória não compartilhada. Quando falamos de threads estamos falando de subrotinas dentro de um mesmo processo com espaço de memória compartilhada.
{% endhint %}

## What is the initial malicious executable that created this process?

Answer: **or4qtckT.exe**

![](../../.gitbook/assets/image%20%2814%29.png)

## If you drill down on the suspicious PID \(vol.py -f infected.vmem --profile=Win7SP1x86 psscan \| grep \(PIDhere\)\), find the process used to delete files

Answer: **taskdl.exe**

Processo **taskdl.exe** tem como PPID o processo **or4qtckT.exe** que é o processo inicial malicioso

![pscan grep](../../.gitbook/assets/image%20%287%29.png)

## Find the path where the malicious file was first executed

Let’s now take a look at the last commands ran, by using **cmdscan**, **consoles** and **cmdline** plugins.

O plugin **consoles** \(que extrai o histórico de comandos digitados no **cmd.exe\)** e **cmdscan** \(que extrai o histórico de comandos também digitados no **cmd.exe** porém utiliza também busca em outros processos relacionados a command line\) não continham nenhuma informação em seus buffers\(área de memória\).

No entanto, o plugin **cmdline** que exibe os argumentos da linha de comando do processo nos deu informações interessantes onde conseguimos extrair o commandline do processo malicioso.

Answer: **C:\Users\hacker\Desktop\or4qtckT.exe**



```bash
root@sapiens:~/Downloads/BTLO Memory Analysis - Ransomware# volatility -f infected.vmem --profile=Win7SP1x86 cmdline
************************************************************************
or4qtckT.exe pid:   2732
Command line : "C:\Users\hacker\Desktop\or4qtckT.exe" 
************************************************************************

```

## Can you identify what ransomware it is? \(Do your research!\)

Answer: **WannaCry**

Somente pelo nome do do processo @WanaDecryptor já deduzimos que é o ransomware da família WannaCry.

## What is the filename for the file with the ransomware public key that was used to encrypt the private key? \(.eky extension\)

Answer: **00000000.eky**

Quando falamos de análise de memória estamos falando de processos que normalmente são executados a partir de conteúdo de dados que estão em disco. e enviados para a memória.   Um das formas de identificar arquivos sendo utilizados por processo é a partir de um referência conhecida como **Handle** que é um identificador abstrato de algum recurso\(arquivos, processos, Threads, etc..\) utilizado por uma aplicação no contexto de S.O. Uma dessas referências são conhecidas como **File Handle** onde conseguimos fazer o endereçamento de arquivos abertos por processos.

```bash
root@sapiens:~/Downloads/BTLO Memory Analysis - Ransomware# volatility -f infected.vmem --profile=Win7SP1x86 handles -p 2732

```

![](../../.gitbook/assets/image%20%281%29.png)

