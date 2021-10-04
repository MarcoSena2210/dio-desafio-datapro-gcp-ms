# dio-desafio-dataproc-gcp-ms

# Digital Innovation One
Código criado para utilização junto a plataforma da Digital Innovation One

<p align="center"><img src="./DIO.png" width="500"></p>

## Desafio GCP Dataproc

O desafio faz parte do curso na plataforma da Digital Innovation One:

__*Criando um ecossitema Hadoop totalmente gerenciado com Google Cloud Platform*__

O desafio consiste em efetuar um processamento de dados utilizando o produto Dataproc do GCP. Esse processamento irá efetuar a contahem das palavras de um livro e informar quantas vezes cada palavra aparece no mesmo.

---

### Etapas do Desafio

1. Criar um bucket no Cloud Storage
    Como: Na sua conta do cloud, (local que você pode colocar código,o nome é único dentro do Cloud) 

    Cloud Storage->
    Cricar em criar intervalo (no caso de idioma em português) 
    Informar o nome (Precisa ser único dentro do cloud);
    Deixar o resto como padrão (nesse teste por ser um teste)

1.2 Criar o cluster (caso não exista,segui a video aula)  

1.3 Ir para o datapro/cluster, abrir o power shell
    copiar os arquivos do github disponibilizado para fazer o upload 
    > git clone https://github.com/MarcoSena2210/dio-desafio-dataproc-gcp-ms.git
    (endereço do git) 
    >ls (para verificar se baixou)
    ir para pasta 
    >cd dio-desafio-dataproc-gcp-ms

2. Atualizar o arquivo ```contador.py``` com o nome do Bucket criado nas linhas que contém ```{SEU_BUCKET}```.
    Caso seja editado o arquivo no power shel do dataproc 
    2.1-Abrir o arquivo com o editor vim
    >vim contador.py
    substituir {SEU_BUCKET} pelo seu, sem as chaves,salvar a edição (:wq ,salva e sai)
    verificando se ficou correto 
    >cat contador.py 



3. Fazer o upload dos arquivos ```contador.py``` e ```livro.txt``` para o bucket criado (instruções abaixo)
     Verificando o nome do bukcet existentes;
     >gsutil ls       
        Exibiu:     
        gs://dataproc-staging-us-central1-683218558323-k692hxer/  (Criado automaticamente pelo dataproc)
        gs://dataproc-temp-us-central1-683218558323-fyi6bqbv/     (Criado automaticamente pelo dataproc)
        gs://desafio-dataproc-ms/                                 (Criado criado manualmente pelo analista)  

     Copiando os arquivos:
     Primeiro ir para pasta onde foi feito o ulpoad
     >cd dio-desafio-dataproc-gcp-ms
     Copiar para o bucket
     >gsutil cp contador.py livro.txt gs://desafio-dataproc-ms (Irá solicitar autorização, autorizar)

    - https://cloud.google.com/storage/docs/uploading-objects



1. Utilizar o código em um cluster Dataproc, executando um Job do tipo PySpark chamando ```gs://{SEU_BUCKET}/contador.py```

    Ao rodar pelo inreface web deu um erro que pode ser visto no arquivo: mensage_erro.png
    Após entrar em contato como o professor Marcelo e seguir suas orientações foi resolvido após alterar via linha de comando a region conforme coamndo:

    ### OBS: Houve um erro que não perimitia localizar a região 
    ### setando a região, provável motivo pelo qual não estava rodando. 
    >gcloud config set dataproc/region us-central1  


1. O Job irá gerar uma pasta no bucket chamada ```resultado```. Dentro dessa pasta o arquivo ```part-00000``` irá conter a lista de palavras e quantas vezes ela é repetida em todo o livro.

### Entrega do Resultado

1. Criar um repositório no GitHub.

2. Criar um arquivo chamado ```resultado.txt```. Dentro desse arquivo, colocar as 10 palavras que mais são usadas no livro, de acordo com o resultado do Job.

3. Inserir os arquivo ```resultado.txt``` e ```part-00000``` no repositório e informar na plataforma da Digital Innovation One.
