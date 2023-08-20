TIPOS DE DADOS DO PROMETHEUS


Gauge: 
O tipo de dado gauge é o tipo de dado utilizado para criar métricas que podem ter seus valores alterados para cima ou para baixo, por exemplo, a ultilização de memória ou cpu. 
Um exemplo de métrica do tipo gauge é a métrica memory_usage, que é uma métrica que mostra a utilização de memória.
memory_usage{instance="localhost:8899",job="Meu Primeiro Exporter"}

Counter: 
O tipo de dado counter é o tipo de dado utilizado que vai ser incrementado no decorrer do tempo, por exemplo, quando queremos contar o número de requisições com status 200, para uma aplicação, no decorrer da última hora. O valor atual do counter quase nunca é importante, pois o que queremos dele são os valores durante uma janela de tempo, como por exemplo, quantas vezes uma determinada aplicação falhou durante um final de semana. Normalmente as métricas counter possuem o sufixo _total, para indicar que é o total de valores que foram contados, como por exemplo:
requests_total{instance="localhost:8899",job="Meu Primeiro Exporter"}

Histogram: 
O tipo de dado histogram é o tipo de dado que te permite especificar o seu valor através de buckets predefinidos, por exemplo, o tempo de execução de uma aplicação. Com o histogram, conseguimos contar todas as requisições que minha aplicação respondeu entre 0 e 0,5 segundos, ou então, as requisições que tiveram respostas entre 1,0 e 2,5 e assim por diante. Por padrão, os buckets predefinidos são até no máximo 10 segundos, mas se quisermos mais, podemos criar os nossos próprios buckets personalizados. Algo importante a mencionar, é que o Prometheus irá contar cada item em cada bucket, e também a soma dos valores. Uma métrica do tipo histogram, inclui alguns itens importantes, que são adicionados ao final do nome da métrica, para indicar o tipo de dado e o tamanho do bucket, como por exemplo:
requests_duration_seconds_bucket{le="0.5"}

Summary:
O tipo de dado summary é bem parecido com o histogram, com a diferença que os buckets aqui são chamados de quantiles, sendo definidos por um valor entre 0 e 1, ou seja, o valor do bucket é o valor que está entre os quantiles.
Da mesma forma como no histogram, podemos criar métricas do tipo summary, com alguns itens importantes adicionados ao final do nome da métrica, como por exemplo:
requests_duration_seconds_sum{instance="localhost:8899",job="Meu Primeiro Exporter"}
