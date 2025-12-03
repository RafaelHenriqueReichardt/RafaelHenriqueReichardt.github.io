### 1. Descrição e Modelagem do Problema

**Cenário escolhido:**

O problema que estamos modelando é o sistema de agendamento de quartos de um hotel. O objetivo é criar uma representação lógica para a gestão de reservas, onde o sistema deve verificar a disponibilidade dos quartos e garantir que as regras do hotel sejam seguidas (ex: não permitir mais de uma reserva para o mesmo quarto no mesmo horário).

**Entidades, Relações, Restrições e Regras:**

* **Entidades**:

  * **Quartos**: Cada quarto tem um número de identificação único.
  * **Reservas**: Cada reserva é associada a um cliente e a um quarto específico em um intervalo de tempo.
  * **Clientes**: Cada cliente tem um identificador único, nome, e detalhes de contato.
* **Relações**:

  * **Reserva de Quartos**: Um cliente pode fazer uma reserva para um quarto em um período de tempo específico.
  * **Disponibilidade de Quartos**: Um quarto pode ser reservado por vários clientes, mas não pode ser reservado por dois clientes no mesmo período de tempo.
* **Restrições**:

  * Um cliente pode ter várias reservas, mas cada reserva se aplica a um quarto e a um período de tempo específico.
  * Um quarto não pode ser reservado para mais de um cliente no mesmo horário.
  * Os quartos têm um limite de capacidade (ex: 2 pessoas por quarto).
* **Regras**:

  * Se um quarto já estiver reservado, não é possível realizar outra reserva no mesmo intervalo de tempo.
  * Os clientes devem ser notificados quando uma reserva for realizada com sucesso ou não.

**Versão Formal do Cenário:**

* ( Quarto(q) ) representa a existência de um quarto ( q ).
* ( Cliente(c) ) representa a existência de um cliente ( c ).
* ( Reserva(c, q, t1, t2) ) significa que o cliente ( c ) fez uma reserva para o quarto ( q ) no intervalo de tempo entre ( t1 ) e ( t2 ).
* ( Disponivel(q, t1, t2) ) indica que o quarto ( q ) está disponível no intervalo de tempo ( [t1, t2] ).

**Exemplo Formal:**

* Se ( Reserva(c_1, q_1, t_1, t_2) ) e ( Reserva(c_2, q_1, t_1, t_2) ), então ( c_1 ) e ( c_2 ) não podem ser duas reservas no mesmo intervalo de tempo para o quarto ( q_1 ), ou seja, uma dessas reservas seria inválida.

---

### 2. Lógica Proposicional

**Definição das proposições:**

* ( P_1 ): O quarto ( q ) está disponível no intervalo ( [t1, t2] ).
* ( P_2 ): O cliente ( c ) fez uma reserva para o quarto ( q ) no intervalo ( [t1, t2] ).
* ( P_3 ): O quarto ( q ) não está disponível no intervalo ( [t1, t2] ).

**Fórmulas Bem Formadas (FBFs):**

* ( \neg P_1 \rightarrow P_2 ): Se o quarto não está disponível, então uma reserva foi feita.
* ( P_1 \rightarrow \neg P_2 ): Se o quarto está disponível, então não há reserva feita.

**Simplificação das FBFs:**

* A fórmula ( \neg P_1 \rightarrow P_2 ) é equivalente a ( P_1 \vee P_2 ) (pelo teorema da implicação).

**Análise semântica (Tabelas-verdade):**

A tabela verdade para a proposição ( P_1 \vee P_2 ):

| ( P_1 ) | ( P_2 ) | ( P_1 \vee P_2 ) |
| ------- | ------- | ---------------- |
| T       | T       | T                |
| T       | F       | T                |
| F       | T       | T                |
| F       | F       | F                |

---

### 3. Dedução Natural

**Exemplo 1**: Suponha que queremos deduzir a possibilidade de uma reserva ser válida.

1. ( \neg P_1 ) (o quarto não está disponível).
2. ( \neg P_1 \rightarrow P_2 ) (Se o quarto não está disponível, então foi feita uma reserva).
3. Concluímos ( P_2 ) (foi feita uma reserva).

**Exemplo 2**: Deduzindo que, se o quarto está disponível, então uma reserva não foi feita.

1. ( P_1 ) (o quarto está disponível).
2. ( P_1 \rightarrow \neg P_2 ) (Se o quarto está disponível, então não foi feita uma reserva).
3. Concluímos ( \neg P_2 ) (não foi feita uma reserva).

---

### 4. Resolução Proposicional

**Converter fórmulas para CNF**:

* Fórmula ( \neg P_1 \rightarrow P_2 ) pode ser reescrita em CNF como ( P_1 \vee P_2 ).
* Fórmula ( P_1 \rightarrow \neg P_2 ) pode ser reescrita como ( \neg P_1 \vee \neg P_2 ).

**Aplicando a resolução**:

A partir da CNF, podemos aplicar a resolução:

1. ( P_1 \vee P_2 )
2. ( \neg P_1 \vee \neg P_2 )

Resolvendo ( P_1 ) e ( \neg P_1 ), temos ( P_2 \vee \neg P_2 ), que resulta em uma contradição (pois sempre será verdade). Isso indica que, se o quarto está disponível, não pode haver uma reserva conflitante.

---

### 5. Lógica de Predicados

**Definição de Predicados, Funções, Variáveis e Domínios**:

* ( Reserva(c, q, t1, t2) ) indica que o cliente ( c ) fez uma reserva no quarto ( q ) entre os horários ( t1 ) e ( t2 ).
* ( Disponivel(q, t1, t2) ) indica que o quarto ( q ) está disponível entre ( t1 ) e ( t2 ).
* O domínio de ( c ) (clientes), ( q ) (quartos), e ( t1, t2 ) (tempo) são conjuntos específicos.

**Formalizando o problema**:

* ( \forall c \forall q \forall t_1 \forall t_2 (Reserva(c, q, t_1, t_2) \rightarrow \neg \exists c' \exists t_1' \exists t_2' (Reserva(c', q, t_1', t_2') \wedge t_1 < t_2' \wedge t_2 > t_1')) ).

**Exemplo de sentença**:

* ( \forall c \exists q \exists t_1 \exists t_2 (Reserva(c, q, t_1, t_2) \rightarrow Disponivel(q, t_1, t_2)) ).

---

### 6. Semântica de Predicados

**Modelos**:

Um modelo para a lógica de predicados poderia ser um conjunto ( M ) que define o valor de verdade para cada predicado, função e variável no domínio, com base na interpretação dos termos. Por exemplo:

* ( M = { Reserva(c_1, q_1, t_1, t_2), Disponivel(q_2, t_1, t_2) } )

**Validade, Satisfatibilidade e Contradições**:

* A fórmula será **válida** se, para toda interpretação do modelo, ela for verdadeira.
* A fórmula será **satisfatível** se houver pelo menos um modelo em que ela seja verdadeira.
* Se a fórmula contiver contradições (como no caso de duas reservas conflitantes), ela será **insatisfatível**.

---

### 7. Substituição, Unificação e Resolução (Predicados)

**Exemplo de substituição**:

* Se temos ( Reserva(c, q, t_1, t_2) ), podemos substituir ( c ) por ( c_1 ), ( q ) por ( q_1 ), etc., para criar uma instância mais específica da fórmula.

**Unificação**:

* Unificar ( Reserva(c_1, q_1, t_1, t_2) ) com ( Reserva(c_2, q_1, t_1, t_2) ) resultaria em uma falha, pois ( c_1 \neq c_2 ).

**Resolução de Predicados**:

* Resolvendo ( Reserva(c_1, q_1, t_1, t_2) ) com ( Reserva(c_2, q_1, t_1, t_2) ), obtemos uma contradição, indicando que duas reservas não podem ser feitas para o mesmo quarto no mesmo horário.

---

### 8. Parte Computacional

**Verificação Automática (Código em Python)**:

Aqui está um exemplo simples de código Python para verificar


se duas reservas são conflitantes:

```python
def verifica_conflito(reserva1, reserva2):
    # Reserva no formato (cliente, quarto, t1, t2)
    c1, q1, t1_1, t2_1 = reserva1
    c2, q2, t1_2, t2_2 = reserva2

    # Verificar se as reservas são para o mesmo quarto e se há sobreposição de tempo
    if q1 == q2 and not (t2_1 <= t1_2 or t2_2 <= t1_1):
        return True  # Há conflito
    return False  # Não há conflito

# Teste
reserva1 = ('c1', 'q1', 10, 12)
reserva2 = ('c2', 'q1', 11, 13)

print(verifica_conflito(reserva1, reserva2))  # Deve retornar True
```

**Autômato**:

Um autômato simples pode ser usado para gerenciar o estado das reservas. Ele teria dois estados principais: `disponível` e `reservado`.

---

### 9. Conclusões e Aplicações

* **Conexão com aplicações reais**: A modelagem lógica e computacional de sistemas de agendamento de quartos é útil para automação de processos de hotelaria. Ela pode ser aplicada em sistemas de gerenciamento de reservas online, integrados com plataformas como Booking, Airbnb, etc.

* **Benefícios**: A modelagem lógica ajuda a evitar inconsistências no sistema e garante que as regras do hotel sejam cumpridas automaticamente. A verificação de conflitos e a resolução de predicados são fundamentais para validar as reservas.

* **Limitações**: A complexidade computacional pode aumentar conforme o número de quartos, clientes e reservas cresce. A modelagem também pode não ser 100% intuitiva em sistemas mais complexos.

* **Potenciais melhorias**: A adição de mais regras, como políticas de cancelamento ou descontos, pode ser feita, mas exigirá expandir as fórmulas e a lógica de dedução para acomodar esses novos casos.
