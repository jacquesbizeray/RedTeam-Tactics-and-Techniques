# Log Analysis

### 

```python
# Comando para ajudar na filtragem de logs tipo APACHE com linhas únicas
cut -d DELIMITADOR -f1 desec_accesslog.txt | sort -u

#Comando para ajudar na filtragem de logs tipo APACHE com linhas únicas e contagem de ocorrências
cut -d - -f1 desec_accesslog.txt | sort | uniq -c | sort -unr
```

