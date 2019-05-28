<h2>Caso 1</h2>
<p>Na loja CasaVeg ao add um produto ao carrinho (Ajax Cart) ocorriam alguns problemas como:</p>
<ol>
<li>Carrinho Vazio</li>
<li>Carrinho contendo produtos que não foram adicionados pelo cliente (produtos a mais).</li>
</ol>
<h3>SOLUÇÃO:</h3>
<p>Abrir em paralelo as tabelas <em>ps_orders</em> e <em>ps_cart</em>.<br />
Ordernar a coluna "id_cart" em ambas "decrecentemente" e comparar o <b>maior ID</b>.<br />
O maior ID da <em>ps_orders</em> deve ser menor que o maior id da <em>ps_cart</em>.<br />
Caso não seja, em alguns casos, o Prestashop vai atribuir pedidos de carrinhos antigos ao carrinho novo pelo simples fato de a nova order tem o mesmo ID ANTIGO.<br />
Limpe a tabela <em>ps_cart</em> e abra o Comando SQL e execute: </li>
</p>
<pre>
ALTER TABLE ps_cart AUTO_INCREMENT = ValorAcimaDoIdCartDaTabelaPS_Orders;
</pre>
<p>Feito isso você terá SETADO o tabela ps_cart para gerar sua próxima row acima dos valores antigos, evitando duplicidade e conflito de informação.</p>