# qa-desafio-tecnico
Desafio técnico para vaga de QA – análise, criação de cenários de teste e identificação de bugs em uma aplicação de cadastro de cursos

---

## 1. Análise inicial da aplicação

A aplicação analisada consiste em um sistema simples de cadastro e listagem de cursos.

O sistema permite ao usuário:

- Cadastrar novos cursos através de um formulário
- Definir informações como nome, descrição, instrutor, imagem, datas, número de vagas e tipo de curso
- Visualizar os cursos cadastrados em uma listagem
- Excluir cursos cadastrados

Durante a análise inicial da aplicação foi possível identificar que o sistema possui validações limitadas nos campos do formulário, o que permite a inserção de dados inconsistentes ou incompletos.

---

## 2. Decisões tomadas para criação dos testes

Para a elaboração dos testes foram considerados os principais fluxos da aplicação, com foco em validar:

- Fluxo principal de cadastro de curso
- Exibição correta dos cursos na listagem
- Validação de campos do formulário
- Comportamentos inesperados do sistema
- Cenários negativos

Os cenários foram criados buscando cobrir situações comuns de uso da aplicação, além de explorar possíveis falhas de validação que poderiam comprometer a integridade dos dados cadastrados.

Também foram considerados cenários envolvendo o comportamento condicional do formulário, como a exibição de campos específicos dependendo do tipo de curso selecionado (online ou presencial).

---

## 3. Raciocínio durante a análise

Durante a execução dos testes foi adotada uma abordagem exploratória, navegando pela aplicação e analisando o comportamento dos campos e fluxos disponíveis.

A partir dessa exploração inicial, foram definidos cenários de teste voltados principalmente para:

- validação de dados de entrada
- consistência das informações cadastradas
- comportamento do sistema diante de dados inválidos
- funcionamento das ações disponíveis na listagem de cursos

Foi possível identificar diversos comportamentos inesperados relacionados principalmente à ausência de validações no formulário de cadastro.

Alguns dos cenários de teste resultaram em falhas devido a esses problemas de validação, permitindo a identificação de bugs relevantes para a qualidade da aplicação.

---

## 4. Cenários e casos de teste

Os cenários e casos de teste criados para este desafio estão documentados na planilha abaixo:

Planilha de testes:  
https://docs.google.com/spreadsheets/d/1OPMn_Dt9R9u9pwp4sM1_c2LJmBzHhRn25ULPJgUt-e8/edit?usp=sharing

Os testes contemplam:

- Fluxo principal de cadastro de curso
- Validações de campos
- Cenários negativos
- Comportamentos inesperados
- Funcionamento da listagem de cursos

No total foram criados **16 casos de teste**, cobrindo os principais comportamentos da aplicação.

---

## 5. Evidências da execução dos testes

As evidências da execução dos testes e dos bugs identificados estão disponíveis no link abaixo:

Evidências:  
https://drive.google.com/drive/folders/1Gw95VlCORQyFWkepBjGUd7fYD5r9EAcu?usp=sharing

As evidências incluem gravações demonstrando os comportamentos observados durante os testes.

---

## 6. Bugs encontrados

### BUG 01 – Sistema permite cadastro de curso com todos os campos vazios

Severidade: Alta  
Prioridade: Alta  

Passos para reproduzir:

1. Acessar a tela de cadastro de curso  
2. Não preencher nenhum campo do formulário  
3. Clicar no botão **Cadastrar curso**

Resultado atual:

O sistema permite o cadastro do curso mesmo com todos os campos vazios e o curso aparece na listagem.

Resultado esperado:

O sistema deveria impedir o cadastro e exibir mensagens de validação informando que os campos obrigatórios devem ser preenchidos.

---

### BUG 02 – Campo número de vagas aceita valores negativos, decimais ou 0

Severidade: Alta  
Prioridade: Alta  

Passos para reproduzir:

1. Acessar a tela de cadastro de curso  
2. Preencher os campos do formulário  
3. Inserir no campo **Número de vagas** valores inválidos como números negativos, decimais ou 0 
4. Clicar em **Cadastrar curso**

Resultado atual:

O sistema aceita os valores informados e permite o cadastro do curso.

Resultado esperado:

O sistema deveria permitir apenas números inteiros positivos maiores que zero.

---

### BUG 03 – Sistema permite cadastro de curso com data de início posterior à data de fim

Severidade: Média  
Prioridade: Média  

Passos para reproduzir:

1. Acessar a tela de cadastro de curso  
2. Preencher os campos do formulário  
3. Informar uma data de início posterior à data de fim  
4. Clicar em **Cadastrar curso**

Resultado atual:

O sistema permite o cadastro do curso com datas inconsistentes.

Resultado esperado:

O sistema deveria validar que a data de início não pode ser posterior à data de fim.

---

### BUG 04 – Curso online pode ser cadastrado sem link de inscrição

Severidade: Média  
Prioridade: Média  

Passos para reproduzir:

1. Acessar a tela de cadastro de curso  
2. Selecionar o tipo de curso **Online**  
3. Não preencher o campo **Link de inscrição**  
4. Clicar em **Cadastrar curso**

Resultado atual:

O sistema permite cadastrar o curso sem informar o link de inscrição.

Resultado esperado:

O sistema deveria exigir o preenchimento do campo quando o curso for online.

---

### BUG05 – Curso presencial pode ser cadastrado sem endereço

Severidade: Média  
Prioridade: Média  

Passos para reproduzir:

1. Acessar a tela de cadastro de curso  
2. Selecionar o tipo de curso **Presencial**  
3. Não preencher o campo **Endereço**  
4. Clicar em **Cadastrar curso**

Resultado atual:

O sistema permite cadastrar o curso sem endereço.

Resultado esperado:

O sistema deveria exigir o preenchimento do endereço quando o curso for presencial.

---

### BUG06 – Botão “Excluir curso” não remove o curso da listagem

Severidade: Alta  
Prioridade: Alta  

Passos para reproduzir:

1. Cadastrar um curso  
2. Acessar a listagem de cursos  
3. Clicar em **Excluir curso**

Resultado atual:

O sistema exibe a mensagem de sucesso, porém o curso continua na listagem.

Resultado esperado:

O curso deveria ser removido da listagem após a exclusão.

---

### BUG07 – Sistema permite cadastro de cursos duplicados

Severidade: Baixa  
Prioridade: Baixa  

Passos para reproduzir:

1. Cadastrar um curso  
2. Cadastrar outro curso com as mesmas informações

Resultado atual:

O sistema permite múltiplos cursos idênticos.

Resultado esperado:

O sistema deveria impedir duplicidade ou alertar o usuário.

---

## Sugestões de melhoria

### Melhoria 01 – Padronização da exibição dos cursos na listagem

**Descrição**

Ao cadastrar cursos com diferentes tamanhos de texto (nome ou descrição), a listagem apresenta variações no tamanho dos elementos, deixando a interface visualmente desorganizada.

**Sugestão**

Aplicar limites de tamanho de texto ou padronizar o layout dos cards ou da listagem para manter consistência visual entre os cursos exibidos.

---

### Melhoria 02 – Definição de limites mínimos e máximos para campos de texto

**Descrição**

Atualmente os campos de texto (nome do curso, descrição e instrutor) não possuem limite mínimo ou máximo de caracteres.

**Sugestão**

Definir limites de tamanho para evitar textos excessivamente curtos ou longos que possam comprometer a experiência do usuário ou a exibição na interface.

---

### Melhoria 03 – Validação do formato da URL da imagem de capa

**Descrição**

O campo de URL da imagem aceita qualquer tipo de texto, mesmo que não seja um link válido.

**Sugestão**

Implementar validação de formato de URL para garantir que apenas links válidos sejam aceitos no campo de imagem.

---

### Melhoria 04 – Confirmação antes de excluir curso

**Descrição**

A ação de exclusão de curso ocorre diretamente ao clicar no botão de excluir.

**Sugestão**

Adicionar uma janela de confirmação antes da exclusão para evitar remoções acidentais de cursos.
