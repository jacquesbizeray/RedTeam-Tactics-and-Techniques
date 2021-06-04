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

![Volatility profile suggestion](../../.gitbook/assets/image%20%281%29.png)

## Run “vol.py -f infected.vmem --profile=Win7SP1x86 psscan” that will list all processes. What is the name of the suspicious process? 

Answer: **@WanaDecryptor**

![psscan plugin output](../../.gitbook/assets/image%20%283%29.png)

## What is the parent process ID for the suspicious process?

Answer: **2732**

{% hint style="info" %}
**Basic Process Architecture**
{% endhint %}

![](../../.gitbook/assets/image%20%287%29.png)

{% hint style="info" %}
 **Processos e Thread**: Basicamente o processo é uma instância de um programa em execução em memória. Um programa pode executar N processos para diferentes tarefas e todos esses subprocessos são conhecidos como **processos filhos** que são iniciados por um **processo pai**. Todos esses processos com área de memória não compartilhada. Quando falamos de threads estamos falando de subrotinas dentro de um mesmo processo com espaço de memória compartilhada.
{% endhint %}

Once you're strong enough, save the world:

{% code title="hello.sh" %}
```bash
# Ain't no code for that yet, sorry
echo 'You got to trust me on this, I saved the world'
```
{% endcode %}



