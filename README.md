# # IFSP Campus Cubatão — CBTEDD2
## Projeto 05 — Agenda de Contatos (Windows Forms Application)

Este projeto consiste na implementação da **Agenda de Contatos** com interface gráfica para Windows Forms em C#, desenvolvida para a disciplina de **Estrutura de Dados 2 (CBTEDD2)** do curso de **Tecnologia em Análise e Desenvolvimento de Sistemas** do Instituto Federal de Educação, Ciência e Tecnologia de São Paulo (IFSP — Campus Cubatão).

---

## Sumário
1. [Visão Geral](#visão-geral)
2. [Diagrama de Classes e Arquitetura](#diagrama-de-classes-e-arquitetura)
3. [Funcionalidades e Adaptação da Interface](#funcionalidades-e-adaptação-da-interface)
4. [Pré-requisitos e Como Executar](#pré-requisitos-e-como-executar)
5. [Estrutura do Código](#estrutura-do-código)

---

## Visão Geral

O objetivo da aplicação é gerenciar contatos pessoais através de uma interface desktop moderna e intuitiva. Cada contato possui:
- E-mail (identificador único)
- Nome completo
- Data de Nascimento (objeto da classe `Data`)
- Lista de Telefones (objetos da classe `Telefone`)

---

## Diagrama de Classes e Arquitetura

O sistema implementa rigorosamente a modelagem orientada a objetos solicitada no enunciado:

```
+--------------------------------------------+
| Data                                       |
+--------------------------------------------+
| - dia: int                                 |
| - mes: int                                 |
| - ano: int                                 |
+--------------------------------------------+
| + setData(int dia, int mes, int ano): void |
| + ToString(): String (override)            |
|    -> "dd/mm/aaaa"                         |
+--------------------------------------------+

+-------------------+
| Telefone          |
+-------------------+
| - tipo: string    |
| - numero: string  |
| - principal: bool |
+-------------------+

+------------------------------------------+
| Contato                                  |
+------------------------------------------+
| - email: string                          |
| - nome: string                           |
| - dtNasc: Data                           |
| - telefones: List<Telefone>              |
+------------------------------------------+
| + getIdade(): int                        |
| + adicionarTelefone(Telefone t): void    |
| + getTelefonePrincipal(): string         |
| + ToString(): String (override)          |
| + Equals(object obj): bool (override)    |
+------------------------------------------+

+------------------------------------+
| Contatos                           |
+------------------------------------+
| - agenda: List<Contato> (readOnly) |
+------------------------------------+
| + adicionar(Contato c): bool       |
| + pesquisar(Contato c): Contato    |
| + alterar(Contato c): bool         |
| + remover(Contato c): bool         |
+------------------------------------+
```

---

## Funcionalidades e Adaptação da Interface

A interface do seletor em modo texto foi adaptada para botões e componentes visuais do Windows Forms:

| Opção Original | Componente Windows Forms | Descrição / Comportamento |
| :--- | :--- | :--- |
| **1. Adicionar contato** | Botão `Adicionar Contato` | Cadastra um novo contato com e-mail, nome, data de nascimento e lista de telefones. Valida se o e-mail já existe. |
| **2. Pesquisar contato** | Botão `Pesquisar` / Campo de E-mail | Busca um contato pelo e-mail informado e preenche automaticamente todos os campos do formulário com os dados encontrados. |
| **3. Alterar contato** | Botão `Alterar Contato` | Atualiza os dados de nome, data de nascimento e telefones do contato correspondente ao e-mail informado. |
| **4. Remover contato** | Botão `Remover Contato` | Solicita confirmação visual e remove o contato pesquisado/selecionado da agenda. |
| **5. Listar contatos** | Botão `Listar Contatos` e `DataGridView` | Exibe todos os contatos cadastrados em uma tabela contendo E-mail, Nome, Data Nasc., Idade, Telefone Principal e Qtd. Telefones. |
| **0. Sair** | Botão `Sair` | Encerra com segurança a aplicação. |

---

## Pré-requisitos e Como Executar

### Opção 1: No Visual Studio (2019 / 2022)
1. Abra o **Visual Studio**.
2. Crie um novo projeto: **Aplicativo do Windows Forms (.NET Framework ou .NET 6+)** com linguagem **C#**.
3. Defina o nome do projeto como `ProjetoAgenda`.
4. Substitua o conteúdo do arquivo `Program.cs` pelo código fornecido neste repositório.
5. Pressione `F5` para compilar e executar a aplicação.

### Opção 2: Via Terminal / .NET CLI (.NET 6 / 7 / 8 / 9)
```bash
# 1. Criar projeto Windows Forms
dotnet new winforms -n ProjetoAgenda -o ProjetoAgenda

# 2. Entrar na pasta
cd ProjetoAgenda

# 3. Substituir o arquivo Program.cs pelo arquivo gerado
# ... copiar o arquivo Program.cs para a pasta ...

# 4. Executar o projeto
dotnet run
```

---

## Estrutura do Código

- `Data`: Representa datas com dia, mês e ano, validação de formato e formatação `"dd/mm/aaaa"`.
- `Telefone`: Modelo para cada número de telefone, tipo (Residencial, Celular, Trabalho, etc.) e sinalização do telefone principal.
- `Contato`: Modela a entidade de contato, calculando dinamicamente a idade (`getIdade()`), gerenciando o telefone principal e comparando igualdade por e-mail (`Equals()`).
- `Contatos`: Encapsula a coleção em memória (`List<Contato>`) oferecendo operações CRUD (Create, Read, Update, Delete).
- `MainForm`: Formulário construído via código (C# puramente programático) com suporte a cadastro de múltiplos telefones, listagem via `DataGridView` e seleção por duplo clique.
