# Comparativo do desempenho das nuvens AWS e GoogleCloud no processamento de big data do Programa Bolsa Família

##### Autores
- Aleteia Patricia F. de Araújo Von Paumgartten
- Esteyse Glenaise Santana Carneiro
- Hudson Neves e Silva
- Francisco Keppler S. Alecrim
- Leonardo Rebouças de Carvalho
- Lucélia Vieira Mota

##### Objetivo
- Executar workloads hadoop em diferentes provedores de núvem e comparar seus desempenhos

##### Limitações
- Os workloads foram desenvolvidos usando URLs que podem ter sido removidas
- Foram projetados para serem executados em ambiente Linux

##### Workloads
- Workload 1 - Calcular a quantidade de bolsas família pagos em 2017 por estado
  
  ```
  Qtde de bolsas  Estado
  21510356        BA
  17631560        SP
  13462414        PE
  12457106        MG
  12284805        CE
  11601055        MA
  10969235        PA
  9384842 RJ
  6093673 PB
  5288845 PI
  4758758 AL
  4542636 AM
  4329379 PR
  4313072 RS
  4085884 RN
  3705041 GO
  3251315 SE
  2023333 ES
  1913055 MT
  1515803 MS
  1502019 TO
  1407727 SC
  1033412 RO
  1010360 AC
  967168  DF
  792596  AP
  548550  RR
  ```
  
- Workload 2 - Calcular a frequência de recebimentos de bolsa familia por NIS agrupado pela quantidade
  
  *Nesse caso **11220885** pessoas receberam o bolsa família **12** vezes em 2017 e **12180822** apenas **uma** vez. Observe que **819** pessoas receberam o benefício **23** vezes*
  
  ```
  Qtde de bolsas recebidas Qtde de NIS
  32 2
  31 2
  30 3
  29 4
  28 5
  27 1
  26 4
  25 21
  24 16
  23 819
  22 740
  21 773
  20 858
  19 1727
  18 3361
  17 2299
  16 9239
  15 7130
  14 58038
  13 34272
  12 11220885
  11 217775
  10 318090
  9 210881
  8 353757
  7 258417
  6 860774
  5 960261
  4 430025
  3 385628
  2 380178
  1 12180822
  ```

##### Nuvens
- Google Cloud - Região (us-east1-b - Carolina do Sul/US)
  - Serviço: Dataproc  
    - Master: 1 x 4 Cores 8 RAM HD 32Gb
    - Workers: 2 x 4 Cores 8 RAM HD 32Gb
  
- AWS - Região (Carolina do Norte/US)
  - Criação de KeyPair (para acessar às máquinas)
  - Criação de Grupo de Segurança (para liberar acesso à porta 22 SSH)
  - Serviço: EMR
    - Master: 1 x m4.large (4 Cores 8 RAM HD 32Gb)
    - Workers: 2 x m4.large (4 Cores 8 RAM HD 32Gb)
 
##### Utilização
- Aprovisionar a núvem
- Acessar a máquina master remota
- Baixar este projeto

  ```
  git clone https://github.com/leonardoreboucas/comparativo-aws-gcloud.git
  ```

  ```
  cd comparativo-aws-gcloud
  ```

- Baixar os dados do Portal da transparência
  ```
  ./baixar_dados.sh
  ```
- Copiar dados para o Hadoop
  ```
  ./copiar_para_hadoop.sh
  ```
- Executar Workload 1
  ```
  ./workload1.sh
  ```

- Executar Workload 2
  ```
  ./workload2.sh
  ```

##### Monitoramento
Os dados de monitoramentos serão gerados nos diretórios: [workload]/monitoramento
Monitores:
 CPU (top)
 ```
 echo `date +'%s'` `sudo top -bc -d 1 -n 1 | grep -m1 -e '%Cpu'`
 ```
 CPU (saída)
 ```
1529085524 %Cpu(s): 24.3 us, 18.6 sy, 0.0 ni, 50.2 id, 6.4 wa, 0.0 hi, 0.5 si, 0.0 st
1529085525 %Cpu(s): 24.3 us, 18.6 sy, 0.0 ni, 50.2 id, 6.4 wa, 0.0 hi, 0.5 si, 0.0 st
1529085526 %Cpu(s): 24.3 us, 18.6 sy, 0.0 ni, 50.1 id, 6.4 wa, 0.0 hi, 0.5 si, 0.0 st
1529085528 %Cpu(s): 24.3 us, 18.6 sy, 0.0 ni, 50.1 id, 6.4 wa, 0.0 hi, 0.5 si, 0.0 st
1529085529 %Cpu(s): 24.3 us, 18.6 sy, 0.0 ni, 50.1 id, 6.4 wa, 0.0 hi, 0.5 si, 0.0 st
1529085530 %Cpu(s): 24.3 us, 18.6 sy, 0.0 ni, 50.1 id, 6.4 wa, 0.0 hi, 0.5 si, 0.0 st
1529085531 %Cpu(s): 24.3 us, 18.6 sy, 0.0 ni, 50.1 id, 6.4 wa, 0.0 hi, 0.5 si, 0.0 st
1529085532 %Cpu(s): 24.3 us, 18.6 sy, 0.0 ni, 50.1 id, 6.4 wa, 0.0 hi, 0.5 si, 0.0 st
1529085534 %Cpu(s): 24.3 us, 18.6 sy, 0.0 ni, 50.1 id, 6.3 wa, 0.0 hi, 0.5 si, 0.0 st
1529085535 %Cpu(s): 24.3 us, 18.6 sy, 0.0 ni, 50.1 id, 6.3 wa, 0.0 hi, 0.5 si, 0.0 st
1529085536 %Cpu(s): 24.4 us, 18.6 sy, 0.0 ni, 50.1 id, 6.3 wa, 0.0 hi, 0.5 si, 0.0 st
1529085537 %Cpu(s): 24.4 us, 18.6 sy, 0.0 ni, 50.1 id, 6.3 wa, 0.0 hi, 0.5 si, 0.0 st
1529085538 %Cpu(s): 24.4 us, 18.6 sy, 0.0 ni, 50.1 id, 6.3 wa, 0.0 hi, 0.5 si, 0.0 st
1529085540 %Cpu(s): 24.4 us, 18.6 sy, 0.0 ni, 50.1 id, 6.3 wa, 0.0 hi, 0.5 si, 0.0 st
 ```
 
 IO (iotop)
 ```
 echo `date +'%s'` `sudo iotop -b -a -k -t -o -n 1 -d 1 | grep "Actual DISK"` `sudo iotop -b -a -k -t -o -n 1 -d 1 | grep "Total DISK"` 
 ```
 
 IO (saída)
 ```
1529085963 18:06:03 Actual DISK READ: 0.00 K/s | Actual DISK WRITE: 0.00 K/s 18:06:04 Total DISK READ : 0.00 K/s | Total DISK WRITE : 0.00 K/s
1529085965 18:06:05 Actual DISK READ: 0.00 K/s | Actual DISK WRITE: 0.00 K/s 18:06:05 Total DISK READ : 0.00 K/s | Total DISK WRITE : 59.95 K/s
1529085966 18:06:06 Actual DISK READ: 0.00 K/s | Actual DISK WRITE: 0.00 K/s 18:06:06 Total DISK READ : 0.00 K/s | Total DISK WRITE : 0.00 K/s
1529085967 18:06:08 Actual DISK READ: 0.00 K/s | Actual DISK WRITE: 0.00 K/s 18:06:08 Total DISK READ : 0.00 K/s | Total DISK WRITE : 0.00 K/s
1529085969 18:06:09 Actual DISK READ: 0.00 K/s | Actual DISK WRITE: 76.12 K/s 18:06:09 Total DISK READ : 0.00 K/s | Total DISK WRITE : 161.47 K/s
1529085970 18:06:11 Actual DISK READ: 0.00 K/s | Actual DISK WRITE: 0.00 K/s 18:06:11 Total DISK READ : 0.00 K/s | Total DISK WRITE : 0.00 K/s
1529085972 18:06:12 Actual DISK READ: 0.00 K/s | Actual DISK WRITE: 0.00 K/s 18:06:12 Total DISK READ : 0.00 K/s | Total DISK WRITE : 0.00 K/s
1529085973 18:06:14 Actual DISK READ: 0.00 K/s | Actual DISK WRITE: 0.00 K/s 18:06:14 Total DISK READ : 0.00 K/s | Total DISK WRITE : 0.00 K/s  
 ```
 
 
 Memória (top)
 ```
 echo `date +'%s'` `sudo top -bc -d 1 -n 1 | grep -m1 -e 'KiB Mem'`
 ```
 
 Memória (saída)
 ```
1529085945 KiB Mem: 3800612 total, 3583308 used, 217304 free, 9372 buffers
1529085946 KiB Mem: 3800612 total, 3567392 used, 233220 free, 9372 buffers
1529085947 KiB Mem: 3800612 total, 3566340 used, 234272 free, 9372 buffers
1529085948 KiB Mem: 3800612 total, 3567408 used, 233204 free, 9372 buffers
1529085949 KiB Mem: 3800612 total, 3564536 used, 236076 free, 9372 buffers
1529085950 KiB Mem: 3800612 total, 3567580 used, 233032 free, 9380 buffers
1529085952 KiB Mem: 3800612 total, 3568128 used, 232484 free, 9380 buffers
1529085953 KiB Mem: 3800612 total, 3578440 used, 222172 free, 9380 buffers
1529085954 KiB Mem: 3800612 total, 3572576 used, 228036 free, 9380 buffers
1529085955 KiB Mem: 3800612 total, 3580352 used, 220260 free, 9388 buffers
1529085956 KiB Mem: 3800612 total, 3575640 used, 224972 free, 9388 buffers
1529085958 KiB Mem: 3800612 total, 3579748 used, 220864 free, 9388 buffers
1529085959 KiB Mem: 3800612 total, 3569808 used, 230804 free, 9388 buffers
1529085960 KiB Mem: 3800612 total, 3569636 used, 230976 free, 9396 buffers
1529085961 KiB Mem: 3800612 total, 3570148 used, 230464 free, 9396 buffers
1529085962 KiB Mem: 3800612 total, 3566556 used, 234056 free, 9396 buffers
1529085964 KiB Mem: 3800612 total, 3569828 used, 230784 free, 9396 buffers
 ```
  
 Rede (iftop)
 ```
 echo `date +"%s"` `sudo iftop -t -p -s 1 | grep "send rate"` `sudo iftop -t -p -s 1 | grep "receive rate"`
 ```
 
  Rede (saída)
 ``` 
1529085653 Total send rate: 33.7Kb 33.7Kb 33.7Kb Total receive rate: 20.7Kb 20.7Kb 20.7Kb Total send and receive rate: 105Kb 105Kb 105Kb
1529085661 Total send rate: 42.4Kb 42.4Kb 42.4Kb Total receive rate: 13.4Kb 13.4Kb 13.4Kb Total send and receive rate: 62.6Kb 62.6Kb 62.6Kb
1529085667 Total send rate: 6.25Kb 6.25Kb 6.25Kb Total receive rate: 16.1Kb 16.1Kb 16.1Kb Total send and receive rate: 106Kb 106Kb 106Kb
1529085673 Total send rate: 85.9Kb 85.9Kb 85.9Kb Total receive rate: 22.4Kb 22.4Kb 22.4Kb Total send and receive rate: 34.9Kb 34.9Kb 34.9Kb
1529085680 Total send rate: 5.21Kb 5.21Kb 5.21Kb Total receive rate: 21.1Kb 21.1Kb 21.1Kb Total send and receive rate: 57.1Kb 57.1Kb 57.1Kb
1529085687 Total send rate: 55.6Kb 55.6Kb 55.6Kb Total receive rate: 16.1Kb 16.1Kb 16.1Kb Total send and receive rate: 21.3Kb 21.3Kb 21.3Kb
1529085693 Total send rate: 4.55Kb 4.55Kb 4.55Kb Total receive rate: 17.9Kb 17.9Kb 17.9Kb Total send and receive rate: 39.3Kb 39.3Kb 39.3Kb
1529085700 Total send rate: 16.9Kb 16.9Kb 16.9Kb Total receive rate: 15.9Kb 15.9Kb 15.9Kb Total send and receive rate: 215Kb 215Kb 215Kb
1529085707 Total send rate: 220Kb 220Kb 220Kb Total receive rate: 14.8Kb 14.8Kb 14.8Kb Total send and receive rate: 49.5Kb 49.5Kb 49.5Kb
1529085714 Total send rate: 26.4Kb 26.4Kb 26.4Kb Total receive rate: 15.0Kb 15.0Kb 15.0Kb Total send and receive rate: 20.8Kb 20.8Kb 20.8Kb
1529085721 Total send rate: 85.9Kb 85.9Kb 85.9Kb Total receive rate: 14.7Kb 14.7Kb 14.7Kb Total send and receive rate: 24.1Kb 24.1Kb 24.1Kb
1529085728 Total send rate: 145Kb 145Kb 145Kb Total receive rate: 17.3Kb 17.3Kb 17.3Kb Total send and receive rate: 152Kb 152Kb 152Kb
```
