# Prospectar Leads — Social Media

Projeto de prospecção de empresas locais para serviços de social media, utilizando Google Places API (New), pesquisa no Instagram e organização dos resultados em Google Sheets e Excel.

## Objetivo

Identificar e avaliar oportunidades comerciais em Santos-SP e São Vicente-SP, mantendo um histórico de empresas pesquisadas e abordadas para evitar duplicidades.

O fluxo também permite revisar leads existentes e pesquisar outras cidades.

## Funcionalidades

- Pesquisa de estabelecimentos com Google Places API.
- Identificação e verificação do Instagram oficial.
- Registro de seguidores, posts e Reels dos últimos 30 dias.
- Avaliação da presença digital e dos canais de contato.
- Priorização de leads pela pontuação Acquisition.
- Histórico de pesquisa e abordagem comercial.
- Exportação dos resultados em Excel.
- Sincronização com a planilha Google Sheets existente.

## Tecnologias

- Python
- Google Places API (New)
- Google Sheets
- OpenPyXL
- ChatGPT/Codex com a skill de prospecção

## Configuração

Instale as dependências:

```bash
python -m pip install openpyxl tzdata
```

Configure a chave do Google Maps na variável de ambiente:

```text
GOOGLE_MAPS_API_KEY
```

O projeto Google Cloud precisa ter a Places API (New) e o faturamento habilitados.

**Não inclua a chave de API no código, no README ou nos commits.**

## Execução

Execute os comandos na pasta da skill que contém o diretório `scripts`.

### Coletar candidatos

```bash
python scripts/google_places.py --limit 100 --max-requests 30 --output candidatos-places.json
```

### Calcular pontuações e gerar o Excel

Após verificar os dados e preparar `leads-entrada.json`:

```bash
python scripts/acquisition.py --input leads-entrada.json --output prospectar-leads.xlsx
```

A verificação do Instagram e a atualização do Google Sheets são etapas complementares. Não são realizadas automaticamente pelo script de pontuação.

## Pontuação Acquisition

A pontuação varia de **0,00 a 1,00**, conforme os seguintes pesos:

| Critério | Peso |
| --- | --- |
| Frequência de publicações | 30% |
| Uso de Reels | 25% |
| Apresentação do perfil | 20% |
| Oportunidade comercial | 20% |
| Facilidade de contato | 5% |

A nota é uma heurística de priorização, não uma previsão de contratação.

Quando faltarem informações, o resultado apresenta um intervalo mínimo–máximo e sinaliza a avaliação como incompleta.

## Histórico

O status da pesquisa é separado do status da abordagem comercial.

Estados de pesquisa:

- Identificado
- Verificação pendente
- Pesquisa concluída
- Revisado

Uma empresa pesquisada não deve ser marcada como abordada sem confirmação de contato.

Nas revisões, os registros existentes são atualizados preservando o histórico comercial.

## Qualidade dos dados

- Registrar fontes e datas de verificação.
- Não inventar seguidores, publicações ou contatos.
- Não tratar dados desconhecidos como zero.
- Confirmar o vínculo entre a empresa e o Instagram.
- Preservar a identificação de filiais.
- Respeitar bloqueios e limitações das fontes.
- Não enviar mensagens comerciais automaticamente.

## Entregáveis

- Arquivo Excel com abas **Leads** e **Resumo**.
- Atualização da planilha Google Sheets, quando a integração estiver disponível.
- Registro das verificações concluídas e das pendências.

## Limitações

O acesso à API do Google Maps não fornece métricas do Instagram. A conclusão da pesquisa depende da disponibilidade das fontes e das integrações autorizadas.

O fluxo é executado sob demanda. Pesquisas recorrentes exigem uma automação configurada separadamente.
