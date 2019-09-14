<p>Prestashop possui recursos de segurança rigorosos.</p>
<p>Um desses recursos é o <b>tempo limite da sessão</b>. Isso é para reduzir a exposição da sua aplicação a ataques baseados em sessões, como roubo de cookies de sessão.</p>
<p>No entanto, isso pode causar problemas, mesmo para usuários legítimos. Os administradores de loja podem ser expulsos da interface do administrador se permanecerem inativos (por exemplo, participando de uma chamada) no meio de uma atualização da loja. Pode ser muito frustrante.</p>
<p>Hoje, vamos discutir quando vemos esse erro, por que e como podemos corrigi-lo.</p>
<h3>Problema no login do Prestashop admin - Onde você vê esse erro?</h3>
<p>As 3 situações de erros mais citadas pelos administradores do prestashop são:</p>
<ol>
<li>O painel de adm do Prestashop expulsa o administrador no meio das configurações do produto (sem motivo).</li>
<li>O proprietário da loja Prestashop não pode fazer login, não importa quantas vezes o cache do navegador seja limpo. Ele continua mostrando a página de login novamente e novamente.</li>
<li>O painel de administração desconecta o proprietário após alguns minutos de inatividade.</li>
</ol>
<h3>Os 3 principais motivos para o problema de login no administrador do Prestashop</h3>
<ol>
<li><b>Duração máxima do tempo de inatividade - "Admin Controller"</b> gerencia as funcionalidades do Backoffice no Prestashop. O período padrão de inatividade do cookie é definido como 15 minutos(900sec) neste arquivo. Você será expulso do painel do administrador após 15 minutos de inatividade.</li>
<li><b>Uso de endereço IP dinâmico</b> - Quando você está no painel de administração do Prestashop, ele protege a sessão, marcando sua sessão de login com seu endereço IP (via cookie de autenticação). Ele verifica constantemente esse endereço IP. Se o seu endereço IP mudar, ele invalidará o cookie e solicitará que você faça login novamente.</li>
<li><b>Valores incorretos para "PS_SHOP_DOMAIN" e "PS_SHOP_DOMAIN_SSL"</b> - Nome de domínio incorreto fornecido para PS_SHOP_DOMAIN e PS_SHOP_DOMAIN_SSL na tabela ps_configuration.
</ol>
<h3>Problema no login do administrador do Prestashop - Como corrigir este erro?</h3>
<p>Para corrigir isso, usamos principalmente 5 maneiras diferentes, com base no problema exato que o proprietário da loja está enfrentando.</p>
<p>Porém, antes de qualquer coisa, é importantíssimo que seja feito um backup dos arquivos a serem mexidos tal como as tabelas do banco de dados.</p>
<h3>1. Limpe o cache e os cookies do navegador</h3>
<p>Para verificar isso, tente acessar de outro navegador ou ativar o "modo de navegação anônima".</p>
<h3>2. Limpe o cache do Prestashop</h3>
<p>Vá para essas pastas e exclua todos os arquivos nelas.</p>
<p>/tools/smarty/cache ou /tools/smarty_v2/cache</p>
<p>ools/smarty/compile ou /tools/smarty_v2/compile</p>
<h3>3. Corrija o nome do domínio salvo no banco de dados</h3>
<p>Dê o nome de domínio correto para PS_SHOP_DOMAIN e PS_SHOP_DOMAIN_SSL na tabela ps_configuration.</p>
<p>Você deve fornecer apenas o nome de domínio. Por exemplo: o URL da sua loja é http://test.com/store/, você deve fornecer os valores como:<p>
<p><pre>PS_SHOP_DOMAIN = test.com<br />PS_SHOP_DOMAIN_SSL = test.com</pre></p>
<p>O diretório de instalação deve ser fornecido no arquivo "/config/setting.inc.php".</p>
<h3>4. Desativar verificação de endereço IP</h3>
<p>Remova a verificação do endereço IP do usuário feita pelo Prestashop.</p>
<p>Você pode desativá-lo no arquivo "classes/cookie.php" dentro da função "isLoggedBack()".</p>
<p>Aqui, remova ou comente a seguinte condição.</p>
<p><pre>!Configuration::get('PS_COOKIE_CHECKIP'))</pre></p>
<h3>5. Aumente o período de inatividade do cookie<h3>
<p>O período de inatividade é definido como 15 minutos por padrão.<br />
Você pode aumentar esse valor no arquivo "classes/controller/AdminController.php".</p>
<p>Procure o código abaixo no arquivo:</p>
<p><pre>if (time $ this->Context>cookie->last_activity + 900 <())</pre></p>
<p>Aqui, o período de inatividade é definido como 900s (15 minutos). Você pode substituir esse valor em segundos.</p>
<h3>Conclusão</h3>
<p>O problema de login do administrador do Prestashop é um problema comum que os proprietários das lojas podem encontrar.</p>
