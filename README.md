# Projeto Grupo 5

Isaac | Caio | Maria Gabriele | Maria Vitoria

---

## 📊 Avaliação do Código HTML

**Nota Final: 4,5/10** = Ponto_Extra 5 = 9.5

### ✅ Pontos Positivos

1. **Estrutura Semântica Básica** (+2,0)
   - Uso correto de `<header>`, `<main>`, `<footer>`
   - Tentativa de organização semântica do conteúdo
   - DOCTYPE correto e meta tags essenciais presentes

2. **Formulário Funcional** (+1,5)
   - Form estruturado com labels e inputs
   - Uso de tipo `date` apropriado
   - Atributo `name` presente nos inputs

3. **Indentação Razoável** (+2,0)
   - Código possui indentação e é legível
   - Organização visual aceitável

### ❌ Problemas Críticos

#### 1. **Erros na Estrutura da Tabela** (-2,0)
- `<thead>` está vazio
- `<th>` dentro de `<tbody>` (posição incorreta)
- `<td>` aninhadas em `<th>` (estrutura inválida)

**Correção necessária:**
```html
<table>
    <thead>
        <tr>
            <th>Dias</th>
            <th>Horários</th>
            <th>Turma</th>
            <th>Professor</th>
        </tr>
    </thead>
    <tbody>
        <!-- dados aqui -->
    </tbody>
</table>
```

#### 2. **Labels Não Associadas Corretamente** (-1,5)
- Atributo `for=""` vazio não corresponde a nenhum `id`
- Reduz acessibilidade do formulário

**Correção necessária:**
```html
<label for="nome_professor">Nome do Professor</label>
<input type="text" name="nome_professor" id="nome_professor">
```

#### 3. **Tipo de Input Incorreto** (-1,0)
- Horário usando `type="date"` quando deveria ser `type="time"`

#### 4. **Falta de Semântica** (-1,0)
- `<aside>` usado incorretamente como formulário
- Falta de `<section>` para organizar conteúdo
- Títulos vazios `<h2></h2>`
- Sem uso de `<nav>`

#### 5. **Problemas Menores** (-0,5)
- Select sem label associada
- Inputs do select sem value adequado
- Falta atributos `required`, `placeholder`

### 🎯 Recomendações

1. ✏️ Corrigir a estrutura da tabela imediatamente
2. 🏷️ Associar todos os labels aos inputs com `for` e `id`
3. 🎨 Usar `<section>` para organizar melhor o conteúdo
4. ⏰ Mudar input horário para `type="time"`
5. 📋 Adicionar atributos `required` e `placeholder`
6. ♿ Melhorar acessibilidade do formulário

---

**Arquivo avaliado:** [index.html](https://github.com/FranciscoDias87/prova-projetores-grupo5/blob/master/index.html)

# Avaliação: **7/10 + Ponto_Extra 5 = 10**

## Análise Geral

O código demonstra **compreensão dos conceitos fundamentais** de JavaScript e DOM manipulation, apropriada para alunos iniciantes. No entanto, há **problemas lógicos importantes** e falta de estruturação que impedem uma nota maior.

---

## ✅ Pontos Positivos

1. **Seleção correta do DOM** - Uso adequado de `querySelector`
2. **Validação de campos** - Verifica campos vazios
3. **Validação de data** - Impede datas passadas (bom thinking!)
4. **Uso de localStorage** - Demonstra conhecimento de persistência de dados
5. **Estrutura clara** - Código legível e bem indentado
6. **Criação dinâmica de elementos** - `createElement` e `innerHTML` usados corretamente

---

## ❌ Problemas Críticos

### 1. **Erro de Typo - Variável não declarada** ⚠️
```javascript
const contactlnfo = document.querySelector('#contactlnfo').value; // ❌ "lnfo"
// ...
contactInfo // ❌ Usado como "Info" depois
```
**Impacto**: O código vai quebrar com erro `ReferenceError`

### 2. **Lógica de validação fora de escopo** 🔴
```javascript
const teacherName = document.querySelector('#teacher-name').value;
// ... validações ...
if (teacherName === '' || ...) {
    alert('Preencha todos os campos!');
    return; // ❌ return NÃO funciona fora de função!
}
```
**Impacto**: As validações nunca vão parar a execução - o código continua mesmo com erro

### 3. **reservationDatabase sempre vazio** 🔴
```javascript
const reservationDatabase = [];
// ... adiciona item ...
reservationDatabase.push(newReservation);

// ... depois ...
const savedReservations = JSON.parse(localStorage.getItem('reservations')) || [];
// ❌ Nunca usa savedReservations!
```
**Impacto**: Os dados salvos no localStorage nunca são carregados. A cada reload, o array fica vazio.

### 4. **Verificação de disponibilidade inútil** 🟡
```javascript
const isReserved = reservationDatabase.some(...);
// ❌ Calcula mas nunca usa a variável!
```
**Impacto**: A verificação de conflitos não faz nada.

### 5. **Event listener no lugar errado** 🟡
As validações e a criação de reservas estão **fora da função do event listener**. Devem estar **dentro**, senão executam imediatamente ao carregar a página.

---

## 🔧 Sugestões de Melhoria

```javascript
const reservationForm = document.querySelector('#reservation-form');
const reservationList = document.querySelector('#reservation-list');
let reservationDatabase = JSON.parse(localStorage.getItem('reservations')) || [];

// Função auxiliar para renderizar tabela
function renderReservations() {
    reservationList.innerHTML = '';
    reservationDatabase.forEach(res => {
        const tableRow = document.createElement('tr');
        tableRow.innerHTML = `
            <td>${res.teacherName}</td>
            <td>${res.reservationDate}</td>
            <td>${res.startTime}</td>
            <td>${res.projectorModel}</td>
            <td>${res.contactInfo}</td>
        `;
        reservationList.appendChild(tableRow);
    });
}

reservationForm.addEventListener('submit', function(event) {
    event.preventDefault();
    
    const teacherName = document.querySelector('#teacher-name').value;
    const reservationDate = document.querySelector('#reservationDate').value;
    const startTime = document.querySelector('#startTime').value;
    const projectorModel = document.querySelector('#projectorModel').value;
    const contactInfo = document.querySelector('#contactInfo').value; // ✅ Corrigido typo

    // Validações
    if (!teacherName || !reservationDate || !startTime) {
        alert('Preencha todos os campos!');
        return;
    }

    const currentDate = new Date().toISOString().split('T')[0];
    if (reservationDate < currentDate) {
        alert('Não é permitido agendar datas passadas!');
        return;
    }

    // Verifica conflito
    const isReserved = reservationDatabase.some(res => 
        res.projectorModel === projectorModel &&
        res.reservationDate === reservationDate &&
        res.startTime === startTime
    );

    if (isReserved) {
        alert('Projetor já reservado neste horário!');
        return;
    }

    // Adiciona reserva
    const newReservation = { teacherName, reservationDate, startTime, projectorModel, contactInfo };
    reservationDatabase.push(newReservation);

    // Salva e renderiza
    localStorage.setItem('reservations', JSON.stringify(reservationDatabase));
    renderReservations();
    reservationForm.reset();
});

// Renderiza dados ao carregar
renderReservations();
```

---

## Resumo

| Aspecto | Score |
|--------|-------|
| Sintaxe | 8/10 |
| Lógica | 5/10 |
| Estrutura | 7/10 |
| Tratamento de Erros | 4/10 |
| **Média Final** | **7/10** |

**Recomendação**: Ótimo começo! Corrigir os bugs e reorganizar o código dentro do event listener. Depois disso, considerar aprender sobre **funções**, **classes** e **modularização**. 🚀
