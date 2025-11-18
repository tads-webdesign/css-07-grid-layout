# Tutorial CSS Grid Layout - Guia Completo para Iniciantes

## 📚 Sumário

1. [Introdução ao CSS Grid](#introdução-ao-css-grid)
   - [O que é CSS Grid?](#o-que-é-css-grid)
   - [Quando usar CSS Grid?](#quando-usar-css-grid)
2. [Grid Container](#grid-container)
   - [display: grid](#display-grid)
   - [grid-template-columns](#grid-template-columns)
   - [grid-template-rows](#grid-template-rows)
   - [gap](#gap)
3. [Grid Items](#grid-items)
   - [grid-column](#grid-column)
   - [grid-row](#grid-row)
   - [grid-area](#grid-area)
4. [Design Responsivo com Media Queries](#design-responsivo-com-media-queries)
5. [Exemplo Completo](#exemplo-completo)

---

## Introdução ao CSS Grid

### O que é CSS Grid?

CSS Grid Layout é um sistema de layout bidimensional que permite criar layouts complexos de forma mais eficiente e com controle total sobre linhas e colunas. É uma das ferramentas mais poderosas do CSS3 para criar designs modernos e responsivos.

**Características principais:**
- Layout bidimensional (linhas e colunas simultaneamente)
- Alinhamento preciso de elementos
- Controle granular do espaçamento
- Responsividade facilitada
- Redução de código HTML e CSS

### Quando usar CSS Grid?

Use CSS Grid quando você precisar:

- ✅ Criar layouts de página completos
- ✅ Organizar conteúdo em linhas E colunas
- ✅ Alinhar elementos de forma precisa
- ✅ Criar layouts responsivos complexos
- ✅ Sobrepor elementos de forma controlada
- ✅ Criar galerias de imagens ou produtos

**Grid vs Flexbox:**
- **Flexbox**: Unidimensional (linha OU coluna) - melhor para componentes
- **Grid**: Bidimensional (linhas E colunas) - melhor para layouts completos

> 💡 **Dica:** Grid e Flexbox podem (e devem) ser usados juntos! Use Grid para o layout geral e Flexbox para componentes internos.

---

## Grid Container

O Grid Container é o elemento pai que contém todos os grid items. Para transformar um elemento em grid container, usamos a propriedade `display: grid`.

### display: grid

A propriedade `display: grid` ativa o CSS Grid em um elemento.

**Sintaxe:**
```css
.container {
  display: grid;
}
```

**Exemplo prático:**

HTML:
```html
<div class="container">
  <div class="item">Item 1</div>
  <div class="item">Item 2</div>
  <div class="item">Item 3</div>
</div>
```

CSS:
```css
.container {
  display: grid;
  background-color: #f0f0f0;
  padding: 10px;
}

.item {
  background-color: #4CAF50;
  color: white;
  padding: 20px;
  text-align: center;
  border: 1px solid #fff;
}
```

**Resultado:** Os itens ficarão empilhados verticalmente (comportamento padrão).

---

### grid-template-columns

Define o número e o tamanho das colunas no grid.

**Sintaxe:**
```css
.container {
  grid-template-columns: valor1 valor2 valor3 ...;
}
```

**Unidades disponíveis:**
- `px` - pixels fixos
- `%` - porcentagem do container
- `fr` - fração do espaço disponível (recomendado)
- `auto` - tamanho automático baseado no conteúdo
- `minmax(min, max)` - valor mínimo e máximo

**Exemplos:**

**Exemplo 1: Três colunas iguais**
```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  /* ou use a função repeat: */
  grid-template-columns: repeat(3, 1fr);
}
```

**Exemplo 2: Colunas com tamanhos diferentes**
```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr 2fr;
  /* primeira coluna: 200px fixos
     segunda coluna: 1 fração
     terceira coluna: 2 frações (dobro da segunda) */
}
```

**Exemplo 3: Layout sidebar + conteúdo**
```css
.container {
  display: grid;
  grid-template-columns: 250px 1fr;
  /* sidebar fixa de 250px + conteúdo flexível */
}
```

**Exemplo 4: Grid responsivo automático**
```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  /* cria colunas automaticamente com mínimo de 200px */
}
```

---

### grid-template-rows

Define o número e o tamanho das linhas no grid.

**Sintaxe:**
```css
.container {
  grid-template-rows: valor1 valor2 valor3 ...;
}
```

**Exemplo 1: Três linhas com tamanhos diferentes**
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 100px 200px 100px;
}
```

**Exemplo 2: Header, conteúdo e footer**
```css
.container {
  display: grid;
  grid-template-rows: 80px 1fr 60px;
  min-height: 100vh;
  /* header: 80px
     conteúdo: espaço restante
     footer: 60px */
}
```

**Exemplo 3: Linhas iguais**
```css
.container {
  display: grid;
  grid-template-rows: repeat(4, 150px);
  /* 4 linhas de 150px cada */
}
```

---

### gap

Define o espaçamento entre linhas e colunas do grid.

**Sintaxe:**
```css
.container {
  gap: valor;                    /* mesmo valor para linhas e colunas */
  gap: valor-linha valor-coluna; /* valores diferentes */
  
  /* ou use as propriedades específicas: */
  row-gap: valor;
  column-gap: valor;
}
```

**Exemplo 1: Gap uniforme**
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  /* 20px de espaço entre todas as células */
}
```

**Exemplo 2: Gaps diferentes**
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 30px 15px;
  /* 30px entre linhas, 15px entre colunas */
}
```

**Exemplo 3: Apenas gap vertical**
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  row-gap: 25px;
  column-gap: 0;
}
```

> 💡 **Dica:** `gap` é melhor que usar margins nos items, pois não adiciona espaço nas bordas externas.

---

## Grid Items

Grid Items são os elementos filhos diretos de um Grid Container. Podemos controlar sua posição e tamanho com propriedades específicas.

### grid-column

Define em quais colunas o item deve se posicionar.

**Sintaxe:**
```css
.item {
  grid-column: início / fim;
  /* ou */
  grid-column-start: valor;
  grid-column-end: valor;
  /* ou ainda */
  grid-column: início / span quantidade;
}
```

**Como funciona a numeração:**
- As linhas da grade são numeradas começando em 1
- Cada coluna tem uma linha de início e uma de fim
- Você pode contar do fim usando números negativos

**Exemplo 1: Item ocupando 2 colunas**
```css
.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

.item-destaque {
  grid-column: 1 / 3;
  /* ocupa da linha 1 até a linha 3 (2 colunas) */
}
```

**Exemplo 2: Usando span**
```css
.item-largo {
  grid-column: span 2;
  /* ocupa 2 colunas a partir de sua posição */
}
```

**Exemplo 3: Item ocupando toda a largura**
```css
.item-full {
  grid-column: 1 / -1;
  /* do início até o fim do grid */
}
```

**Exemplo completo:**
```html
<div class="container">
  <div class="item item-1">1</div>
  <div class="item item-2">2 (largo)</div>
  <div class="item item-3">3</div>
  <div class="item item-4">4</div>
</div>
```

```css
.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

.item-2 {
  grid-column: 2 / 4; /* ocupa colunas 2 e 3 */
  background-color: #ff6b6b;
}
```

---

### grid-row

Define em quais linhas o item deve se posicionar.

**Sintaxe:**
```css
.item {
  grid-row: início / fim;
  /* ou */
  grid-row-start: valor;
  grid-row-end: valor;
  /* ou ainda */
  grid-row: início / span quantidade;
}
```

**Exemplo 1: Item ocupando 2 linhas**
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 100px;
  gap: 10px;
}

.item-alto {
  grid-row: 1 / 3;
  /* ocupa da linha 1 até a linha 3 (2 linhas) */
}
```

**Exemplo 2: Sidebar vertical**
```css
.sidebar {
  grid-column: 1;
  grid-row: 1 / -1;
  /* ocupa todas as linhas da primeira coluna */
}
```

**Exemplo 3: Combinando column e row**
```css
.item-grande {
  grid-column: 2 / 4;  /* 2 colunas */
  grid-row: 1 / 3;     /* 2 linhas */
  /* cria um item 2x2 */
}
```

---

### grid-area

Define a área do grid que o item deve ocupar. Pode ser usado de duas formas:

**Forma 1: Shorthand para posicionamento**
```css
.item {
  grid-area: row-start / column-start / row-end / column-end;
}
```

**Forma 2: Nome de área (com grid-template-areas)**
```css
.item {
  grid-area: nome-da-area;
}
```

**Exemplo 1: Posicionamento com grid-area**
```css
.item {
  grid-area: 1 / 1 / 3 / 3;
  /* linha-início / coluna-início / linha-fim / coluna-fim */
}
```

**Exemplo 2: Layout com áreas nomeadas**
```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: 80px 1fr 60px;
  grid-template-areas:
    "header  header  header"
    "sidebar content aside"
    "footer  footer  footer";
  gap: 10px;
  min-height: 100vh;
}

.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.content { grid-area: content; }
.aside   { grid-area: aside; }
.footer  { grid-area: footer; }
```

**Exemplo 3: Layout de card**
```css
.card {
  display: grid;
  grid-template-columns: 100px 1fr;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "imagem titulo"
    "imagem descricao"
    "imagem botao";
  gap: 15px;
}

.card-imagem    { grid-area: imagem; }
.card-titulo    { grid-area: titulo; }
.card-descricao { grid-area: descricao; }
.card-botao     { grid-area: botao; }
```

> 💡 **Dica:** Usar `grid-template-areas` torna o código mais legível e fácil de manter!

---

## Design Responsivo com Media Queries

Media queries permitem adaptar o layout do grid para diferentes tamanhos de tela.

### Estratégia Mobile-First

É recomendado começar com o design mobile e adicionar complexidade para telas maiores.

**Exemplo 1: Layout simples que se adapta**

```css
/* Mobile first - 1 coluna por padrão */
.container {
  display: grid;
  grid-template-columns: 1fr;
  gap: 20px;
  padding: 15px;
}

/* Tablets - 2 colunas */
@media (min-width: 768px) {
  .container {
    grid-template-columns: repeat(2, 1fr);
    gap: 25px;
    padding: 20px;
  }
}

/* Desktop - 3 colunas */
@media (min-width: 1024px) {
  .container {
    grid-template-columns: repeat(3, 1fr);
    gap: 30px;
    padding: 30px;
  }
}

/* Desktop grande - 4 colunas */
@media (min-width: 1440px) {
  .container {
    grid-template-columns: repeat(4, 1fr);
    gap: 40px;
  }
}
```

**Exemplo 2: Layout com sidebar responsivo**

```css
/* Mobile - stack vertical */
.layout {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-areas:
    "header"
    "main"
    "sidebar"
    "footer";
  gap: 15px;
}

/* Tablet e Desktop - sidebar lateral */
@media (min-width: 768px) {
  .layout {
    grid-template-columns: 1fr 300px;
    grid-template-areas:
      "header  header"
      "main    sidebar"
      "footer  footer";
    gap: 20px;
  }
}

/* Desktop grande - layout com 3 colunas */
@media (min-width: 1200px) {
  .layout {
    grid-template-columns: 250px 1fr 300px;
    grid-template-areas:
      "header header  header"
      "nav    main    sidebar"
      "footer footer  footer";
  }
}
```

**Exemplo 3: Galeria responsiva automática**

```css
.galeria {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
  padding: 20px;
}

/* Ajustes finos por breakpoint */
@media (max-width: 600px) {
  .galeria {
    grid-template-columns: 1fr;
    gap: 15px;
  }
}

@media (min-width: 1200px) {
  .galeria {
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 30px;
  }
}
```

**Exemplo 4: Cards que reorganizam**

```css
.cards {
  display: grid;
  gap: 20px;
}

/* Mobile - 1 coluna */
@media (max-width: 767px) {
  .cards {
    grid-template-columns: 1fr;
  }
  
  .card-destaque {
    grid-column: 1;
  }
}

/* Tablet - 2 colunas, card destaque ocupa 2 */
@media (min-width: 768px) and (max-width: 1023px) {
  .cards {
    grid-template-columns: repeat(2, 1fr);
  }
  
  .card-destaque {
    grid-column: 1 / -1;
  }
}

/* Desktop - 3 colunas */
@media (min-width: 1024px) {
  .cards {
    grid-template-columns: repeat(3, 1fr);
  }
  
  .card-destaque {
    grid-column: span 2;
    grid-row: span 2;
  }
}
```

### Dicas para Responsividade

1. **Use unidades relativas:** `fr`, `%`, `minmax()`, `auto-fit`, `auto-fill`
2. **Evite larguras fixas em pixels** quando possível
3. **Teste em vários dispositivos** ou use as DevTools do navegador
4. **Considere orientação:** use `@media (orientation: landscape)` se necessário
5. **Use `auto-fit` ou `auto-fill`** para grids que se adaptam automaticamente

---

## Exemplo Completo

Vamos criar um layout completo de um site com header, navegação, conteúdo principal, sidebar, e footer, totalmente responsivo.

### HTML Completo

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CSS Grid - Exemplo Completo</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  
  <!-- Layout Principal -->
  <div class="layout">
    
    <!-- Header -->
    <header class="header">
      <h1>Meu Site com CSS Grid</h1>
      <p>Layout responsivo e moderno</p>
    </header>
    
    <!-- Navegação -->
    <nav class="nav">
      <a href="#">Início</a>
      <a href="#">Sobre</a>
      <a href="#">Serviços</a>
      <a href="#">Contato</a>
    </nav>
    
    <!-- Conteúdo Principal -->
    <main class="main">
      <h2>Conteúdo Principal</h2>
      
      <!-- Grid de Cards -->
      <div class="cards">
        <article class="card card-destaque">
          <img src="https://via.placeholder.com/400x300" alt="Destaque">
          <h3>Artigo em Destaque</h3>
          <p>Este card ocupa mais espaço no layout desktop.</p>
          <a href="#" class="btn">Leia mais</a>
        </article>
        
        <article class="card">
          <img src="https://via.placeholder.com/400x300" alt="Imagem">
          <h3>Artigo 2</h3>
          <p>Descrição breve do artigo.</p>
          <a href="#" class="btn">Leia mais</a>
        </article>
        
        <article class="card">
          <img src="https://via.placeholder.com/400x300" alt="Imagem">
          <h3>Artigo 3</h3>
          <p>Descrição breve do artigo.</p>
          <a href="#" class="btn">Leia mais</a>
        </article>
        
        <article class="card">
          <img src="https://via.placeholder.com/400x300" alt="Imagem">
          <h3>Artigo 4</h3>
          <p>Descrição breve do artigo.</p>
          <a href="#" class="btn">Leia mais</a>
        </article>
        
        <article class="card">
          <img src="https://via.placeholder.com/400x300" alt="Imagem">
          <h3>Artigo 5</h3>
          <p>Descrição breve do artigo.</p>
          <a href="#" class="btn">Leia mais</a>
        </article>
      </div>
    </main>
    
    <!-- Sidebar -->
    <aside class="sidebar">
      <h3>Sidebar</h3>
      <div class="widget">
        <h4>Categorias</h4>
        <ul>
          <li><a href="#">Tecnologia</a></li>
          <li><a href="#">Design</a></li>
          <li><a href="#">CSS</a></li>
          <li><a href="#">JavaScript</a></li>
        </ul>
      </div>
      <div class="widget">
        <h4>Populares</h4>
        <ul>
          <li><a href="#">Post popular 1</a></li>
          <li><a href="#">Post popular 2</a></li>
          <li><a href="#">Post popular 3</a></li>
        </ul>
      </div>
    </aside>
    
    <!-- Footer -->
    <footer class="footer">
      <p>&copy; 2024 Meu Site. Desenvolvido com CSS Grid.</p>
    </footer>
    
  </div>
  
</body>
</html>
```

### CSS Completo

```css
/* Reset básico */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  line-height: 1.6;
  color: #333;
  background-color: #f5f5f5;
}

/* ===== LAYOUT PRINCIPAL (MOBILE FIRST) ===== */

.layout {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-areas:
    "header"
    "nav"
    "main"
    "sidebar"
    "footer";
  gap: 0;
  min-height: 100vh;
}

/* ===== HEADER ===== */

.header {
  grid-area: header;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 30px 20px;
  text-align: center;
}

.header h1 {
  font-size: 2rem;
  margin-bottom: 10px;
}

.header p {
  font-size: 1.1rem;
  opacity: 0.9;
}

/* ===== NAVEGAÇÃO ===== */

.nav {
  grid-area: nav;
  background-color: #2c3e50;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 0;
}

.nav a {
  color: white;
  text-decoration: none;
  padding: 15px 20px;
  display: block;
  transition: background-color 0.3s;
}

.nav a:hover {
  background-color: #34495e;
}

/* ===== CONTEÚDO PRINCIPAL ===== */

.main {
  grid-area: main;
  background-color: white;
  padding: 30px 20px;
}

.main h2 {
  color: #667eea;
  margin-bottom: 30px;
  font-size: 1.8rem;
}

/* ===== GRID DE CARDS ===== */

.cards {
  display: grid;
  grid-template-columns: 1fr;
  gap: 20px;
  margin-top: 20px;
}

.card {
  background-color: #fff;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
  transition: transform 0.3s, box-shadow 0.3s;
  display: flex;
  flex-direction: column;
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(0,0,0,0.2);
}

.card img {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.card h3 {
  padding: 15px 20px 10px;
  color: #2c3e50;
  font-size: 1.3rem;
}

.card p {
  padding: 0 20px;
  color: #666;
  flex-grow: 1;
}

.card .btn {
  display: inline-block;
  margin: 15px 20px 20px;
  padding: 10px 20px;
  background-color: #667eea;
  color: white;
  text-decoration: none;
  border-radius: 5px;
  transition: background-color 0.3s;
  text-align: center;
}

.card .btn:hover {
  background-color: #764ba2;
}

/* ===== SIDEBAR ===== */

.sidebar {
  grid-area: sidebar;
  background-color: #f9f9f9;
  padding: 30px 20px;
  border-left: 3px solid #667eea;
}

.sidebar h3 {
  color: #667eea;
  margin-bottom: 20px;
  font-size: 1.5rem;
}

.widget {
  background-color: white;
  padding: 20px;
  margin-bottom: 20px;
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.05);
}

.widget h4 {
  color: #2c3e50;
  margin-bottom: 15px;
  font-size: 1.1rem;
}

.widget ul {
  list-style: none;
}

.widget ul li {
  padding: 8px 0;
  border-bottom: 1px solid #eee;
}

.widget ul li:last-child {
  border-bottom: none;
}

.widget a {
  color: #667eea;
  text-decoration: none;
  transition: color 0.3s;
}

.widget a:hover {
  color: #764ba2;
}

/* ===== FOOTER ===== */

.footer {
  grid-area: footer;
  background-color: #2c3e50;
  color: white;
  text-align: center;
  padding: 25px 20px;
}

/* ===== MEDIA QUERIES - RESPONSIVIDADE ===== */

/* Tablets - a partir de 768px */
@media (min-width: 768px) {
  .layout {
    grid-template-columns: 1fr;
    grid-template-areas:
      "header"
      "nav"
      "main"
      "sidebar"
      "footer";
  }
  
  .header h1 {
    font-size: 2.5rem;
  }
  
  .nav {
    justify-content: flex-start;
    padding: 0 20px;
  }
  
  /* Cards em 2 colunas */
  .cards {
    grid-template-columns: repeat(2, 1fr);
    gap: 25px;
  }
  
  /* Card destaque ocupa 2 colunas */
  .card-destaque {
    grid-column: 1 / -1;
  }
}

/* Desktop - a partir de 1024px */
@media (min-width: 1024px) {
  .layout {
    grid-template-columns: 1fr 300px;
    grid-template-areas:
      "header  header"
      "nav     nav"
      "main    sidebar"
      "footer  footer";
    gap: 0;
    max-width: 1400px;
    margin: 0 auto;
  }
  
  .main {
    padding: 40px;
  }
  
  .sidebar {
    padding: 40px 30px;
  }
  
  /* Cards em 2 colunas no desktop */
  .cards {
    grid-template-columns: repeat(2, 1fr);
    gap: 30px;
  }
  
  /* Card destaque ocupa 2 colunas e 2 linhas */
  .card-destaque {
    grid-column: 1 / -1;
    grid-row: span 1;
  }
}

/* Desktop grande - a partir de 1200px */
@media (min-width: 1200px) {
  .layout {
    grid-template-columns: 250px 1fr 320px;
    grid-template-areas:
      "header header  header"
      "nav    nav     nav"
      "sidebar main   main"
      "footer footer  footer";
  }
  
  .nav {
    padding: 0 40px;
  }
  
  .main {
    padding: 50px;
  }
  
  /* Cards em 3 colunas */
  .cards {
    grid-template-columns: repeat(3, 1fr);
    gap: 30px;
  }
  
  /* Card destaque ocupa 2 colunas */
  .card-destaque {
    grid-column: span 2;
    grid-row: span 2;
  }
  
  .card-destaque img {
    height: 300px;
  }
}

/* Desktop muito grande - a partir de 1600px */
@media (min-width: 1600px) {
  .layout {
    max-width: 1600px;
  }
  
  /* Cards em 4 colunas */
  .cards {
    grid-template-columns: repeat(4, 1fr);
    gap: 35px;
  }
  
  /* Card destaque ainda ocupa 2 colunas */
  .card-destaque {
    grid-column: span 2;
    grid-row: span 2;
  }
}
```

### Explicação do Exemplo Completo

Este exemplo demonstra:

1. **Layout Principal com Grid:**
   - Usa `grid-template-areas` para definir as áreas
   - Layout flexível que se reorganiza em diferentes telas

2. **Mobile First:**
   - Começa com 1 coluna (mobile)
   - Adiciona complexidade progressivamente

3. **Breakpoints Responsivos:**
   - **< 768px:** Layout vertical (mobile)
   - **768px:** Cards em 2 colunas
   - **1024px:** Sidebar lateral, 2 colunas de cards
   - **1200px:** 3 colunas, sidebar reorganizada
   - **1600px:** 4 colunas de cards

4. **Grid dentro de Grid:**
   - Layout principal usa Grid
   - Cards também usam Grid
   - Demonstra a composição de layouts

5. **Técnicas Avançadas:**
   - Card destaque que muda de tamanho por breakpoint
   - Áreas nomeadas para facilitar reorganização
   - Combinação de `fr`, pixels fixos e `span`
   - Sidebar que muda de posição

6. **Boas Práticas:**
   - Código semântico (header, nav, main, aside, footer)
   - Transições suaves
   - Espaçamento consistente com `gap`
   - Hover effects nos cards

### Como Testar

1. Copie o HTML para um arquivo `index.html`
2. Copie o CSS para um arquivo `style.css`
3. Abra o arquivo HTML no navegador
4. Redimensione a janela para ver a responsividade
5. Use o DevTools (F12) para testar diferentes dispositivos

---

## 🎯 Resumo e Próximos Passos

Você aprendeu:

✅ **O que é CSS Grid** e quando usá-lo  
✅ **Grid Container:** `display: grid`, `grid-template-columns`, `grid-template-rows`, `gap`  
✅ **Grid Items:** `grid-column`, `grid-row`, `grid-area`  
✅ **Responsividade:** Media queries e layouts adaptativos  
✅ **Exemplo completo:** Site responsivo do zero

### Recursos para Praticar

- 🎮 [CSS Grid Garden](https://cssgridgarden.com/) - Jogo para aprender Grid
- 📚 [MDN Web Docs - CSS Grid](https://developer.mozilla.org/pt-BR/docs/Web/CSS/CSS_Grid_Layout)
- 🎨 [Grid by Example](https://gridbyexample.com/) - Exemplos práticos
- 🔧 [CSS Grid Generator](https://cssgrid-generator.netlify.app/) - Ferramenta visual

### Desafios para Você

1. Criar um layout de galeria de fotos responsivo
2. Fazer um dashboard com widgets usando Grid
3. Criar um layout de e-commerce com produtos
4. Reproduzir layouts de sites famosos usando Grid

**Bons estudos! 🚀**
