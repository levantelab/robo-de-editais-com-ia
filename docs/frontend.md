# Proposta de frontend do Robô de Editais

Para um piloto local, use [Streamlit](https://docs.streamlit.io/get-started/installation) com SQLite. Para uma equipe que precise de perfis e revisão compartilhada, evolua para [Next.js](https://nextjs.org/docs/app/getting-started/installation) com API de leitura e banco compartilhado. O coletor roda em processo agendado separado da interface.

| Tela | Conteúdo e ação principal |
| --- | --- |
| Radar | Resultados com filtros por tema, fonte, prazo e triagem. Comece pelos editais que vencem antes. |
| Detalhes | Prazo, quem pode propor, justificativa, trechos da fonte e histórico de retificações. Botão para abrir o documento oficial. |
| Meu perfil | Regiões, temas, vínculo, prazo mínimo de preparação e preferências de canal. |
| Fontes e alertas | Última coleta bem-sucedida por fonte, falhas pendentes e avisos enviados, incluindo o motivo de cada atualização. |

Primeira entrega sugerida: uma lista filtrável, uma ficha detalhada e um perfil salvo. Importe os dados da coleta a partir do SQLite e teste com três registros sintéticos: edital aberto, vencido e retificado. Habilite alertas quando a ligação com a fonte e o histórico de alterações estiverem visíveis no painel.
