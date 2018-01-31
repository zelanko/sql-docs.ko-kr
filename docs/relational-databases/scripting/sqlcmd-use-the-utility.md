---
title: "sqlcmd 유틸리티 사용 | Microsoft 문서"
ms.custom: 
ms.date: 06/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- Transact-SQL statements, executing
- command prompt utilities [SQL Server], sqlcmd
- statements [SQL Server], executing
- sqlcmd utility, about sqlcmd utility
ms.assetid: 3ec89119-7314-43ef-9e91-12e72bb63d62
caps.latest.revision: 
author: mightypen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: ea2018f4b9b0ad9c0ef29dbacaeaa6e7639a1a34
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="sqlcmd---use-the-utility"></a>sqlcmd - 유틸리티 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] **sqlcmd** 유틸리티는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 및 스크립트의 임시 대화형 실행과 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립팅 태스크의 자동화를 위한 명령줄 유틸리티입니다. **sqlcmd** 를 대화형으로 사용하거나 **sqlcmd**를 사용하여 실행할 스크립트 파일을 작성하려면 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 이해해야 합니다. 일반적으로 **sqlcmd** 유틸리티는 다음과 같은 방법으로 사용됩니다.  
  
-   사용자는 명령 프롬프트에서와 비슷한 방법으로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 입력합니다. 결과는 명령 프롬프트에 표시됩니다. 명령 프롬프트 창을 열려면 Windows 검색 상자에 “cmd”를 입력하고 **명령 프롬프트**를 클릭하여 엽니다. 명령 프롬프트에서 **sqlcmd** 를 입력한 뒤 원하는 옵션을 입력합니다. **sqlcmd**에서 지원하는 옵션의 전체 목록은 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)를 참조하세요.  
  
-   실행할 단일 **문을 지정하거나 실행할** 문이 포함된 텍스트 파일을 유틸리티에 알려 [!INCLUDE[tsql](../../includes/tsql-md.md)] sqlcmd [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업을 제출합니다. 출력은 일반적으로 텍스트 파일로 전송되지만 명령 프롬프트에 표시될 수도 있습니다.  
  
-   [쿼리 편집기의](../../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md) SQLCMD 모드 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   SMO(SQL Server 관리 개체)  
  
-   SQL Server 에이전트 CmdExec 작업  
  
## <a name="typically-used-sqlcmd-options"></a>일반적으로 사용되는 sqlcmd 옵션  
  
-   서버 옵션(**-S**): **sqlcmd**가 연결하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스를 식별합니다.  
  
-   인증 옵션(**-E**, **-U** 및 **-P**): **sqlcmd**가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하기 위해 사용하는 자격 증명을 지정합니다. **참고:** **-E** 옵션은 기본값이므로 지정하지 않아도 됩니다.  
  
-   입력 옵션(**-Q**, **-q** 및 **-i**): **sqlcmd**에 입력될 내용의 위치를 식별합니다.  
  
-   출력 옵션(**-o**): **sqlcmd**가 출력 내용을 저장할 파일을 지정합니다.  
  
## <a name="connect-to-the-sqlcmd-utility"></a>sqlcmd 유틸리티에 연결  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 대화형으로 실행하기 위해 Windows 인증을 사용하여 기본 인스턴스에 연결  
  
    ```  
    sqlcmd -S <ComputerName>  
    ```  
  
    > **참고:** 위 예에서 **-E** 는 기본값이므로 따로 지정하지 않았으며 **sqlcmd** 는 Windows 인증을 사용하여 기본 인스턴스에 연결합니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 대화형으로 실행하기 위해 Windows 인증을 사용하여 명명된 인스턴스에 연결  
  
    ```  
    sqlcmd -S <ComputerName>\<InstanceName>  
    ```  
  
     로 구분하거나 여러  
  
    ```  
    sqlcmd -S .\<InstanceName>  
    ```  
  
-   Windows 인증을 사용하고 입력 및 출력 파일을 지정하여 명명된 인스턴스에 연결  
  
    ```  
    sqlcmd -S <ComputerName>\<InstanceName> -i <MyScript.sql> -o <MyOutput.rpt>  
    ```  
  
-   Windows 인증을 사용하여 로컬 컴퓨터의 기본 인스턴스에 연결하고 쿼리를 실행한 다음 쿼리 실행이 완료된 후에도 **sqlcmd** 가 실행되는 상태로 유지  
  
    ```  
    sqlcmd -q "SELECT * FROM AdventureWorks2012.Person.Person"  
    ```  
  
-   Windows 인증을 사용하여 로컬 컴퓨터의 기본 인스턴스에 연결하고 쿼리를 실행한 다음 출력을 파일로 전송하고 쿼리 실행이 완료되면 **sqlcmd** 종료  
  
    ```  
    sqlcmd -Q "SELECT * FROM AdventureWorks2012.Person.Person" -o MyOutput.txt  
    ```  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문을 대화형으로 실행하기 위해 [!INCLUDE[tsql](../../includes/tsql-md.md)] 인증을 사용하여 명명된 인스턴스에 연결( **sqlcmd** 에서 암호를 묻는 메시지 표시)  
  
    ```  
    sqlcmd -U MyLogin -S <ComputerName>\<InstanceName>  
    ```  
  
    > **힌트** **sqlcmd** 유틸리티에서 지원하는 옵션 목록을 보려면 `sqlcmd -?`를 실행하세요.  
  
## <a name="run-transact-sql-statements-interactively-by-using-sqlcmd"></a>sqlcmd를 사용하여 대화형으로 Transact-SQL 문 실행  
 **sqlcmd** 유틸리티를 대화형으로 사용하여 명령 프롬프트 창에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] sqlcmd **를 사용하여**문을 대화형으로 실행하려면 입력 파일이나 쿼리를 지정하는 **-Q**, **-q**, **-Z**또는 **-i** 옵션을 사용하지 않고 유틸리티를 실행합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
 `sqlcmd -S <ComputerName>\<InstanceName>`  
  
 입력 파일이나 쿼리 없이 명령을 실행하면 **sqlcmd** 가 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하고 `1>` 과 그 뒤에 밑줄이 깜박이는 새 줄을 표시합니다. 이를 **sqlcmd** 프롬프트라고 합니다. `1` 은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 첫 번째 줄임을 의미하고 **sqlcmd** 프롬프트는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 입력할 때 문이 시작되는 지점입니다.  
  
 **sqlcmd** 프롬프트에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] GO **,** EXIT **등과 같이** 문과 **sqlcmd**명령을 모두 입력할 수 있습니다. 각 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 문 캐시를 호출한 버퍼에 저장됩니다. 이러한 문은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 명령을 입력하고 Enter 키를 누르면 **등과 같이** 로 전송됩니다. **sqlcmd**를 종료하려면 새 줄의 시작 부분에 **EXIT** 또는 **QUIT** 를 입력합니다.  
  
 문 캐시를 지우려면 **:RESET**을 입력합니다. **^C** 을(를) 입력하면 **sqlcmd** 가 종료됩니다. **^C** 는 **GO** 명령을 실행한 후 문 캐시의 실행을 중지하는 데 사용할 수도 있습니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 **:ED** 명령과 **sqlcmd** 프롬프트라고 합니다. 그렇게 하면 편집기가 열리며 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 편집한 후 편집기를 닫으면 수정된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 명령 창에 나타납니다. **문을 실행하려면** GO [!INCLUDE[tsql](../../includes/tsql-md.md)] 를 입력합니다.  
  
## <a name="quoted-strings"></a>따옴표 붙은 문자열  
 따옴표 두 개를 연속으로 입력하여 문자열 내에 따옴표를 삽입하는 예외적인 경우를 제외하고 따옴표로 묶인 문자는 추가적인 전처리 없이 사용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 이러한 문자 시퀀스를 하나의 따옴표로 처리합니다. 변환은 서버에서 발생합니다. 스크립팅 변수 역시 문자열 내에서는 단순한 문자로 처리됩니다.  
  
 예를 들어 다음과 같이 사용할 수 있습니다.  
  
 `sqlcmd`  
  
 `PRINT "Length: 5"" 7'";`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Length: 5" 7'`  
  
## <a name="strings-that-span-multiple-lines"></a>여러 줄로 구성된 문자열  
 **sqlcmd** 는 스크립트에서 문자열을 여러 줄로 나누어 입력할 수 있도록 지원합니다. 예를 들어 다음 `SELECT` 문은 여러 줄로 나누어져 있으나 `GO`를 입력한 후 Enter 키를 누르면 단일 문자열로 실행됩니다.  
  
 `SELECT First line`  
  
 `FROM Second line`  
  
 `WHERE Third line;`  
  
 `GO`  
  
## <a name="interactive-sqlcmd-example"></a>대화형 sqlcmd 실행 예  
 다음은 **sqlcmd** 를 대화형으로 실행할 때 나타나는 내용의 예입니다.  
  
 명령 프롬프트 창을 열면 다음과 비슷한 줄 하나가 나타납니다.  
  
 `C:\> _`  
  
 이는 `C:\` 폴더가 현재 폴더이며 파일 이름을 지정하면 Windows가 해당 폴더에서 파일을 찾을 것이라는 의미입니다.  
  
 **sqlcmd** 를 입력하여 로컬 컴퓨터의 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하면 명령 프롬프트 창에 다음과 같은 내용이 나타납니다.  
  
 `C:\>sqlcmd`  
  
 `1> _`  
  
 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결되어 이제 `sqlcmd` 에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문과 `sqlcmd` 명령을 입력해도 된다는 의미입니다. `1>` 다음의 깜박이는 밑줄은 입력하는 문과 명령이 표시될 위치를 나타내는 `sqlcmd` 프롬프트입니다. 이제 **USE AdventureWorks2012** 를 입력하고 Enter 키를 누릅니다. 그런 다음 **GO** 를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에 다음과 같은 내용이 나타납니다.  
  
 `sqlcmd`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Changed database context to 'AdventureWorks2012'.`  
  
 `1> _`  
  
 `USE AdventureWorks2012` 를 입력한 다음 Enter 키를 누르면 `sqlcmd` 가 새 줄을 시작합니다. `GO,` 를 입력한 다음 Enter 키를 누르면 `sqlcmd` 가 `USE AdventureWorks2012` 문을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 보냅니다. `sqlcmd` 는 `USE` 문이 성공적으로 완료되었음을 나타내는 메시지를 반환하고 새 `1>` 프롬프트를 표시하여 새 문이나 명령을 입력하도록 합니다.  
  
 다음 예에서는 `SELECT` 문, `GO` 를 실행할 `SELECT`및 `EXIT` 를 종료할 `sqlcmd`를 입력할 경우 명령 프롬프트 창에 나타나는 내용을 보여 줍니다.  
  
 `sqlcmd`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `SELECT TOP (3) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `BusinessEntityID   FirstName                 LastName`  
  
 `----------- -------------------------------- -----------`  
  
 `1           Syed                             Abbas`  
  
 `2           Catherine                        Abel`  
  
 `3           Kim                              Abercrombie`  
  
 `(3 rows affected)`  
  
 `1> EXIT`  
  
 `C:\>`  
  
 `3> GO` 줄 다음에 표시된 줄은 `SELECT` 문의 출력입니다. 출력이 생성된 후 `sqlcmd` 는 `sqlcmd` 프롬프트를 다시 설정하고 `1>`을 표시합니다. `EXIT` 줄에 `1>`를 입력하면 명령 프롬프트 창을 처음 열었을 때와 동일한 줄이 표시됩니다. 이는 `sqlcmd` 가 해당 세션을 종료했음을 나타냅니다. 이제 다시 `EXIT` 명령을 입력하여 명령 프롬프트 창을 닫을 수 있습니다.  
  
## <a name="running-transact-sql-script-files-using-sqlcmd"></a>sqlcmd를 사용하여 Transact-SQL 스크립트 파일 실행  
 **sqlcmd** 를 사용하여 데이터베이스 스크립트 파일을 실행할 수 있습니다. 스크립트 파일은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, **sqlcmd** 명령 및 스크립팅 변수를 포함하는 텍스트 파일입니다. 변수를 스크립팅하는 방법은 [스크립팅 변수와 함께 sqlcmd 사용](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)을 참조하세요. **sqlcmd** 는 대화형으로 입력된 문과 명령을 사용하는 방식과 유사한 방식으로 스크립트 파일의 문, 명령 및 스크립팅 변수를 사용합니다. 주된 차이점은 **sqlcmd** 가 사용자의 문, 명령 및 스크립팅 변수 입력 작업을 기다리지 않고 일시 중지 없이 입력 파일을 읽는다는 점입니다.  
  
 다음과 같이 데이터베이스 스크립트 파일을 만드는 다른 방법도 있습니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]문 집합을 대화형으로 작성하고 디버그한 다음 쿼리 창의 내용을 스크립트 파일로 저장할 수 있습니다.  
  
-   메모장과 같은 텍스트 편집기를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 포함하는 텍스트 파일을 만들 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-running-a-script-by-using-sqlcmd"></a>1. sqlcmd를 사용하여 스크립트 실행  
 메모장을 시작하고 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 입력합니다.  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 `SELECT TOP (3) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 `MyFolder` 라는 폴더를 만든 다음 스크립트를 `MyScript.sql` 폴더에 `C:\MyFolder`파일로 저장합니다. 명령 프롬프트에 다음을 입력하여 스크립트를 실행하고 출력을 `MyOutput.txt` 의 `MyFolder`에 저장합니다.  
  
 `sqlcmd -i C:\MyFolder\MyScript.sql -o C:\MyFolder\MyOutput.txt`  
  
 메모장에서 `MyOutput.txt` 의 내용을 보면 다음이 나타납니다.  
  
 `Changed database context to 'AdventureWorks2012'.`  
  
 `BusinessEntityID FirstName   LastName`  
  
 `---------------- ----------- -----------`  
  
 `1                Syed        Abbas`  
  
 `2                Catherine   Abel`  
  
 `3                Kim         Abercrombie`  
  
 `(3 rows affected)`  
  
### <a name="b-using-sqlcmd-with-a-dedicated-administrative-connection"></a>2. 전용 관리 연결에 sqlcmd 사용  
 다음 예에서 `sqlcmd` 는 DAC(관리자 전용 연결)를 사용하여 차단 문제가 발생한 서버에 연결하는 데 사용됩니다.  
  
 `C:\>sqlcmd -S ServerName -A`  
  
 `1> SELECT blocked FROM sys.dm_exec_requests WHERE blocked <> 0;`  
  
 `2> GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `spid   blocked`  
  
 `------ -------`  
  
 `62       64`  
  
 `(1 rows affected)`  
  
 `sqlcmd` 를 사용하여 차단 프로세스를 끝냅니다.  
  
 `1> KILL 64;`  
  
 `2> GO`  
  
### <a name="c-using-sqlcmd-to-execute-a-stored-procedure"></a>3. sqlcmd를 사용하여 저장 프로시저 실행  
 다음 예에서는 `sqlcmd`를 사용하여 저장 프로시저를 실행하는 방법을 보여 줍니다. 다음 저장 프로시저를 만듭니다.  
  
 `USE AdventureWorks2012;`  
  
 `IF OBJECT_ID ( ' dbo.ContactEmailAddress, 'P' ) IS NOT NULL`  
  
 `DROP PROCEDURE dbo.ContactEmailAddress;`  
  
 `GO`  
  
 `CREATE PROCEDURE dbo.ContactEmailAddress`  
  
 `(`  
  
 `@FirstName nvarchar(50)`  
  
 `,@LastName nvarchar(50)`  
  
 `)`  
  
 `AS`  
  
 `SET NOCOUNT ON`  
  
 `SELECT EmailAddress`  
  
 `FROM Person.Person`  
  
 `WHERE FirstName = @FirstName`  
  
 `AND LastName = @LastName;`  
  
 `SET NOCOUNT OFF`  
  
 `sqlcmd` 프롬프트에서 다음을 입력합니다.  
  
 `C:\sqlcmd`  
  
 `1> :Setvar FirstName Gustavo`  
  
 `1> :Setvar LastName Achong`  
  
 `1> EXEC dbo.ContactEmailAddress $(Gustavo),$(Achong)`  
  
 `2> GO`  
  
 `EmailAddress`  
  
 `-----------------------------`  
  
 `gustavo0@adventure-works.com`  
  
### <a name="d-using-sqlcmd-for-database-maintenance"></a>4. 데이터베이스 유지 관리에 sqlcmd 사용  
 다음 예에서는 데이터베이스 유지 관리 태스크에 `sqlcmd` 를 사용하는 방법을 보여 줍니다. 다음 코드로 `C:\BackupTemplate.sql` 을 만듭니다.  
  
 `USE master;`  
  
 `BACKUP DATABASE [$(db)] TO DISK='$(bakfile)';`  
  
 `sqlcmd` 프롬프트에서 다음을 입력합니다.  
  
 `C:\ >sqlcmd`  
  
 `1> :connect <server>`  
  
 `Sqlcmd: Successfully connected to server <server>.`  
  
 `1> :setvar db msdb`  
  
 `1> :setvar bakfile c:\msdb.bak`  
  
 `1> :r c:\BackupTemplate.sql`  
  
 `2> GO`  
  
 `Changed database context to 'master'.`  
  
 `Processed 688 pages for database 'msdb', file 'MSDBData' on file 2.`  
  
 `Processed 5 pages for database 'msdb', file 'MSDBLog' on file 2.`  
  
 `BACKUP DATABASE successfully processed 693 pages in 0.725 seconds (7.830 MB/sec)`  
  
### <a name="e-using-sqlcmd-to-execute-code-on-multiple-instances"></a>5. sqlcmd를 사용하여 여러 인스턴스의 코드 실행  
 단일 파일에 있는 다음 코드는 두 개의 인스턴스에 연결하는 스크립트를 보여 줍니다. 두 번째 인스턴스에 대한 연결 전에 `GO` 가 있습니다.  
  
 `:CONNECT <server>\,<instance1>`  
  
 `EXEC dbo.SomeProcedure`  
  
 `GO`  
  
 `:CONNECT <server>\,<instance2>`  
  
 `EXEC dbo.SomeProcedure`  
  
 `GO`  
  
### <a name="e-returning-xml-output"></a>5. XML 출력 반환  
 다음 예에서는 XML 출력이 서식이 지정되지 않은 연속 스트림으로 반환되는 방법을 보여 줍니다.  
  
 `C:\>sqlcmd -d AdventureWorks2012`  
  
 `1> :XML ON`  
  
 `1> SELECT TOP 3 FirstName + ' ' + LastName + ', '`  
  
 `2> FROM Person.Person`  
  
 `3> GO`  
  
 `Syed Abbas, Catherine Abel, Kim Abercrombie,`  
  
### <a name="f-using-sqlcmd-in-a-windows-script-file"></a>6. Windows 스크립트 파일에서 sqlcmd 사용  
 **sqlcmd**명령(예: `sqlcmd -i C:\InputFile.txt -o C:\OutputFile.txt,` )은 VBScript와 함께 .bat 파일에서 실행될 수 있습니다. 이 경우 대화형 옵션은 사용하지 마십시오. **sqlcmd** 는 .bat 파일을 실행하는 컴퓨터에 설치되어야 합니다.  
  
 첫 번째 단계로 다음과 같은 4개의 파일을 만듭니다.  
  
-   C:\badscript.sql  
  
    ```  
    SELECT batch_1_this_is_an_error  
    GO  
    SELECT 'batch #2'  
    GO  
    ```  
  
-   C:\goodscript.sql  
  
    ```  
    SELECT 'batch #1'  
    GO  
    SELECT 'batch #2'  
    GO  
    ```  
  
-   C:\returnvalue.sql  
  
    ```  
    :exit(select 100)  
    @echo off  
    C:\windowsscript.bat  
    @echo off  
  
    echo Running badscript.sql  
    sqlcmd -i badscript.sql -b -o out.log  
    if not errorlevel 1 goto next1  
    echo == An error occurred   
  
    :next1  
  
    echo Running goodscript.sql  
    sqlcmd -i goodscript.sql -b -o out.log  
    if not errorlevel 1 goto next2  
    echo == An error occurred   
  
    :next2  
    echo Running returnvalue.sql  
    sqlcmd -i returnvalue.sql -o out.log  
    echo SQLCMD returned %errorlevel% to the command shell  
  
    :exit  
    ```  
  
-   C:\windowsscript.bat  
  
    ```  
    @echo off  
  
    echo Running badscript.sql  
    sqlcmd -i badscript.sql -b -o out.log  
    if not errorlevel 1 goto next1  
    echo == An error occurred   
  
    :next1  
  
    echo Running goodscript.sql  
    sqlcmd -i goodscript.sql -b -o out.log  
    if not errorlevel 1 goto next2  
    echo == An error occurred   
  
    :next2  
    echo Running returnvalue.sql  
    sqlcmd -i returnvalue.sql -o out.log  
    echo SQLCMD returned %errorlevel% to the command shell  
  
    :exit  
    ```  
  
 그런 다음 명령 프롬프트에서 `C:\windowsscript.bat`를 실행합니다.  
  
 `C:\>windowsscript.bat`  
  
 `Running badscript.sql`  
  
 `== An error occurred`  
  
 `Running goodscript.sql`  
  
 `Running returnvalue.sql`  
  
 `SQLCMD returned 100 to the command shell`  
  
### <a name="g-using-sqlcmd-to-set-encryption-on-windows-azure-sql-database"></a>7. sqlcmd를 사용하여 Windows Azure SQL 데이터베이스에 암호화 설정  
 **sqlcmd**는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 데이터에 대한 연결에서 암호화 및 인증서 신뢰를 지정하기 위해 실행할 수 있습니다. 2가지 **sqlcmd**``옵션을 사용할 수 있습니다.  
  
-   -N 스위치는 클라이언트에서 암호화된 연결을 요청하는 데 사용됩니다. 이 옵션은 ADO.net 옵션 `ENCRYPT = true`와 동일합니다.  
  
-   –C 스위치는 클라이언트에서 유효성 검사 없이 암시적으로 서버 인증서를 신뢰하도록 구성하는 데 사용됩니다. 이 옵션은 ADO.net 옵션 `TRUSTSERVERCERTIFICATE = true`와 동일합니다.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 서비스는 SQL Server 인스턴스에서 사용 가능한 `SET` 옵션 중 일부는 지원하지 않습니다. 다음 옵션은 해당하는 `SET` 옵션이 `ON` 또는 `OFF`로 설정되어 있는 경우 오류를 반환합니다.  
  
-   SET ANSI_DEFAULTS  
  
-   SET ANSI_NULLS  
  
-   SET REMOTE_PROC_TRANSACTIONS  
  
-   SET ANSI_NULL_DEFAULT  
  
 다음 SET 옵션은 예외를 반환하지 않지만 사용할 수 없습니다. 이러한 옵션은 더 이상 사용되지 않습니다.  
  
-   SET CONCAT_NULL_YIELDS_NULL  
  
-   SET ANSI_PADDING  
  
-   SET QUERY_GOVERNOR_COST_LIMIT  
  
#### <a name="syntax"></a>구문  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 공급자 설정에 포함된 사례를 참조합니다. `ForceProtocolEncryption = False`, `Trust Server Certificate = No`  
  
 Windows 자격 증명을 사용한 연결 및 통신 암호화:  
  
```  
SQLCMD –E –N  
  
```  
  
 Windows 자격 증명을 사용한 연결 및 서버 인증서 신뢰:  
  
```  
SQLCMD –E –C  
  
```  
  
 Windows 자격 증명을 사용한 연결, 통신 암호화 및 서버 인증서 신뢰:  
  
```  
SQLCMD –E –N –C  
  
```  
  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 공급자 설정에 포함된 사례를 참조합니다. `ForceProtocolEncryption = True`, `TrustServerCertificate = Yes`  
  
 Windows 자격 증명을 사용한 연결, 통신 암호화 및 서버 인증서 신뢰:  
  
```  
SQLCMD –E  
  
```  
  
 Windows 자격 증명을 사용한 연결, 통신 암호화 및 서버 인증서 신뢰:  
  
```  
SQLCMD –E –N  
  
```  
  
 Windows 자격 증명을 사용한 연결, 통신 암호화 및 서버 인증서 신뢰:  
  
```  
SQLCMD –E –T  
  
```  
  
 Windows 자격 증명을 사용한 연결, 통신 암호화 및 서버 인증서 신뢰:  
  
```  
SQLCMD –E –N –C  
  
```  
  
 공급자가 `ForceProtocolEncryption = True` 를 지정하는 경우 연결 문자열에 `Encrypt=No` 가 있어도 암호화가 설정됩니다.  
  
## <a name="more-about-sqlcmd"></a>sqlcmd에 대한 자세한 정보  
 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)   
 [스크립팅 변수와 함께 sqlcmd 사용](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)   
 [쿼리 편집기로 SQLCMD 스크립트 편집](../../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)   
 [작업 단계 관리](http://msdn.microsoft.com/library/51352afc-a0a4-428b-8985-f9e58bb57c31)   
 [CmdExec 작업 단계 만들기](http://msdn.microsoft.com/library/b48da5b4-6fe7-4eb7-bade-dc7d697c6d5c)  
  
  
