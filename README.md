# Projeto DataBricks:
Notebooks Vendidos

#### Quais fatores afetam os preços dos computadores portáteis?

* Vários fatores diferentes podem afetar os preços dos laptops. Esses fatores incluem a marca do computador e o número de opções e complementos incluídos no pacote do computador. Além disso, a quantidade de memória e a velocidade do processador também podem afetar o preço. Embora menos comum, alguns consumidores gastam dinheiro adicional para comprar um computador com base na “aparência” geral e no design do sistema.

* Em muitos casos, os computadores de marca são mais caros do que as versões genéricas. Esse aumento de preço geralmente tem mais a ver com o reconhecimento do nome do que com qualquer superioridade real do produto. Uma grande diferença entre os sistemas de marca e genéricos é que, na maioria dos casos, os computadores de marca oferecem melhores garantias do que as versões genéricas. Ter a opção de devolver um computador com defeito costuma ser um incentivo suficiente para encorajar muitos consumidores a gastar mais dinheiro.

* A funcionalidade é um fator importante na determinação dos preços dos laptops. Um computador com mais memória geralmente funciona melhor por mais tempo do que um computador com menos memória. Além disso, o espaço no disco rígido também é crucial, e o tamanho do disco rígido geralmente afeta os preços. Muitos consumidores também podem procurar drivers de vídeo digital e outros tipos de dispositivos de gravação que possam afetar os preços dos laptops.

* A maioria dos computadores vem com algum software pré-instalado. Na maioria dos casos, quanto mais software for instalado em um computador, mais caro ele será. Isso é especialmente verdadeiro se os programas instalados forem de editores de software bem estabelecidos e reconhecíveis. Aqueles que estão pensando em comprar um novo laptop devem estar cientes de que muitos dos programas pré-instalados podem ser apenas versões de teste e expirarão dentro de um determinado período de tempo. Para manter os programas, será necessário adquirir um código e, em seguida, fazer o download de uma versão permanente do software.
* Muitos consumidores que estão comprando um novo computador estão comprando um pacote completo. Além do próprio computador, esses sistemas normalmente incluem um monitor, teclado e mouse. Alguns pacotes podem até incluir uma impressora ou câmera digital. O número de extras incluídos em um pacote de computador geralmente afeta os preços dos laptops.

* Alguns líderes da indústria de fabricação de computadores tornam um ponto de venda oferecer computadores em estilo elegante e em uma variedade de cores. Eles também podem oferecer um design de sistema incomum ou contemporâneo. Embora isso seja menos importante para muitos consumidores, para aqueles que valorizam a “aparência”, esse tipo de sistema pode valer o custo extra.

#### De onde eu consegui esses dados?

* Extraiu esses dados de flipkart.com
* usou uma ferramenta automatizada de extensão da Web do Chrome chamada Instant Data Scrapper
* recomendo que você use esta bela ferramenta para obter os dados de qualquer lugar na web. é muito fácil de usar, nenhum conhecimento de codificação é necessário.

#### O que você pode fazer?
* Visualize esses dados e prepare gráficos de alta qualidade o máximo que puder.

* Construir um modelo para prever o preço

* Descrição das colunas: consulte a seção de colunas de dados.



## Análise Descritiva SQL


### Exploração/Desenvolvimento

alter view vw_notebooks_vendidos 
as 
select *,(ultimo_preco * 0.063) as preco_atual_real,
(preco_antigo * 0.063) as preco_anterior_real,
(desconto/100) as desconto_
from notebooks_vendidos

select * from vw_notebooks_vendidos
.

##### Média de Preço das Marcas
select
case when marca = 'lenovo' then 'Lenovo' 
     else marca 
end as marca_ajustada,
avg(preco_atual_real) as media_preco_atual
from vw_notebooks_vendidos 
group by case when marca = 'lenovo' then 'Lenovo' 
     else marca 
end 
order by 2 desc
%sql WITH q AS (select
case when marca = 'lenovo' then 'Lenovo' 
     else marca 
end as marca_ajustada,
avg(preco_atual_real) as media_preco_atual
from vw_notebooks_vendidos 
group by case when marca = 'lenovo' then 'Lenovo' 
     else marca 
end 
order by 2 desc) SELECT `marca_ajustada`,SUM(`media_preco_atual`) `column_8c15775e2` FROM q GROUP BY `marca_ajustada`
![newplot](https://user-images.githubusercontent.com/86385596/214394947-97f77d1a-1f06-4938-b65b-5fad9eef3f44.png)



###### Participação da Memórias(DDR3, DDR4 e DDR5)
select
case when ram_type = 'LPDDR3' then 'DDR3'
     when ram_type in ('LPDDR4','LPDDR4X') then 'DDR4'
else ram_type end as tipo_memoria,
avg(preco_atual_real) as media_preco_atual
from vw_notebooks_vendidos 
group by

case when ram_type = 'LPDDR3' then 'DDR3'
     when ram_type in ('LPDDR4','LPDDR4X') then 'DDR4'
else ram_type end

order by 2 desc
![plot3](https://user-images.githubusercontent.com/86385596/214395050-d1e4b1ce-8582-4a57-b922-39a0794853ff.png)

.


###### Tipo de Memória com Mais Vendas (DDR3, DDR4 e DDR5)

select
case when ram_type = 'LPDDR3' then 'DDR3'
     when ram_type in ('LPDDR4','LPDDR4X') then 'DDR4'
else ram_type end as tipo_memoria,
sum(preco_atual_real) as media_preco_atual
from vw_notebooks_vendidos 
group by

case when ram_type = 'LPDDR3' then 'DDR3'
     when ram_type in ('LPDDR4','LPDDR4X') then 'DDR4'
else ram_type end

order by 2 desc
%sql WITH q AS (select
case when ram_type = 'LPDDR3' then 'DDR3'
     when ram_type in ('LPDDR4','LPDDR4X') then 'DDR4'
else ram_type end as tipo_memoria,
sum(preco_atual_real) as media_preco_atual
from vw_notebooks_vendidos 
group by

case when ram_type = 'LPDDR3' then 'DDR3'
     when ram_type in ('LPDDR4','LPDDR4X') then 'DDR4'
else ram_type end

order by 2 desc) SELECT `tipo_memoria`,SUM(`media_preco_atual`) `column_8c15775e4` FROM q GROUP BY `tipo_memoria`
![newplot (1)](https://user-images.githubusercontent.com/86385596/214394940-094828e9-94fa-4295-873d-1c35e7e865fd.png)

