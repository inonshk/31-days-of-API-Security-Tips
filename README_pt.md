# 31 dias de dicas de segurança de API

### Este desafio são as dicas de segurança da API de 31 dias da Inon Shkedy

#### -API TIP: 1/31-

*As versões mais antigas das APIs tendem a ser mais vulneráveis e não possuem mecanismos de segurança.
Aproveite a natureza previsível das APIs REST para encontrar versões antigas.
Veja uma chamada para `api/v3/login` e verifique se  `api/v1/login` também existe. Pode ser mais vulnerável.*

--------------------------------------------------------------------------------------------------------------------------

#### -API TIP: 2/31-

*Nunca assuma que há apenas uma maneira de se autenticar em uma API!
Aplicativos modernos têm muitos endpoints da API para autorização: `/api/mobile/login` | `/api/v3/login` | `/api/magic_link`; etc ..
Encontre e teste todos eles para encontrar problemas de autorização.*

--------------------------------------------------------------------------------------------------------------------------

#### -API TIP:3/31-

*Lembra quando SQL Injections costumavam ser extremamente comuns 5 a 10 anos atrás, e mesmo assim você poderia invadir quase todas as empresas?
BOLA (IDOR) é a nova epidemia de segurança de API.
Como pentester, se você entender como explorá-lo, o sucesso é garantido.*

> Saiba mais sobre o BOLA: [https://medium.com/@inonst/a-deep-dive-on-the-most-critical-api-vulnerability-bola-1342224ec3f2](https://medium.com/@inonst/a-deep-dive-on-the-most-critical-api-vulnerability-bola-1342224ec3f2)
--------------------------------------------------------------------------------------------------------------------------

#### -API TIP: 4/31-

Testando um aplicativo Ruby on Rails e achou um parâmetro HTTP que contém uma URL?
Às vezes, os desenvolvedores usam a função "Kernel#open" para acessar URLs == Game Over.
Basta enviar um pipe como o primeiro caractere e depois um comando shell (Command Injection por design)

> Saiba mais sobre open function: [https://apidock.com/ruby/Kernel/open](https://apidock.com/ruby/Kernel/open)
--------------------------------------------------------------------------------------------------------------------------

#### -API TIP:5/31-

*Achou SSRF (Server-side request forgery) ? Use-o para:*
* Varredura de portas internas
* Aproveite os serviços em nuvem (como 169.254.169.254)
* Use http://webhook.site para revelar o endereço IP e as bibliotecas HTTP
* Faça o download de um arquivo muito grande (camada 7 DoS)
* SSRF reflexivo? descubra os gerenciamentos de consoles locais

--------------------------------------------------------------------------------------------------------------------------

#### -API TIP: 6/31-

*Mass Assignment é algo real.
Os frameworks modernos incentivam os desenvolvedores a usar o MA sem entender as implicações de segurança.
Durante a exploração, não adivinhe os nomes das propriedades do objeto, basta encontrar um endpoint GET que retorne todos eles.*

![Infographic](https://pbs.twimg.com/media/ENpsW25XYAAjEJE?format=jpg)

--------------------------------------------------------------------------------------------------------------------------

#### - API TIP: 7/31 -

*Uma empresa expõe uma API para desenvolvedores?
Esta não é a mesma API usada pelo aplicativo móvel / web. Sempre teste-os separadamente.
Não pense que eles implementam os mesmos mecanismos de segurança.*

--------------------------------------------------------------------------------------------------------------------------

#### - API TIP: 8/31 -

Pentest para API REST? Dê uma chance e verifique se a API também suporta SOAP.
Altere o content-type para "application/xml", adicione um XML simples no request body e veja como a API lida com isso.

> Às vezes, a autenticação é feita em um componente diferente que é compartilhado entre APIs REST e SOAP == API SOAP pode suportar JWT

> Se a API retornar o stack trace com um DUMPling, provavelmente será vulnerável **
 
--------------------------------------------------------------------------------------------------------------------------

#### - API TIP: 9/31 -

*Pentest para APIs? Tentando encontrar vulnerabilidades do BOLA (IDOR)? 
Os IDs nos HTTP bodies/headers tendem a ser mais vulneráveis que os IDs nas URLs. 
Tente se concentrar neles primeiro.*

--------------------------------------------------------------------------------------------------------------------------

#### -API TIP: 10/31-

*Explorando o BFLA (Broken Function Level Authorization)?
Aproveite a natureza previsível do REST para encontrar endpoints da API do administrador!
Por exemplo: você viu a seguinte chamada de API `GET /api/v1/users/<id>`
Dê uma chance e mude para `DELETE / POST para criar / excluir usuários`.*

--------------------------------------------------------------------------------------------------------------------------

#### - API TIP: 11/31 - 

*A API usa o Authorization header? Esqueça o CSRF!
Se o mecanismo de autenticação não suportar cookies, a API será protegida contra CSRF por design.*

--------------------------------------------------------------------------------------------------------------------------

#### -API TIP : 12/31-

*Teste para BOLA (IDOR)?
Mesmo se o ID for GUID ou não numérico, tente enviar um valor numérico.
Por exemplo: `/?user_id=111` em vez de` user_id=inon@traceable.ai`
Às vezes, o mecanismo de autorização suporta ambos e é mais fácil fazer força bruta com números.*

--------------------------------------------------------------------------------------------------------------------------

#### -API TIP: 13/31-

*Use Mass Assignment para ignorar os mecanismos de segurança.
Por exemplo, mecanismo "inserir senha":
- `POST /api/rest_pass` requer senha antiga.
- `PUT /api/update_user` é vulnerável ao MA == pode ser usado para atualizar a senha sem enviar a antiga (para CSRF)*

--------------------------------------------------------------------------------------------------------------------------

#### - API TIP: 14/31 -

*Ficou travado durante um teste de API? Expanda sua superfície de ataque! Encontre subdomínios / irmãos usando http://Virustotal.com e http://Censys.io.
Alguns desses domínios podem expor as mesmas APIs com diferentes configurações / versões.*

--------------------------------------------------------------------------------------------------------------------------

#### -API TIP:15/31-

*Recursos estáticos == fotos, vídeos, ..
Servidores Web (IIS, Apache) tratam recursos estáticos de maneira diferente quando se trata de autorização.
Mesmo que os desenvolvedores implementem uma autorização decente, há uma boa chance de você acessar recursos estáticos de outros usuários.*

--------------------------------------------------------------------------------------------------------------------------

#### -API TIP: 16/31-

Mesmo se você usar outro proxy da web, sempre use Burp em segundo plano.
Os caras da @PortSwigger estão fazendo um trabalho muito bom em ajudá-lo a gerenciar o seu pentest.
Use o recurso "tree view" (versão gratuita) para ver todos os endpoints da API que você acessou.

--------------------------------------------------------------------------------------------------------------------------

#### -API TIP:17/31-

*Mobile Certificate Pinning?
Antes de iniciar a engenharia reversa e aplicar patches no aplicativo cliente, verifique os clientes iOS e Android e versões mais antigas deles.
Há uma boa chance de que o pinning não esteja ativado em um deles. Economize tempo.*

--------------------------------------------------------------------------------------------------------------------------

#### -API TIP: 18/31-

*Empresas e desenvolvedores tendem a colocar mais recursos (incluindo segurança) nas principais APIs.
Sempre procure os recursos mais específicos que ninguém usa para encontrar vulnerabilidades interessantes.
`POST /api/profile/upload_christmas_voice_greeting`*

--------------------------------------------------------------------------------------------------------------------------

#### -API TIP:19/31-

*Quais recursos você acha que tendem a ser mais vulneráveis?*
*Vou começar:*
* Gerenciamento de usuários da organização
* Exportar para CSV / HTML / PDF
* Visualizações personalizadas de painéis
* Criação e gerenciamento de usuários
* Compartilhamento de objetos (fotos, postagens, etc)

--------------------------------------------------------------------------------------------------------------------------

#### - API TIP:20/31- 

*Testando APIs de autorização?
Se você testar na produção, há uma boa chance dos endpoints de autorização terem proteção contra força bruta.
De qualquer forma, os engenheiros de DevOps tendem a desativar o rate limit em ambientes que não são de produção. 
Não se esqueça de testá-los :)*

> Um bom exemplo desse problema: falha do Facebook (encontrado por @sehacure) [http://www.anandpraka.sh/2016/03/how-i-could-have-hacked-your-facebook.html](http://www.anandpraka.sh/2016/03/how-i-could-have-hacked-your-facebook.html)
--------------------------------------------------------------------------------------------------------------------------

#### -API TIP:21/30-

*Ficou preso durante um teste de API? Expanda a superfície de ataque!
Use http://archive.com, encontre versões antigas do aplicativo Web e explore novos endpoints da API.
Não pode usar o cliente? Verifique os arquivos .js nas URLs. Alguns deles são endpoints da API. *

--------------------------------------------------------------------------------------------------------------------------

#### -API TIP:22/31-

*As APIs tendem a vazar PII (Personally Identifiable Information) por design.
Os engenheiros de back-end retornam objetos JSON brutos e confiam nos engenheiros de front-end para filtrar dados confidenciais.
Encontrou um recurso confidencial (por exemplo, `recibo`)? Encontre todos os endpoints que retornam: `/download_receipt`,`/export_receipt`, etc..*

> Alguns endpoints podem vazar dados excessivos que não devem ser acessíveis pelo usuário.

> Este é um exemplo dos Top 10 OWASP para APIs - #3 - Exposição excessiva a dados
--------------------------------------------------------------------------------------------------------------------------

#### -API TIP:23/31-

*Encontrou uma maneira de baixar arquivos aleatórios de um servidor web?
Mude o teste de caixa preta para caixa branca.
Baixe o código fonte do aplicativo (arquivos DLL: use IL-spy; Java compilado - use Luyten)
Leia o código e encontre novos problemas!*

--------------------------------------------------------------------------------------------------------------------------

#### -API TIP:24/31-

*Ficou travado durante um teste de API? Expanda sua superfície de ataque!
Lembre-se: os desenvolvedores geralmente desativam os mecanismos de segurança em ambientes que não são de produção (QA / staging / etc);
Aproveite esse fato para ignorar autorização, rate limit e validação de entrada.*

--------------------------------------------------------------------------------------------------------------------------

#### -API TIP:25/31-

*Encontrou um recurso "exportar para PDF"?
Há uma boa chance dos desenvolvedores usarem uma biblioteca externa para converter HTML -> PDF no background.
Tente injetar elementos HTML e causar "Export Injection".*

> Aprender mais sobre Export Injection: [https://medium.com/@inonst/export-injection-2eebc4f17117](https://medium.com/@inonst/export-injection-2eebc4f17117) 
--------------------------------------------------------------------------------------------------------------------------

#### -API TIP:26/31-

*Procurando por BOLA (IDOR) nas APIs? obteve erros 401/403?
Truques para burlar autorização: *
* Enrole a ID com um array` {"id": 111}` --> `{"id": [111]} `
* JSON wrap `{"id":111}` --> `{"id":{"id":111}}`
* Enviar ID duas vezes `URL?id=<LEGITIMO>&id=<VITIMA>`
* Enviar curinga `{"user_id":"*"}`
 
> Em alguns casos, o mecanismo de autorização espera uma sequência simples (um ID neste caso) e, se receber um JSON, não executará as verificações de autorização.Em seguida, quando a entrada for para o componente de busca de dados, pode haver um JSON em vez de uma string.
--------------------------------------------------------------------------------------------------------------------------

#### -API TIP:27/31-

*Os servidores de back-end não são mais responsáveis pela proteção contra o XSS.
APIs não retornam HTML, mas JSON.
Se a API retornar o payload do XSS? -
Por exemplo: `{"name":"In<script>alert(21)</script>on} `
Isso é bom! A proteção sempre precisa estar do lado do cliente*

--------------------------------------------------------------------------------------------------------------------------

#### -API TIP:28/31-

*Pentest para aplicativos .NET? Encontrou um parâmetro que contém o caminho / nome do arquivo? 
Às vezes, os desenvolvedores usam "Path.Combine(path_1, path_2)" para criar o caminho completo. 
Path.Combine tem um comportamento estranho: se o parâmetro 2 for caminho absoluto, o parâmetro 1 será ignorado.*
##### Utilize-o para controlar o caminho

> Saiba mais: [https://www.praetorian.com/blog/pathcombine-security-issues-in-aspnet-applications](https://www.praetorian.com/blog/pathcombine-security-issues-in-aspnet-applications)
--------------------------------------------------------------------------------------------------------------------------

#### -API TIP:29/30-

*As APIs expõem a implementação fundamental do aplicativo.
Os pentesters devem aproveitar esse fato para entender melhor usuários, funções, recursos e correlações entre eles e encontrar vulnerabilidades e exploits.
Sempre tenha curiosidade sobre as respostas da API. *

--------------------------------------------------------------------------------------------------------------------------

#### -API TIP:30/31-

*Ficou travado durante um teste de API? Expanda sua superfície de ataque!
Se a API tiver clientes móveis, faça o download de versões antigas do arquivo APK para explorar a funcionalidade antiga / herdada e descobrir novos endpoints da API.*

> Lembre-se: as empresas nem sempre implementam mecanismos de segurança desde o primeiro dia, e os engenheiros do DevOps nem sempre depreciam as APIs antigas. 
Aproveite esses fatos para encontrar endpoints da API escondidas que não implementam mecanismo de segurança (autorização, filtragem de entrada e rate limit)

> Baixe versões antigas do APK de aplicativos para Android: [https://apkpure.com](https://apkpure.com)
--------------------------------------------------------------------------------------------------------------------------

#### -API TIP: 31/31-

*Encontrou um parâmetro `limit` /` page`? (por exemplo: `/api/news?limit=100`) Pode ser vulnerável ao DoS da camada 7. 
Tente enviar um valor longo (por exemplo: `limit=999999999`) e veja o que acontece:)*

--------------------------------------------------------------------------------------------------------------------------

## Fonte

#### Todas as informações são retiradas do twitter de *Inon Shkedy*

##### Links:
 
* [Inon Shkedy](https://twitter.com/inonshkedy)
* [Traceableai](https://twitter.com/traceableai/)
* [OWASP API PROJECT](https://github.com/OWASP/API-Security)
