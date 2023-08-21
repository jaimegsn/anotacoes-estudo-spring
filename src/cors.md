# CORS e Same-Origin

CORS é um acrônimo para **Cross-Origin Resource Sharing** (Compartilhamento de Recursos entre Origens Cruzadas). Trata-se de um mecanismo de segurança implementado nos navegadores web para proteger as aplicações web contra acessos não autorizados a recursos por parte de origens (domínios, protocolos ou portas) externas.

Mas os navegadores por padrão já possuem uma política para resolver esse problema chamada **same-origin**, então porque eu deveria me preocupar em implementar o CORS ? Essa preocupação se deve ao fato de que o **same-origin** é muito restritivo para cenários legítimos de integração entre sistemas.

### Como funciona Same-Origin:

Os navegadores por padrão utilizam uma política de segurança chamada **same-origin (mesma origem),** onde só é permitido a troca de informações se os envolvidos tiverem a mesma origem.

E uma origem é composta por: **protocolo**, **domínio** e **porta**. Por exemplo:

- **`http://exemplo.com:80`**
  - Procolos: **`http`**
  - domínio: **`exemplo.com`**
  - porta (geralmente oculta): **`80`**

Caso algum desses 3 seja diferente a origem já muda.

Então segundo essa política **same-origin** para conseguimos realizar uma requisição de um Servidor A para um Servidor B solicitando algum recurso, é necessário que os dois estejam na mesma origem.

### Como funciona o CORS:

A política de CORS permite que um servidor configure explicitamente quais origens externas têm permissão para acessar seus recursos por meio de solicitações HTTP. Isso possibilita uma integração controlada e segura entre sistemas que operam em domínios diferentes.

Ou seja basicamente ele funciona como um segurança que verifica se a origem de uma determinada requisição têm permissão para acessar determinado recurso ou não, se não tiver permissão é bloqueado.
