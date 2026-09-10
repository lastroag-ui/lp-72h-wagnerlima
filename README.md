# LP de 72h — Wagner Lima

Site de uma pagina, HTML estatico. Sem build, sem node, sem banco.
O que esta na branch `main` e exatamente o que esta no ar hoje em
https://site.seugestordemarketing.com.br/

## Subir na hospedagem

Jogue o conteudo da raiz do repositorio na raiz do subdominio (o
`public_html` do subdominio, ou a pasta que o painel apontar). O
`index.html` fica na raiz, sem subpasta.

### Automatizar na Hostinger (deploy a cada push)

No hPanel: **Avancado > Git**.

1. Repositorio: a URL SSH deste repo
2. Branch: `main`
3. Diretorio: a pasta do subdominio
4. O painel gera uma **chave SSH**. Copie ela e mande pra gente, que
   cadastramos aqui como *deploy key* (o repo e privado, sem a chave o
   painel nao consegue clonar).
5. Depois de criado, o painel mostra um **webhook**. Manda ele pra
   gente tambem, que a gente pluga aqui no GitHub. A partir disso todo
   push na `main` publica sozinho.

Sem o passo 5 ainda funciona, so nao e automatico: e clicar em
**Deploy** no painel quando quiser atualizar.

## Atencao, o ponto que mais quebra

O endereco `site.seugestordemarketing.com.br` esta escrito dentro dos
arquivos, nas tags que o Google e as redes sociais leem (canonical,
og:image, dados estruturados, sitemap, robots).

- Se o subdominio novo for o **mesmo** `site.seugestordemarketing.com.br`,
  nao precisa mexer em nada.
- Se for **outro** subdominio, troque `site.seugestordemarketing.com.br`
  pelo novo endereco nestes arquivos:

  | arquivo | ocorrencias |
  |---|---|
  | `index.html` | 24 |
  | `robots.txt` | 2 |
  | `sitemap.xml` | 2 |
  | `llms.txt` | 1 |

  Se nao trocar, a pagina abre normal, mas o Google le que a versao
  oficial dela e a antiga, e o preview do WhatsApp e do Instagram vai
  buscar a imagem no endereco antigo.

## O que tem aqui

| arquivo | o que e |
|---|---|
| `index.html` | a pagina |
| `404.html` | pagina de erro |
| `assets/img/` | imagens: logo, prints dos sites, imagem de preview |
| `favicon.ico`, `wl-simbolo-3.png`, `wl-simbolo-3.ico`, `apple-touch-icon.png` | icones |
| `robots.txt` | libera os buscadores, inclusive os de IA |
| `sitemap.xml` | mapa do site |
| `llms.txt` | resumo da pagina para buscador com IA |
| `.htaccess` e `assets/.htaccess` | cache e compressao (Apache e LiteSpeed) |
| `_headers` | a mesma coisa, no formato da Cloudflare. Fora da Cloudflare nao faz nada, pode ignorar |

## Tag do Google

A pagina tem o Google Tag Manager instalado, container **GTM-NJDBRFZC**,
no `<head>` e logo depois do `<body>`. Os disparos de clique no WhatsApp
estao configurados dentro desse container, entao avise antes de trocar
ou remover.

## O que nao mudar sem combinar

- o numero do WhatsApp: **55 11 94170 8181**
- o container do GTM
- o texto da pagina

## Nota

A versao na Cloudflare continua no ar durante a migracao. Ela sai do ar
so depois que o subdominio novo estiver respondendo.
