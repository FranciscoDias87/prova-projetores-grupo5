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
