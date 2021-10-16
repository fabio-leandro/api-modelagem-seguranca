# api-modelagem-seguranca
Repositório para armazenar informações sobre modelagem e segurança de API's

Notas sobre Modelagem e Segurança na Construção de APIs

O que é API?
APIs são Interfaces que permite a comunicação entre aplicações sem que precise saber os detalhes por trás do desenvolvimento de determinada API.
Uma API funcionando com um cliente fazendo uma requisição a essa API. Então, ela faz a busca no servidor e retorna uma resposta.
Um exemplo de API é o GOOGLE MAPS.
Uma API facilita a comunicação entre aplicações porque há ganho de agilidade e compatibilidade.
As APIs pode ser do tipo pública ou privada.
1 - Sobre Modelagem de APIS
O mercado utiliza dominantemente APIs com o conceito REST e a comunicação via protocolo HTTP. 
REST (Representational State Transfer) define princípios arquiteturais para a comunicação entre cliente e servidor.
O HTTP (HyperText Markup Language) funciona como um protocolo de requisição-resposta no modelo computacional cliente-servidor.
Uma API/RESTFUL é aquela que foi implementada seguindo todas as boas práticas do protocolo REST.
1.1	– Métodos Seguros e Métodos Idempotentes
Um método é seguro se ele for utilizado apenas para operações de leitura, tais como o GET, HEAD e OPTIONS. Não se espera que seja feito qualquer tipo de alteração no estado do servidor ao realizar uma requisição a estes métodos.
Um método é considerado idempotente se os efeitos colaterais de uma ou mais requisições idênticas forem iguais a uma única requisição.

 
Fonte: https://medium.com/@ramonrune/arquitetando-uma-api-restful-8ffcf892586a

1.2	- Modelo de Maturidade de Richardson
Leonard Richardson fez uma análise em centenas de API's diferentes. E dividiu em quatro categorias para identificar o nível de maturidade da API com base no quanto eles são compatíveis com REST. 
Ele utilizou três fatores. URI, HTTP, HATEOAS (Hypermedia). 
 

1.2.1	- Nível 0

Nesse nível pode se dizer que são utilizados os verbos HTTP, mas sem respeitar as regras do padrão REST. Como no quadro abaixo os verbos HTTP não correspondem com a URI.

 
FONTE: https://rivaildojunior.medium.com/modelo-de-maturidade-de-richardson-para-apis-rest-8845f93b288


1.2.2	– Nível 1

Nesse nível os recursos já correspondem com os verbos. Os recursos são representados por substantivos no plural.

 


1.2.3	– Nível 2

No nível 2 os verbos HTTP são usados de forma correta. Os verbos mais utilizados são GET, POST, PUT e DELETE.

 

1.2.4	– Nível 3

Para o HATEOAS, uma API que implementa esse nível fornece aos seus clientes links que indicarão como poderá ser feita a navegação entre seus recursos.

 
Fonte: https://rivaildojunior.medium.com/modelo-de-maturidade-de-richardson-para-apis-rest-8845f93b288


1.3	– Dicas para melhores práticas para o desenvolvimento de uma API RESTFUL

O Recurso deve ser escrito no substantivo;
Referente a plural e singular, deve seguir o padrão em todo o projeto. Se usar no singular, que seja feito em todo o projeto.
Os recursos devem ser descritivos e fáceis de entender.

GET /clientes — Lista os clientes.
GET /clientes/1 — Obtém os dados do cliente 1.
POST /clientes — Cria um novo cliente.
PUT /clientes/1 — Altera o cliente 1.
DELETE /clientes/1 — Remove o cliente 1.
PATCH /clientes/1 — Atualiza parcialmente o cliente 1.

Utilize no máximo um encadeamento de 3–4 recursos no máximo. Isso para facilitar a compreensão.

GET /clientes/1/parceiros — Lista os parceiros do cliente 1.
GET /clientes/1/parceiros/1 — Lista o parceiro 1 do cliente 1.

A documentação precisa ser fácil de encontrar, compreensível ao desenvolvedor, fácil de testar e informar o seu propósito específico.

É uma boa prática sempre versionar. Pode se utilizar o versionamento na URI do recurso:

GET /v1/clientes
POST /v1/clientes
GET /v1/public/characters
GET/v1/public/characters/1

Onde for permitido, é recomendado utilizar JSON para as respostas.
JSON é um formato amplamente utilizado na Web, os arquivos JSON usam 30% menos banda do que arquivos XML.

As pessoas acessam APIs de diversos locais (shoppings, em casa, aeroportos, bancos, restaurantes, etc). Devemos tomar cuidado, pois nunca se sabe se não há ninguém interceptando as mensagens. Não deixe as pessoas acessaram sua API sem o uso de HTTPS.

Em situações de busca, filtro, ordenação, status, paginação é interessante usar QUERY PARAMS.

GET /clientes?ativo=true

Logs auxiliam no processo de debug da API.

As métricas que são geradas pela API também são importantes para analisar se essa API está sendo usada corretamente ou identificar possíveis melhorias.

Mensagens de retorno descritivas podem auxiliar o cliente no consumo da API.

Ao estruturar uma API, é interessante dividi-la em camadas. Cada camada terá sua responsabilidade específica. Um modelo a ser seguido pode ser:

Camada de persistência de dados: Controla banco de dados.
Camada de serviço/negócios: Contém as lógicas de negócio.
Camada de recurso: Realiza a exposição dos recursos.

Para dados que não mudam frequentemente e não são sensíveis a erro, é interessante a utilização de caches para otimizar a performance de sua API.

Formas de realizar autenticação, como por exemplo:

Sem autorização.
Bearer Token.
Basic Auth.
Digest Auth.
OAuth 1.0.
OAuth 2.0
Hawk Authentication.
AWS Signature.
Dentre outros mecanismos.

No caso de retornar uma grande quantidade de dados, uma boa prática é a realização de paginação. 

Na paginação, podemos passar alguns dados a nossa API:

Quantidade de registros a ser retornada.
Página que desejamos.
Ordenação.

No retorno, é interessante mostrar a página atual e a quantidade total de páginas totais se possível.

GET /clientes?page=1&pageSize=10&sort=nome

1.4 — Critérios de escolha da linguagem

Ao escolher a linguagem, é interessante analisar uma série de fatores:

•	Documentação fornecida.
•	Força da comunidade.
•	Conhecimento prévio.
•	Bibliotecas e componentes fornecidos.
•	Adoção pelo mercado.
•	Arquitetura da linguagem (Java, JavaScript, C#, Erlang, Elixir, C++, Rust, Go, Python, PHP, Groovy, Scala, Perl, etc) e do ambiente em que ela executa.
•	Compatibilidade entre o que a linguagem fornece e o seu sistema tenta resolver.
•	Estabilidade da linguagem.
•	Cultura da organização.
•	Facilidades que cada linguagem fornece.
•	Desempenho da linguagem.
•	Produtividade.
•	Bugs conhecidos na linguagem.
•	Facilidade de desenvolvimento.
•	Ambiente necessário para a execução da linguagem escolhida.
•	Dentre outros critérios.
1.4	– Hospedagem das APIs

Conceitos importantes:

IAAS — Infrastructure as a Service: Empresa contrata uma capacidade de hardware, memória, armazenamento, processamento, etc. Te fornece um maior nível de flexibilidade e controle do gerenciamento sobre seus recursos, sendo geralmente o que os desenvolvedores mais comumente estão acostumados.

PAAS — Platform as a service: Empresa contrata um ambiente completo de desenvolvimento onde se cria, modifica e otimiza software. Modelo focado em se preocupar mais com a programação do que com o gerenciamento da infraestrutura.

SAAS — Software as a Service: É basicamente o software como um serviço, como Facebook, Twitter, Skype, etc. Nesta categoria, se oferece um produto.

Alguns provedores de computação em nuvem:

•	Amazon Web Services.
•	Azure.
•	Google Cloud Platform.
•	IBM Cloud.
•	Oracle Cloud.
•	Alibaba Cloud.

Aspectos a serem considerados antes de escolher a plataforma:

•	Recursos que cada uma das soluções oferece.
•	Serviços que utilizaremos.
•	Custo para a execução.
•	Quantidade de documentação presente em cada solução.
•	Nível de suporte e auxilio que a plataforma fornece.
•	Quantidade de conteúdo disponível.
•	Comunidade que utiliza a plataforma.

Feito um estudo melhor de cada solução, alguns questionamentos podem ser feitos segundo Ramon Gonçalves Gutierrez, link nas referências:

•	Utilizarei de um SGBD relacional (MySQL, Postgree, SQL Server, etc) ou uma solução NoSQL (MongoDB, DynamoDB, etc) ?
•	Utilizarei algum mecanismo de armazenamento em memória como o Redis ou Memcached ?
•	Utilizarei algum produto de API Gateway fornecido pelas soluções (API Gateway AWS, API Gee da Google Cloud, etc) ?
•	A plataforma suporta a hospedagem para a linguagem de programação e plataformas que estou utilizando ?
•	Utilizarei uma arquitetura monolítica ou de microserviços? Devo utilizar computação serverless?
•	Onde armazenarei meus “objetos” (documentos, arquivos, imagens, etc) ? Através da Amazon S3, Google Cloud Storage, Azure Blob ou outra solução?
•	Qual o suporte a CDN (Content delivery Network) em cada uma das soluções? Em quais produtos está integrado ?
•	Devo escalar verticalmente ou horizontalmente ? Qual das suas opções é mais viável para minha situação atual ?
•	Quais os parâmetros de escalabilidade utilizarei para incrementar ou decrementar instancias ?
•	A solução contem um mecanismo de DNS (Route 53, etc) ?
•	Qual o custo mensal de todos os recursos que necessito ?


2	– Sobre a Segurança de APIs

Visibilidade, Controle de Acesso, Gerenciamento de tráfego, Proteção de Ameaças e a Segurança como Integridade e Confiabilidade das APIs.

2.1	– Fundamentos de Segurança

2.1.1 - Níveis de criticidades

Básico:
•	Clients Apps – Somente Apps desenvolvidos pela própria empresa.

•	Informações Sensíveis – Informações acessórias não relacionadas a usuários.

•	Alteração de Dados Importantes – Somente GETs.

Intermediário:
•	Clients Apps – Alguns Apps externos de parceiros externos bem conhecido.

•	Informações Sensíveis – Informações sociais, Internet das Coisas.

•	Alteração de Dados Importantes – GETs, alguns POSTs e PUTs em recursos não vitais.

Crítico:
•	Clients Apps – API totalmente pública, potencialmente centenas de Apps externos.

•	Informações Sensíveis – Registros médicos, transações financeiras, dados vitais ao negócio.

•	Alteração de Dados Importantes – Todas as operações (inclusive. DELETEs) em elementos e coleções de recursos vitais.

2.1.2 – Atributos de segurança

•	Autenticação/Autorização
•	Integridade
•	Disponibilidade
•	Privacidade
•	Auditoria

2.1.3 – Design Patterns

API FIRST
•	Múltiplos Canais
•	Experiências e Telas diferentes
•	Parceiros externos e Clientes
•	Integrações OnPremise-Cloud

SEPARATION OF CONCERNS
•	Agrupamento de elementos com responsabilidades semelhantes
•	Simplificação de regras de negócio
WEB API FAÇADE
•	O Padrão Façade nos permite desconectar a implementação do cliente de qualquer subsistema. Assim, se quiséssemos acrescentar novas funcionalidades no subsistema seria necessário apenas alterar a Facade ao invés de alterar diversos pontos do sistema. Além disso, o padrão Facade simplifica uma interface tornando-a muito mais simples e unifica um conjunto de classes mais complexas que pertencem a um subsistema.
•	Uma camada especifica chamada de API GATEWAY onde é possível concentrar uma série de componentes relacionados à segurança, aliviando essa preocupação de segurança das APIs. Deixam as regras de negócios independentes e simplificam as implementações das APIs.


2.2	– Ameaças e Vulnerabilidades

2.2.1	- Autenticação/Autorização
Ameaças:
•	Acesso não autorizado
•	Ataque Força Bruta
•	Roubo de Credenciais
•	Session hijacking
Medidas:
App Token:
•	Normalmente usadas para autenticar Apps, não usuários;
•	Tokens gerados automaticamente (mais longos e difíceis de quebrar)
•	O Desenvolvedor da App pode regerar a chave no portal de developers
•	Autenticação é feita em todos os requests.
OAuth2:
•	Protocolo de autorização que provê acesso seguro a resources delegado pelo dono dos dados;
•	Clients Apps se registram com Client ID/ Secret e Redirect URL;
•	São 4 tipos de “Authorization Grants” para acesso às APIs com fluxos diferentes.
OpenID Connect:
•	Protocolo de Single Sign-On(SSO) para a internet;
•	Complementar ao OAuth2;
•	ID Token é usado como documento de identificação;
•	Enconded como JWT (JSON Web Token).

Outras recomendações:
•	Autenticação Multi-Fatores;
•	Evitar o uso de Sessão. Lembre-se que RESTful é Stateless;
•	Usar os padrões a não ser que você saiba exatamente o que está fazendo;
•	Cuidados especiais na manipulação dos tokens(Não envie por email, disponibilize em seu site de developers(usando HTTPS), não armazene em plain-text e nem logs, cuidado com Forwards/Redirects).
2.2.2	– Disponibilidades

Ameaças:
•	DDoS (Distributed Denial of Service)
•	Buffer Overflow
•	Injection (SQL, XML, JSON)


Medidas:

•	Identificar comportamento malicioso;
•	Monitorar o tráfego nas APIs (preferencialmente com alertas);
•	Limitar o uso dos Apps;
•	Plugar detecção de Fraude de negócio.

2.2.3	– Privacidade

Ameaças:
•	Information Disclosure(Revelação de dados privados)
•	Man-in-the-middle e Network Eavesdropping (Espionagem)
•	Data Scraping

Medidas:
•	Use sempre SSL/TLS;
•	Algumas situações podem requerer criptografia adicional(usar algoritmos já comprovados);
•	Informações sensíveis devem ser mascaradas (número de cartão de crédito, tokens, etc);
•	Error Handling (não expor detalhes do backend, sem stacktrace).

2.2.4 - Auditoria

Ameaças:
•	Repudiação
•	Compliance(PCI-DSS, HIPAA)

Medidas:

•	Armazenar os logs com as chamadas realizadas (especialmente as críticas);
•	Cuidados especiais (Os logs podem crescer, logs em arquivo nem sempre são fáceis de inspecionar / buscar, dados sensíveis devem ser obfuscados).

2.2.5 - Integridade

Ameaças:
•	Injection (SQL, XML, JSON)
•	Cross-site Scripting (XSS)
•	Cross-site Request Forgery (XSRF)

Medidas:

•	Reduza a superfície de Ataque (o que não pode ser acessado e nem deve ser mostrado);
•	Prevenção de XML, JSON e SQL Injection (Filter Input, Escape Output);
•	Unique Transaction ID para evitar “Replay Requests”;
•	Utilizar chaves opacas.





Referências:

Entendendo a Importância da Modelagem e Segurança na Construção de APIs. Disponível em: 
https://web.digitalinnovation.one/lab/entendendo-a-importancia-da-modelagem-e-seguranca-na-construcao-de-apis/learning/

Artigo de RAMON LACAVA GUTIERREZ. Disponível em:
https://medium.com/@ramonrune/arquitetando-uma-api-restful-8ffcf892586a

Artigo de Ed Price – MSFT. Disponível em:
https://docs.microsoft.com/pt-br/azure/architecture/best-practices/api-design

Conceito FUNDAMENTAL para Desenvolvimento de APIs. Vídeo disponível em:
https://www.youtube.com/watch?v=HTkAO4wx2uw

Boas práticas para uma API RESTful. Vídeo disponível em:
https://www.youtube.com/watch?v=P-juXKmJy_g

Esse é o meu segredo para modelar bem REST APIs. Vídeo disponível em:
https://www.youtube.com/watch?v=FVuhfwvuj3Y

Os Fundamentos da Segurança de APIs. Vídeo disponível em:
https://www.youtube.com/watch?v=h4A8HytL5ts


Padrão de Projeto Facade em Java. Disponível em:
https://www.devmedia.com.br/padrao-de-projeto-facade-em-java/26476




Links uteis:

OWASP: https://owasp.org;
OWASP Project API Secutory: https://owasp.org/www-project-api-security;
API Academy Certification: https://apiacademy.co/api-certification;
API Security Articles: https://apisecurity.io;
OpenAPI Initiative: https://www.openapis.org;
Swagger: https://swagger.io;
Swagger OpenAPI Specification: https://swagger.io/specification;
Postman: https://www.postman.com/postman/workspace/postman-team-collections/overview;
Java + Spring: https://www.java.com/pt-BR/download/help/develop.html e https://spring.io/projects/spring-boot;
Apigee: https://cloud.google.com/training/apigee/?hl=pt.

















