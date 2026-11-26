# Coleta de editais com ferramentas gratuitas

| Fonte | Ferramenta | Quando usar |
| --- | --- | --- |
| API ou RSS oficial | Python padrão (`urllib.request`, `json`, `xml.etree.ElementTree`) | Primeira escolha. Use a paginação e os filtros documentados. |
| Portal com HTML estático | [Scrapy](https://docs.scrapy.org/en/latest/intro/install.html) | Para vários portais ou páginas, com limite de requisições por domínio e exportação estruturada. |
| Listagem pública que depende de JavaScript | [scrapy-playwright](https://pypi.org/project/scrapy-playwright/) | Renderize apenas as páginas em que o HTML original não contém a listagem e a fonte não fornece API ou feed adequado. |
| PDF com texto | [pypdf](https://pypdf.readthedocs.io/en/stable/) | Extraia o texto por página. Em PDF escaneado, use [Tesseract](https://tesseract-ocr.github.io/) para OCR e revise os campos decisivos no original. |
| Histórico de um piloto | [SQLite](https://docs.python.org/3/library/sqlite3.html) | Guarde fontes, chamadas, versões e histórico de avisos em um arquivo local. |

## Instalação

Baixe [Python](https://www.python.org/downloads/) e use Python 3.11 ou superior. No terminal, crie o ambiente e instale os pacotes nele.

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install scrapy pypdf
```

No Linux ou macOS, use `.venv/bin/python` no lugar de `.\.venv\Scripts\python.exe`. Se uma fonte realmente precisar de navegador, instale a integração e o Chromium conforme as instruções do pacote.

```powershell
.\.venv\Scripts\python.exe -m pip install scrapy-playwright
.\.venv\Scripts\python.exe -m playwright install chromium
```

## Como manter a coleta leve e confiável

1. Cadastre duas ou três fontes oficiais por perfil. Pesquise na própria instituição pelo nome do programa, número do edital e termos como “retificação” e “prorrogação”. Use a busca geral para encontrar fontes novas e confirme o resultado na página oficial.
2. Consulte só URLs públicas permitidas. Respeite `robots.txt`, os limites do portal e `Retry-After`. Em Scrapy, habilite `ROBOTSTXT_OBEY` e [AutoThrottle](https://docs.scrapy.org/en/latest/topics/autothrottle.html). Pause o conector se a fonte devolver bloqueio persistente.
3. Use `ETag` e `Last-Modified` quando a fonte oferecer esses cabeçalhos. Baixe o PDF quando for novo ou houver sinal de alteração. Registre a última execução bem-sucedida por fonte.
4. Normalize primeiro órgão, número, ano e URL. Extraia prazo, proponente e benefício com item ou página de evidência. Use IA na classificação e na leitura dos documentos novos ou alterados. Se faltar evidência, mande para revisão.
5. Valide a cobertura com uma amostra manual do próprio portal. Registre volume encontrado, URLs abertas, registros sem prazo, duplicatas e falhas de coleta. Uma rodada vazia e uma fonte indisponível devem aparecer como estados diferentes.
