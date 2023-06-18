# C# Parte 5: Bibliotecas DLLs, documentação e usando o NuGet

Projeto de estudos _forkado_ faz parte do curso [C# Parte 5: Bibliotecas DLLs, documentação e usando o NuGet](https://cursos.alura.com.br/course/csharp-biblioteca-dll-documentacao-nuget) da plataforma [Alura](https://www.alura.com.br).


## Para saber mais: GAC

O compilador do C# faz uma cópia das DLLs usadas pelo seu programa no diretório destino de compilação. Mas, isto não acontece com todas as DLLs. O .NET Framework, por exemplo, não é replicado para o diretório destino.

Sabe-se que isto é resolvido pelo sistema operacional. Mas, como o sistema operacional Windows funciona para prover a DLL na versão correta para a aplicação?

O Windows possui um grande catálogo de bibliotecas chamado **GAC - Global Assembly Cache**. Além do .NET Framework, existem várias outras DLLs do sistema operacional e programas instalados em sua máquina no GAC.

É possível verificar o diretório do Windows onde estas bibliotecas são armazenadas e acessadas. Até a versão 3.5 do .NET Framework, o diretório usado é o `C:\WINDOWS\assembly`.

É possível contar os arquivos .DLL deste diretório com o comando do PowerShell abaixo:

```powershell
(gci -Path c:\Windows\assembly -file -r | ? Name -like *.dll ).Length
```

À partir da versão 4.0 do .NET Framework, os diretórios usados pelo Windows para guardar as DLLs nestas versões é o `C:\WINDOWS\Microsoft.NET\assembly`.

Mas, o que acontece se ocorre um conflito entre o nome de uma biblioteca existente no GAC e no diretório do executável? Em termos gerais, a ordem para buscar as DLLs é: primeiro o GAC, depois o diretório do executável.


## Para saber mais: e minhas bibliotecas?

O catálogo de pacotes **NuGet** tornou mais simples a recuperação de dependências dos nossos projetos. Nesta galeria existem apenas pacotes **públicos**!

É possível criar uma conta no NuGet e publicar pacotes lá, mas, são raros as bibliotecas desenvolvidas dentro de empresas que podem ser publicadas.

Então, com as DLLs internas ainda há dependência das referências aos arquivos em diretórios específicos?

É possível hospedar um servidor próprio NuGet internamente na empresa. A Microsoft disponibilizou uma [documentação para isto](https://learn.microsoft.com/pt-br/nuget/hosting-packages/nuget-server).

Após configurar um NuGet interno na empresa, basta configurar o Visual Studio para buscar pacotes neste novo servidor, através do menu `Ferramentas > Gerenciador de pacotes NuGet > Configurações de Gerenciador de Pacotes` e alterando o item `Fonte de pacotes` (_Package Sources_) com o endereço do novo serviço.