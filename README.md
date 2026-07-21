# 🚀 Miniguia de Estudos: Animações Interativas com GSAP e ScrollTrigger

![Capa do Projeto](img/Gemini_Generated_Image_q6x96sq6x96sq6x9.png)

> **Projeto Prático - Bootcamp DIO**  
> Repositório criado para o desafio de projeto da DIO, explorando o uso da Inteligência Artificial (NotebookLM) como ferramenta de aprendizagem ativa, curadoria e organização de conhecimento técnico focado em Front-end.

---

## 📌 Contexto e Objetivos

O desenvolvimento web moderno, especialmente na criação de landing pages interativas (como o projeto temático da marca Fanta que estou desenvolvendo), exige interfaces dinâmicas e performáticas. A biblioteca **GSAP (GreenSock Animation Platform)** em conjunto com o plugin **ScrollTrigger** é o padrão da indústria para animações baseadas na rolagem do usuário.

### Objetivos de Estudo:
* **Compreender a mecânica do GSAP:** Entender o uso de Timelines e encadeamento de animações.
* **Dominar o ScrollTrigger:** Aprender a sincronizar animações com a rolagem da página, utilizando propriedades como `scrub` e `pin`.
* **Performance:** Estudar otimizações de layout e o uso de *transforms* para evitar gargalos de renderização (*Layout Thrashing*), garantindo animações a 60 FPS.

---

## 📚 Curadoria de Fontes

Para alimentar o caderno temático no **NotebookLM**, foram selecionadas 3 fontes abertas de alta relevância técnica que foram salvas em PDF para análise da IA:

| # | Fonte / Título | Origem | Justificativa de Escolha |
|---|---|---|---|
| 1 | **GSAP Getting Started Guide** | GreenSock Docs | Documentação oficial com os conceitos base e sintaxe moderna (v3). |
| 2 | **ScrollTrigger Docs** | GreenSock Docs | Mapeamento completo de propriedades de scroll interativo. |
| 3 | **Desempenho de Animações Web** | MDN Web Docs | Guia focado no Caminho de Renderização Crítico e uso de aceleração por hardware. |

---

## 🧠 Engenharia de Prompts e "Cicatrizes" (Troubleshooting)

Nesta seção estão documentadas as interações com o NotebookLM. O processo revelou que a IA pode ser uma ótima assistente, mas exige validação técnica e restrições de contexto.

### 🧪 Teste 1: A Grande Alucinação de Contexto (Confusão de Domínio)
* **Prompt Utilizado:** *"Gere um resumo do assunto e um glossário com os termos principais (como scrub, pin, timeline) com base nos PDFs fornecidos."*
* **O Problema (Cicatriz):** A IA sofreu de *Confusão de Domínio*. Ao ler palavras como "Timeline", "Scrub" e "Pin", o modelo ignorou as documentações do GSAP e gerou um glossário focado em softwares de edição de vídeo (citando Adobe Premiere, Puppet Pin do After Effects e reprodução manual de frames). 
* **A Solução:** Refinei o prompt aplicando restrições rígidas: *"Gere um glossário EXCLUSIVAMENTE focado em desenvolvimento web e código JavaScript, definindo os termos estritamente sob a ótica do plugin ScrollTrigger. É proibido mencionar softwares de edição de vídeo."*

### 🧪 Teste 2: Prática e Performance (A Armadilha do Pin)
* **Prompt Utilizado:** *"Estou construindo uma landing page interativa temática para a marca Fanta. (...) Uma lata de refrigerante deve descer a tela girando em 360 graus. Quando atingir o meio da tela (50%), ela deve ficar fixada no lugar (pin) enquanto o usuário continua rolando a página. A rotação deve estar amarrada ao scroll."*
* **O Acerto (Performance):** A IA justificou brilhantemente a substituição de atributos de layout (`top`/`left`) por *transforms* (`y`/`rotation`) citando a prevenção de recálculo de renderização (Layout Thrashing) baseado no artigo da MDN.
* **O Problema (Cicatriz):** A IA sugeriu usar `pin: true` diretamente no elemento da lata animada. Porém, ao testar na prática, o layout HTML quebrou. A IA falhou em alertar que a boa prática exige a criação de uma `div wrapper` (container) em volta do elemento para receber o pin sem destruir o espaçamento dos elementos irmãos.

---

## 📖 Miniguia de Estudo (Entrega Final)

### 1. Resumo Estruturado
* **GSAP Core:** A biblioteca manipula propriedades CSS numéricas através de JavaScript de forma altamente otimizada, sendo recomendada a manipulação de `transforms` (x, y, scale, rotation) e `opacity` para evitar sobrecarga no Caminho de Renderização Crítico.
* **Timelines:** Sequenciadores de animação (`gsap.timeline()`) que substituem a necessidade de calcular `delays` complexos, permitindo agrupar e controlar o fluxo de várias animações de forma coesa.
* **ScrollTrigger:** Plugin que vincula o progresso de uma animação ao deslocamento da barra de rolagem, permitindo ancoragem de elementos e depuração visual.

### 2. Glossário de Conceitos-Chave Corrigido (Foco em Código)

| Conceito | Descrição no Contexto Web |
|---|---|
| **`scrub`** | Propriedade do ScrollTrigger que amarra o tempo da animação diretamente à velocidade da barra de rolagem do usuário. |
| **`pin`** | Fixa (ancora) um elemento na tela durante um trecho específico do scroll. Requer atenção ao uso de wrappers para não quebrar o CSS ao redor. |
| **`Timeline`** | Instância JavaScript (`gsap.timeline()`) usada para encadear animações consecutivas ou sobrepostas sem precisar gerenciar atrasos manuais. |
| **`Layout Thrashing`** | Problema de desempenho grave ("Jank") causado pela animação de propriedades como `width`, `top` ou `margin`, que forçam o navegador a recalcular toda a geometria da página. |
| **`markers`** | Indicadores visuais (`markers: true`) inseridos na tela em ambiente de desenvolvimento para ajudar a depurar os pontos de início (`start`) e fim (`end`) do scroll. |

### 3. Biblioteca de Prompts Reutilizáveis

Para futuras revisões, utilize estes prompts no NotebookLM alimentado com a documentação do GSAP:

```text
PROMPT 1 (Revisão de Código Web):
"Analise o seguinte trecho de código GSAP/ScrollTrigger [INSERIR CÓDIGO]. Identifique possíveis problemas de performance que possam causar Layout Thrashing ou quebra de fluxo com o uso do 'pin'. Sugira a versão otimizada usando apenas transforms."

PROMPT 2 (Criação de Lógica):
"Com base na documentação oficial do GSAP v3, crie um guia passo a passo para animar uma seção onde 3 elementos aparecem em cascata (usando stagger) assim que a seção atinge 80% do viewport do usuário."

PROMPT 3 (Teste de Conhecimento):
"Gere um quiz técnico de 5 perguntas sobre ScrollTrigger (focado nas propriedades start, end, scrub e pin) com gabarito comentado, garantindo que o contexto seja 100% focado em desenvolvimento JavaScript."
