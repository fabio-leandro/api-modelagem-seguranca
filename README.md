<h1>Notas sobre Modelagem e Segurança de APIs</h1>

<h3>O que é API?</h3>
        <p>APIs são Interfaces que permite a comunicação entre aplicações sem que precise saber os detalhes por trás do desenvolvimento de determinada API.</p>
        <p>Uma API funcionando com um cliente fazendo uma requisição a essa API. Então, ela faz a busca no servidor e retorna uma resposta.</p>
        <p>Um exemplo de API é o GOOGLE MAPS.</p>
        <p>Uma API facilita a comunicação entre aplicações porque há ganho de agilidade e compatibilidade.</p>
        <p>As APIs pode ser do tipo pública ou privada.</p>
        
 <h3>1 - Sobre Modelagem de APIS</h3>
        <p>O mercado utiliza dominantemente APIs com o conceito REST e a comunicação via protocolo HTTP.</p>
        <p>REST (Representational State Transfer) define princípios arquiteturais para a comunicação entre cliente e servidor.</p>
        <p>O HTTP (HyperText Markup Language) funciona como um protocolo de requisição-resposta no modelo computacional cliente-servidor.</p>
        <p>Uma API/RESTFUL é aquela que foi implementada seguindo todas as boas práticas do protocolo REST.</p>
        
 <h3>1.1	– Métodos Seguros e Métodos Idempotentes</h3>
        <p>Um método é seguro se ele for utilizado apenas para operações de leitura, tais como o GET, HEAD e OPTIONS. Não se espera que seja feito qualquer tipo de alteração no    estado do servidor ao realizar uma requisição a estes métodos.</p>
        <p>Um método é considerado idempotente se os efeitos colaterais de uma ou mais requisições idênticas forem iguais a uma única requisição.</p>
        
<img src="https://miro.medium.com/max/365/0*DpdbJdENtF_LuaNM.png">
        <cite><a href="https://medium.com/@ramonrune/arquitetando-uma-api-restful-8ffcf892586a">Fonte: https://medium.com</a></cite>
        
 <h3>1.2 - Modelo de Maturidade de Richardson</h3>
        <p>Leonard Richardson fez uma análise em centenas de API's diferentes. E dividiu em quatro categorias para identificar o nível de maturidade da API com base no quanto eles são compatíveis com REST.</p>
        <p>Ele utilizou três fatores. URI, HTTP, HATEOAS (Hypermedia).</p>

<img src="https://miro.medium.com/max/673/0*TJCnow0Iq8NInxbb.png">

<h3>1.2.1 - Nível 0</h3>
        <p>Nesse nível pode se dizer que são utilizados os verbos HTTP, mas sem respeitar as regras do padrão REST. Como no quadro abaixo os verbos HTTP não correspondem com a URI.</p>
        <img src="https://miro.medium.com/max/700/1*4pgZ-uzVa734XE5KmBBu9A.png">
 <h3>1.2.2 – Nível 1</h3>
        <p>Nesse nível os recursos já correspondem com os verbos. Os recursos são representados por substantivos no plural.</p>
        <img src="https://miro.medium.com/max/700/1*YMrDthJ9-S5zXlVfofMq1g.png">
  <h3>1.2.3 – Nível 2</h3>
        <p>No nível 2 os verbos HTTP são usados de forma correta. Os verbos mais utilizados são GET, POST, PUT e DELETE.</p>
        <img src="https://miro.medium.com/max/700/1*uPNw5I9AJCZsYPvSgQN-NA.png">      
 <h3>1.2.4 – Nível 3</h3>
        <p>Para o HATEOAS, uma API que implementa esse nível fornece aos seus clientes links que indicarão como poderá ser feita a navegação entre seus recursos.</p>
        <img src="https://miro.medium.com/max/633/1*g-_jI5oc-7tD9K78FEahiw.png">
       
<h3>1.3	– Dicas para melhores práticas para o desenvolvimento de uma API RESTFUL</h3>
        <p>O Recurso deve ser escrito no substantivo. Referente a plural e singular, deve seguir o padrão em todo o projeto. Se usar no singular, que seja feito em todo o projeto. Os recursos devem ser descritivos e fáceis de entender.</p>
        
<dl>
            <dd>GET /clientes — Lista os clientes.</dd>
            <dd>GET /clientes/1 — Obtém os dados do cliente 1.</dd>
            <dd>POST /clientes — Cria um novo cliente.</dd>
            <dd>PUT /clientes/1 — Altera o cliente 1.</dd>
            <dd>DELETE /clientes/1 — Remove o cliente 1.</dd>
            <dd>PATCH /clientes/1 — Atualiza parcialmente o cliente 1.</dd>
        </dl>
 
 <p>Utilize no máximo um encadeamento de 3–4 recursos no máximo. Isso para facilitar a compreensão.</p>

   <dl>
            <dd>GET /clientes/1/parceiros — Lista os parceiros do cliente 1.</dd>
            <dd>GET /clientes/1/parceiros/1 — Lista o parceiro 1 do cliente 1.</dd>
        </dl>

   <p>A documentação precisa ser fácil de encontrar, compreensível ao desenvolvedor, fácil de testar e informar o seu propósito específico.</p>
        <p>É uma boa prática sempre versionar. Pode se utilizar o versionamento na URI do recurso:</p>
        <dl>
            <dd>GET /v1/clientes</dd>
            <dd>POST /v1/clientes</dd>
            <dd>GET /v1/public/characters</dd>
            <dd>GET/v1/public/characters/1</dd>
        </dl>
 <p>Onde for permitido, é recomendado utilizar JSON para as respostas. JSON é um formato amplamente utilizado na Web, os arquivos JSON usam 30% menos banda do que arquivos XML.</p>
        <p>As pessoas acessam APIs de diversos locais (shoppings, em casa, aeroportos, bancos, restaurantes, etc). Devemos tomar cuidado, pois nunca se sabe se não há ninguém interceptando as mensagens. Não deixe as pessoas acessaram sua API sem o uso de HTTPS.</p>
        <p>Em situações de busca, filtro, ordenação, status, paginação é interessante usar QUERY PARAMS.</p>
        <dl>
            <dd>GET /clientes?ativo=true</dd>
        </dl>
 
 <p>Logs auxiliam no processo de debug da API.</p>
        <p>As métricas que são geradas pela API também são importantes para analisar se essa API está sendo usada corretamente ou identificar possíveis melhorias.</p>
        <p>Mensagens de retorno descritivas podem auxiliar o cliente no consumo da API.</p>
        <p>Ao estruturar uma API, é interessante dividi-la em camadas. Cada camada terá sua responsabilidade específica. Um modelo a ser seguido pode ser:</p>
        <dl>
            <dd><b>Camada de persistência de dados: </b>Controla banco de dados.</dd>
            <dd><b>Camada de serviço/negócios: </b>Contém as lógicas de negócio.</dd>
            <dd><b>Camada de recurso: </b>Realiza a exposição dos recursos.</dd>
        </dl>
 
 <p>Para dados que não mudam frequentemente e não são sensíveis a erro, é interessante a utilização de caches para otimizar a performance de sua API.</p>
        <p>Formas de realizar autenticação, como por exemplo:</p>
        <dl>
            <dd>Sem autorização.</dd>
            <dd>Bearer Token.</dd>
            <dd>Basic Auth.</dd>
            <dd>Digest Auth.</dd>
            <dd>OAuth 1.0.</dd>
            <dd>OAuth 2.0</dd>
            <dd>Hawk Authentication.</dd>
            <dd>AWS Signature.</dd>
            <dd>Dentre outros mecanismos.</dd>
        </dl>
    
 <p>No caso de retornar uma grande quantidade de dados, uma boa prática é a realização de paginação.</p>
        <p>Na paginação, podemos passar alguns dados a nossa API:</p>
        <dl>
            <dd>Quantidade de registros a ser retornada.</dd>
            <dd>Página que desejamos.</dd>
            <dd>Ordenação.</dd>
        </dl>

   <p>No retorno, é interessante mostrar a página atual e a quantidade total de páginas totais se possível.</p>
        <dl>
            <dd>GET /clientes?page=1&pageSize=10&sort=nome</dd>
        </dl>

   <h3>1.4 — Critérios de escolha da linguagem</h3>
        <p>Ao escolher a linguagem, é interessante analisar uma série de fatores:</p>
        <dl>
            <dd>•	Documentação fornecida.</dd>
            <dd>•	Força da comunidade.</dd>
            <dd>•	Conhecimento prévio</dd>
            <dd>•	Bibliotecas e componentes fornecidos.</dd>
            <dd>•	Adoção pelo mercado.</dd>
            <dd>•	Arquitetura da linguagem (Java, JavaScript, C#, Erlang, Elixir, C++, Rust, Go, Python, PHP, Groovy, Scala, Perl, etc) e do ambiente em que ela executa.</dd>
            <dd>•	Compatibilidade entre o que a linguagem fornece e o seu sistema tenta resolver.</dd>
            <dd>•	Estabilidade da linguagem.</dd>
            <dd>•	Cultura da organização.</dd>
            <dd>•	Facilidades que cada linguagem fornece.</dd>
            <dd>•	Desempenho da linguagem.</dd>
            <dd>•	Produtividade.</dd>
            <dd>•	Bugs conhecidos na linguagem.</dd>
            <dd>•	Facilidade de desenvolvimento.</dd>
            <dd>•	Ambiente necessário para a execução da linguagem escolhida.</dd>
            <dd>•	Dentre outros critérios.</dd>
        </dl>
<h3>1.4	– Hospedagem das APIs</h3>
        <p>Conceitos importantes:</p>
        <p><b> IAAS — Infrastructure as a Service:</b> Empresa contrata uma capacidade de hardware, memória, armazenamento, processamento, etc. Te fornece um maior nível de flexibilidade e controle do gerenciamento sobre seus recursos, sendo geralmente o que os desenvolvedores mais comumente estão acostumados.</p>
        <p><b> PAAS — Platform as a service:</b> Empresa contrata um ambiente completo de desenvolvimento onde se cria, modifica e otimiza software. Modelo focado em se preocupar mais com a programação do que com o gerenciamento da infraestrutura.</p>
        <p><b> SAAS — Software as a Service:</b> É basicamente o software como um serviço, como Facebook, Twitter, Skype, etc. Nesta categoria, se oferece um produto.</p>
        
<dl>
            <dt>Alguns provedores de computação em nuvem:</dt>
            <dd>•	Amazon Web Services.</dd>
            <dd>•	Azure.</dd>
            <dd>•	Google Cloud Platform.</dd>
            <dd>•	IBM Cloud.</dd>
            <dd>•	Oracle Cloud.</dd>
            <dd>•	Alibaba Cloud.</dd>
        </dl>
        
<dl>
            <dt>Aspectos a serem considerados antes de escolher a plataforma:</dt>
            <dd>•	Recursos que cada uma das soluções oferece.</dd>
            <dd>•	Serviços que utilizaremos.</dd>
            <dd>•	Custo para a execução.</dd>
            <dd>•	Quantidade de documentação presente em cada solução.</dd>
            <dd>•	Nível de suporte e auxilio que a plataforma fornece.</dd>
            <dd>•	Quantidade de conteúdo disponível.</dd>
            <dd>•	Comunidade que utiliza a plataforma.</dd>
        </dl>
        
        
<dl>
            <dt>Feito um estudo melhor de cada solução, alguns questionamentos podem ser feitos segundo Ramon Gonçalves Gutierrez, link nas referências:</dt>
            <dd>•	Utilizarei de um SGBD relacional (MySQL, Postgree, SQL Server, etc) ou uma solução NoSQL (MongoDB, DynamoDB, etc) ?</dd>
            <dd>•	Utilizarei algum mecanismo de armazenamento em memória como o Redis ou Memcached ?</dd>
            <dd>•	Utilizarei algum produto de API Gateway fornecido pelas soluções (API Gateway AWS, API Gee da Google Cloud, etc) ?</dd>
            <dd>•	A plataforma suporta a hospedagem para a linguagem de programação e plataformas que estou utilizando ?</dd>
            <dd>•	Utilizarei uma arquitetura monolítica ou de microserviços? Devo utilizar computação serverless?</dd>
            <dd>•	Onde armazenarei meus “objetos” (documentos, arquivos, imagens, etc) ? Através da Amazon S3, Google Cloud Storage, Azure Blob ou outra solução?</dd>
            <dd>•	Qual o suporte a CDN (Content delivery Network) em cada uma das soluções? Em quais produtos está integrado ?</dd>
            <dd>•	Devo escalar verticalmente ou horizontalmente ? Qual das suas opções é mais viável para minha situação atual ?</dd>
            <dd>•	Quais os parâmetros de escalabilidade utilizarei para incrementar ou decrementar instancias ?</dd>
            <dd>•	A solução contem um mecanismo de DNS (Route 53, etc) ?</dd>
            <dd>•	Qual o custo mensal de todos os recursos que necessito ?</dd>
        </dl>
        
<h3>2 – Sobre a Segurança de APIs</h3>
        <p>Visibilidade, Controle de Acesso, Gerenciamento de tráfego, Proteção de Ameaças e a Segurança como Integridade e Confiabilidade das APIs.</p>
        <h3>2.1	– Fundamentos de Segurança</h3>
        <h3>2.1.1 - Níveis de criticidades</h3>

 <dl>
            <dt>Básico:</dt>
            <dd>•	Clients Apps – Somente Apps desenvolvidos pela própria empresa.</dd>
            <dd>•	Informações Sensíveis – Informações acessórias não relacionadas a usuários.</dd>
            <dd>•	Alteração de Dados Importantes – Somente GETs.</dd>
        </dl>

<dl>
            <dt>Intermediário:</dt>
            <dd>•	Clients Apps – Alguns Apps externos de parceiros externos bem conhecido.</dd>
            <dd>•	Informações Sensíveis – Informações sociais, Internet das Coisas.</dd>
            <dd>•	Alteração de Dados Importantes – GETs, alguns POSTs e PUTs em recursos não vitais.</dd>
        </dl>

   <dl>
            <dt>Crítico:</dt>
            <dd>•	Clients Apps – API totalmente pública, potencialmente centenas de Apps externos.</dd>
            <dd>•	Informações Sensíveis – Registros médicos, transações financeiras, dados vitais ao negócio.</dd>
            <dd>•	Alteração de Dados Importantes – Todas as operações (inclusive. DELETEs) em elementos e coleções de recursos vitais.</dd>
        </dl>

 <h3>2.1.2 – Atributos de segurança</h3>
           
   <dl>
            <dd><b>Integridade</b></dd>
            <dd><b>Disponibilidade</b></dd>
            <dd><b>Privacidade</b></dd>
            <dd><b>Auditoria</b></dd>
            <dd><b>Autenticação/Autorização</b></dd>
        </dl>

   <h3>2.1.3 – Design Patterns</h3>
        <dl>
            <dt>API FIRST</dt>
            <dd>•	Múltiplos Canais</dd>
            <dd>•	Experiências e Telas diferentes</dd>
            <dd>•	Parceiros externos e Clientes</dd>
            <dd>•	Integrações OnPremise-Cloud</dd>
        </dl>

   <dl>
            <dt>SEPARATION OF CONCERNS</dt>
            <dd>•	Agrupamento de elementos com responsabilidades semelhantes</dd>
            <dd>•	Simplificação de regras de negócio</dd>
        </dl>

<dl>
            <dt>WEB API FAÇADE</dt>
            <dd>•	O Padrão Façade nos permite desconectar a implementação do cliente de qualquer subsistema. Assim, se quiséssemos acrescentar novas funcionalidades no     subsistema seria necessário apenas alterar a Facade ao invés de alterar diversos pontos do sistema. Além disso, o padrão Facade simplifica uma interface tornando-a muito mais simples e unifica um conjunto de classes mais complexas que pertencem a um subsistema.</dd>
            <dd>•	Uma camada especifica chamada de API GATEWAY onde é possível concentrar uma série de componentes relacionados à segurança, aliviando essa preocupação de segurança das APIs. Deixam as regras de negócios independentes e simplificam as implementações das APIs.</dd>
        </dl>

<h3>2.2	– Ameaças e Vulnerabilidades</h3>
        <h3>2.2.1 - Autenticação/Autorização</h3>
        <h4>Ameaças:</h4>
        <dl>
            <dd>•	Acesso não autorizado</dd>
            <dd>•	Ataque Força Bruta</dd>
            <dd>•	Roubo de Credenciais</dd>
            <dd>•	Session hijacking</dd>
        </dl>

   <h4>Medidas:</h4>

   <dl>
            <dt>App Token:</dt>
            <dd>•	Normalmente usadas para autenticar Apps, não usuários;</dd>
            <dd>•	Tokens gerados automaticamente (mais longos e difíceis de quebrar);</dd>
            <dd>•	O Desenvolvedor da App pode regerar a chave no portal de developers;</dd>
            <dd>•	Autenticação é feita em todos os requests.</dd>
        </dl>

   <dl>
            <dt>OAuth2:</dt>
            <dd>•	Protocolo de autorização que provê acesso seguro a resources delegado pelo dono dos dados;</dd>
            <dd>•	Clients Apps se registram com Client ID/ Secret e Redirect URL;</dd>
            <dd>•	São 4 tipos de “Authorization Grants” para acesso às APIs com fluxos diferentes.</dd>
        </dl>

<dl>
            <dt>OpenID Connect:</dt>
            <dd>•	Protocolo de Single Sign-On(SSO) para a internet;</dd>
            <dd>•	Complementar ao OAuth2;</dd>
            <dd>•	ID Token é usado como documento de identificação;</dd>
            <dd>•	Enconded como JWT (JSON Web Token).</dd>
        </dl>

   <dl>
            <dt>Outras recomendações:</dt>
            <dd>•	Autenticação Multi-Fatores;</dd>
            <dd>•	Evitar o uso de Sessão. Lembre-se que RESTful é Stateless;</dd>
            <dd>•	Usar os padrões a não ser que você saiba exatamente o que está fazendo;</dd>
            <dd>•	Cuidados especiais na manipulação dos tokens(Não envie por email, disponibilize em seu site de developers(usando HTTPS), não armazene em plain-text e nem logs, cuidado com Forwards/Redirects).</dd>
        </dl>

<h3>2.2.2 – Disponibilidades</h3>
        <h4>Ameaças:</h4>
        <dl>
            <dd>•	DDoS (Distributed Denial of Service)</dd>
            <dd>•	Buffer Overflow</dd>
            <dd>•	Injection (SQL, XML, JSON)</dd>
        </dl>

 <h4>Medidas:</h4>
        <dl>
            <dd>•	Identificar comportamento malicioso;</dd>
            <dd>•	Monitorar o tráfego nas APIs (preferencialmente com alertas);</dd>
            <dd>•	Limitar o uso dos Apps;</dd>
            <dd>•	Plugar detecção de Fraude de negócio.</dd>
        </dl>

 <h3>2.2.3 – Privacidade</h3>
        <h4>Ameaças:</h4>
        <dl>
            <dd>•	Information Disclosure(Revelação de dados privados)</dd>
            <dd>•	Man-in-the-middle e Network Eavesdropping (Espionagem)</dd>
            <dd>•	Data Scraping</dd>
        </dl>
        <h4>Medidas:</h4>
        <dl>
            <dd>•	Use sempre SSL/TLS;</dd>
            <dd>•	Algumas situações podem requerer criptografia adicional(usar algoritmos já comprovados);</dd>
            <dd>•	Informações sensíveis devem ser mascaradas (número de cartão de crédito, tokens, etc);</dd>
            <dd>•	Error Handling (não expor detalhes do backend, sem stacktrace).</dd>
        </dl>

  <h3>2.2.4 - Auditoria</h3>
        <h4>Ameaças</h4>
        <dl>
            <dd>•	Repudiação</dd>
            <dd>•	Compliance(PCI-DSS, HIPAA)</dd>
        </dl>

<h4>Medidas:</h4>
        <dl>
            <dd>•	Armazenar os logs com as chamadas realizadas (especialmente as críticas);</dd>
            <dd>•	Cuidados especiais (Os logs podem crescer, logs em arquivo nem sempre são fáceis de inspecionar / buscar, dados sensíveis devem ser obfuscados).</dd>
        </dl>

  <h3>2.2.5 - Integridade</h3>
        <h4>Ameaças:</h4>
        <dl>
            <dd>•	Injection (SQL, XML, JSON)</dd>
            <dd>•	Cross-site Scripting (XSS)</dd>
            <dd>•	Cross-site Request Forgery (XSRF)</dd>
        </dl>

   <h4>Medidas:</h4>
        <dl>
            <dd>•	Reduza a superfície de Ataque (o que não pode ser acessado e nem deve ser mostrado);</dd>
            <dd>•	Prevenção de XML, JSON e SQL Injection (Filter Input, Escape Output);</dd>
            <dd>•	Unique Transaction ID para evitar “Replay Requests”;</dd>
            <dd>•	Utilizar chaves opacas.</dd>
        </dl>

<h2 align="center">Referências</h2>

   <p>Entendendo a Importância da Modelagem e Segurança na Construção de APIs. Disponível em: <br> 
            https://web.digitalinnovation.one/lab/entendendo-a-importancia-da-modelagem-e-seguranca-na-construcao-de-apis/learning/
        </p>

  <p>
            Artigo de RAMON LACAVA GUTIERREZ. Disponível em: <br>
            https://medium.com/@ramonrune/arquitetando-uma-api-restful-8ffcf892586a
        </p>

 <p>
            Artigo de Ed Price – MSFT. Disponível em: <br>
            https://docs.microsoft.com/pt-br/azure/architecture/best-practices/api-design
        </p>

  <p>
            Conceito FUNDAMENTAL para Desenvolvimento de APIs. Vídeo disponível em: <br>
            https://www.youtube.com/watch?v=HTkAO4wx2uw
        </p>

 <p>
            Boas práticas para uma API RESTful. Vídeo disponível em: <br>
            https://www.youtube.com/watch?v=P-juXKmJy_g
        </p>

 <p>
            Esse é o meu segredo para modelar bem REST APIs. Vídeo disponível em: <br>
            https://www.youtube.com/watch?v=FVuhfwvuj3Y
        </p>

  <p>
            Os Fundamentos da Segurança de APIs. Vídeo disponível em: <br>
            https://www.youtube.com/watch?v=h4A8HytL5ts
        </p>

  <p>
            Padrão de Projeto Facade em Java. Disponível em: <br>
            https://www.devmedia.com.br/padrao-de-projeto-facade-em-java/26476
        </p>

<h2 align="center">Links uteis:</h2>

   OWASP: https://owasp.org; <br>
   OWASP Project API Secutory: https://owasp.org/www-project-api-security; <br>
   API Academy Certification: https://apiacademy.co/api-certification; <br>
   API Security Articles: https://apisecurity.io; <br>
   OpenAPI Initiative: https://www.openapis.org; <br>
   Swagger: https://swagger.io; <br>
   Swagger OpenAPI Specification: https://swagger.io/specification; <br>
   Postman: https://www.postman.com/postman/workspace/postman-team-collections/overview; <br>
   Java + Spring: https://www.java.com/pt-BR/download/help/develop.html e https://spring.io/projects/spring-boot; <br>
   Apigee: https://cloud.google.com/training/apigee/?hl=pt. <br>











