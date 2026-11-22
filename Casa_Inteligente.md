# Casa Inteligente

Projeto **ExpoTech 2026**. A proposta é
desenvolver uma solução de casa inteligente com cadastro e
acompanhamento de equipamentos e manutenções, além de automação de
notificações.

## Objetivo

Apoiar o gerenciamento de equipamentos e manutenções, integrando a
aplicação desenvolvida no Bubble a recursos de automação para avisar os
responsáveis quando uma manutenção exigir atenção.

## Tecnologias e ferramentas

  -----------------------------------------------------------------------
  Tecnologia                          Utilização no projeto
  ----------------------------------- -----------------------------------
  Bubble                              Construção da aplicação e
                                      gerenciamento dos dados

  Make                                 Automação do fluxo de notificações

  JavaScript                          Cálculo dos dias restantes no node
                                      Code do Make

  Python                              Classificação de manutenção,
                                      conforme o planejamento da equipe

  GitHub                              Controle de versão, armazenamento e
                                      documentação
  -----------------------------------------------------------------------

## Fluxo de notificações

``` text
Bubble → Webhook (Make) → Code → IF → Outlook
```

1.  **Bubble:** envia os dados da manutenção por uma requisição HTTP.
2.  **Webhook:** recebe a requisição POST no Make.
3.  **Code:** calcula quantos dias faltam para a data prevista.
4.  **IF:** avalia as condições para decidir se deve notificar.
5.  **Outlook:** envia o aviso ao responsável quando as condições são
    atendidas.

### Regra de notificação

``` text
dias_restantes <= 3 E status != "Concluída"
```

As duas condições devem ser verdadeiras ao mesmo tempo. Manutenções
atrasadas também se enquadram na condição de prazo, pois apresentam um
número negativo de dias restantes.

## Dados de entrada

Exemplo ilustrativo do JSON enviado ao fluxo:

``` json
{
  "equipamento": "Compressor 01",
  "tipo_manutencao": "Preventiva",
  "data_manutencao": "2026-11-20",
  "responsavel": "João Silva",
  "email_responsavel": "joao@empresa.com",
  "status": "Agendada"
}
```

  Campo                 Tipo                    Descrição
  --------------------- ----------------------- --------------------------------------
  `equipamento`         String                  Nome ou identificação do equipamento
  `tipo_manutencao`     String                  Tipo de manutenção
  `data_manutencao`     String (`AAAA-MM-DD`)   Data prevista
  `responsavel`         String                  Nome do responsável
  `email_responsavel`   String                  E-mail de destino
  `status`              String                  Situação da manutenção


### Automação Make

-   Workflow: **Notificação de Manutenção**
-   Método HTTP: `POST`
-   Caminho sugerido no guia: `manutencao`


  -----------------------------------------------------------------------
  Cenário                             Resultado esperado
  ----------------------------------- -----------------------------------
  Manutenção daqui a 3 dias e status  Enviar e-mail
  diferente de Concluída              

  Manutenção daqui a 30 dias          Não enviar e-mail

  Manutenção com data passada e       Enviar e-mail
  status diferente de Concluída       

  Status igual a Concluída            Não enviar e-mail
  -----------------------------------------------------------------------
  

## Equipe e responsabilidades

Confirme os nomes e a divisão final antes de publicar:

  -----------------------------------------------------------------------
  Integrante   RA                     Responsabilidade registrada no
                                      planejamento
  ----------------------------------- -----------------------------------
  Eduarda     274232                  Estrutura do aplicativo no Bubble;
                                      integração Bubble + Make com Rafa;
                                      testes

  Gabriel     187249                  Repositório e documentação; organização
                                      de tarefas usando Scrum e kanban
                                      no Trello
                                      
  Rafael      277673                  Classificação de manutenção em
                                      Python; testes da classificação

  João        291542                  Workflow de notificações no Make;
                                      integração Bubble + Make com Eduarda

  Artur                               Repositório e documentação;
                                      organização das evidências com a
                                      equipe

  Todos                               Evidências, teste do fluxo completo
                                      e apresentação final
  -----------------------------------------------------------------------

## Documentação complementar

-   Documentação técnica: **[Documentacao_Casa_em_Dia_2050_Python_atualizada (2).docx](https://github.com/user-attachments/files/35235325/Documentacao_Casa_em_Dia_2050_Python_atualizada.2.docx)
**

------------------------------------------------------------------------
