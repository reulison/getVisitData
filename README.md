# getVisitData
Obtém os dados de origem, mídia, campanha, conteúdo e termo, assim como o Google Analytics. E salva nos seguintes cookies: getVisitSource, getVisitMedium, getVisitCampaing.

# Contato
Se tiver qualquer duvida basta enviar um e-mail para eu@reulison.com.br

# Formatos suportados
- CommonJS: https://cdn.jsdelivr.net/npm/getvisitdata/dist/getvisitdata.cjs.js
- UMD: https://cdn.jsdelivr.net/npm/getvisitdata/dist/getvisitdata.umd.js
- ESM: https://cdn.jsdelivr.net/npm/getvisitdata/dist/getvisitdata.esm.js

Instalar com npm
```shell
npm i getvisitdata
```

# Construir a partir do código fonte
clonar este repositório e:
```shell
npm install
npm run build
```

# Modo usar
```html
<script src="https://cdn.jsdelivr.net/npm/getvisitdata/dist/getvisitdata.umd.js"></script>
<script>console.log(visitData.get());</script>

<!-- ou, e você pode copiar isso para um console javascript sem a tag <script> também para teste -->

<script>
  await import('https://cdn.jsdelivr.net/npm/getvisitdata/dist/getvisitdata.umd.js')
  console.log(visitData.get())
</script>
```
## visitData.get() retornará um objeto como
```json
{
  "source": "google",
  "medium": "organic"
}
```
Você também pode executar `visitData.rawData()` que retornará muito mais informações

Os resultados são armazenados em cache com `sessionStorage`, então visualizações de página subsequentes na mesma sessão retornarão o resultado original.

## Opções
| Opção  |  Função | Valor  |
| ------------ | ------------ | ------------ |
| **cache**  | desabilitar cache  |  `true` or `false`|
| **url_parameters**  | parâmetros de URL personalizados  |  ex. `{campaign: ['campaign', 'utm_campaign'], urlparam_custom: ['custom']}` |

### cache
A primeira vez que visitdata `get()` ou `rawData()` for chamado, a biblioteca armazenará os resultados em `sessionStorage`, para que as visualizações de página subsequentes na mesma sessão retornem os resultados originais do cache.

Durante o teste, ou por algum outro motivo, você pode querer desabilitar o cache. Você pode fazer isso chamando:

```javascript
visitData.setOption('cache', false)
```
### url_parameters

Por padrão, o `visitData` assume que sua URL pode ter parâmetros UTM padrão, como `utm_source`, `utm_medium`, `utm_campaign`, `utm_content` e `utm_term`. No entanto, você pode querer escolher parâmetros personalizados adicionalmente.

Por exemplo, digamos que você realmente queira rastrear um `campaign_id` em vez de `utm_campaign` e, às vezes, seu `medium` pode estar em um parâmetro chamado `custom_medium`. Você pode fazer algo assim:

```javascript
visitData.setOption('url_parameters', {
    'medium': ['utm_medium', 'custom_medium'],
    'source': ['utm_source'],
    'campaign': ['utm_campaign'],
    'campaign_id': ['campaign_id']
})
```
Note que o valor de cada chave precisa ser uma lista.

Agora, chamar `visitData.get()` retornará um objeto como:

```json
  'medium': 'cpc',
  'source: 'google',
  'campaign: 'My campaign',
  'campaign_id': '1241234'
```
