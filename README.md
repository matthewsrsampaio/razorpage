C# .NET CRUD MVC RAZORPAGE

1 - Criar o projeto
	1.1 - ASP.NET Core Web App (Razor Pages)
	1.2 - Escolhe o framework desejado (Eu escolhi .net8)
	1.3 - Authentication type = individual accounts
	1.4 - [v] Configure HTTPS
	1.5 - Escolhe se vai querer docker ou não 

2 - Criar Modelos
	2.1 - Criar a pasta Models
	2.2 - Criar primeira Model
	2.3 - Para ter certeza de que as anotações estão funcionando importe sem as aspas duplas "using System.ComponentModel.DataAnnotations;"
	2.4 - Algumas anotações essenciais: 
		[Required], 
		[Key], 
		[DataType(DataType.DateTime)], 
		[DisplayName("Algum nome")], 
		[StringLength(10, ErrorMessage = "msg")], 
		[MinLength(2, ErrorMessage = "msg")], 
		[EmailAddress(ErrorMessage = "msg"))]

3 - Adicionar suporte ao Entity Framework com SQLite para persistir os dados
	3.1 Pelo Nuget Package Manager
				Tools 	
				-> NuGet Package Manager 
				-> Manage Nuget Packages for Solution 
				-> Download&Install(Microsoft.EntityFrameWorkCore.Sqlite)

	3.2 Pelo Terminal
		Comando: 
	dotnet add package Microsoft.EntityFrameworkCore.Sqlite

4 - Atualizar as referências no ApplicationDbContext para que as tabelas possam se geradas no banco.
	ex: public DbSet<NomeDaClasse> NomeDaClasse { get; set; } = default!;

5 - Criar uma migração para atualizar o banco
	5.1 - Instalar a ferramenta dotnet EntityFramework
	Comando: dotnet tool install --global dotnet-ef

	5.2 - Criar migração
	Comando: dotnet ef migrations add NomeDaMigração

	5.3 - Atualizar o banco
	Comando: dotnet ef database update

6 - Criar templates -> Scaffold
	6.1 - Instalar gerador de código
	Comando: dotnet tool install -g dotnet-aspnet-codegenerator

	6.2 - Instalar o gerador de códigos
		6.2.1  Terminal
		Comando: dotnet add package Microsoft.VirtualStudio.Web.CodeGenerator.Design

		6.2.2 Nuget Package Manager
		Tools 	
		-> NuGet Package Manager 
		-> Manage Nuget Packages for Solution 
		-> Download&Install(Microsoft.VirtualStudio.Web.CodeGenerator.Design)

7 - Criar as RazorPage (templates)
	7.1 - Com o seguinte código pode-se criar os templates de Create, List, Update, Delete e Details. Precisa apenas mudar o nome do template.

	7.2 - Comando para criar RazorPage
	Comando: dotnet aspnet-codegenerator razorpage Create Create -m Student -dc ApplicationDbContext -sqlite -udl -outDir Pages/Students
		
		7.2.1 - "dotnet aspnet-codegenerator razorpage"
		Cria o template razorpage

		7.2.2 Create Create
		O primeiro Create dá nome ao template e o segundo Create diz que tipo de template será criado. Nesse exemplo, criamos um template de Create.

		7.2.3 - "-m Student"
		Determina o Model que será usado. No nosso código "-m Student" usará o modelo Student.

		7.2.4 - "-dc ApplicationDbContext"
		Determina o DataContext. Nesse caso nosso DataContext chama-se ApplicationDbContext.

		7.2.5 - "-sqlite"
		Determina que o DataContext use o sqlite e não o padrão SqlServer. No meu caso, essa flag não funcionou pq já estava deprecated.

		7.2.6 - "-udl"
		Chama-se UseDefaultLayout.
		Determina que o codegenerator use o layout padrão na criação do template.

		7.2.7 - "-outDir Pages/Students"
		Determina o diretório em que a página será criada. Neste caso, Students que está dentro de Pages.

		7.2.8 - Agora é só criar:
		Editar: Edit Edit
		Deletar: Delete Delete
		Listar: Index List
		Detalhes: Details Details

8 - Observação quando for Listar
	8.1 - Pegando Student como exemplo. Quando formos listar não podemos esquecer de mudar no asp-page o "Students" e depois adicionar "/Index", ficando "Students/Index"
	Exemplo:
	<li class="nav-item">
    	<a class="nav-link text-dark" asp-area="" asp-page="Students/Index">Home</a>
	</li>






Vídeo Referência: https://www.youtube.com/watch?v=fmDYYsSXrKM&t=174s
