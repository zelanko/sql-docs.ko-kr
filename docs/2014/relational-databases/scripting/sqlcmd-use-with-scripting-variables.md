---
title: 스크립팅 변수와 함께 sqlcmd 사용 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- scripts [SQL Server], sqlcmd utility
- variables [SQL Server], scripts
- scripting variables [SQL Server]
- sqlcmd utility, scripts
- setvar command
ms.assetid: 793495ca-cfc9-498d-8276-c44a5d09a92c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b394e91c01e4607c74f73d90630095af2e912941
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090056"
---
# <a name="use-sqlcmd-with-scripting-variables"></a>스크립팅 변수와 함께 sqlcmd 사용
  스크립트에서 사용할 수 있는 변수를 스크립팅 변수라고 합니다. 스크립팅 변수를 사용하면 하나의 스크립트를 여러 시나리오에서 사용할 수 있습니다. 예를 들어 하나의 스크립트를 여러 서버에서 실행해야 하는 경우 각 서버에 맞게 스크립트를 수정하는 대신 서버 이름에 스크립팅 변수를 사용할 수 있습니다. 스크립팅 변수로 제공되는 서버 이름을 변경하여 같은 스크립트를 다른 서버에서 실행할 수 있습니다.  
  
 스크립팅 변수는 **setvar** 명령을 사용하여 명시적으로 정의하거나 **sqlcmd-v** 옵션을 사용하여 암시적으로 정의할 수 있습니다.  
  
 이 항목에는 **SET**를 사용하여 Cmd.exe 명령 프롬프트에서 환경 변수를 정의하는 예도 포함되어 있습니다.  
  
## <a name="setting-scripting-variables-by-using-the-setvar-command"></a>setvar 명령을 사용하여 스크립팅 변수 설정  
 **setvar** 명령은 스크립팅 변수를 정의하는 데 사용됩니다. **setvar** 명령을 사용하여 정의한 변수는 내부적으로 저장됩니다. **SET**를 사용하여 명령 프롬프트에서 정의하는 환경 변수와 스크립팅 변수를 혼동하면 안 됩니다. 스크립트에서 환경 변수가 아니거나 **setvar**을 사용하여 정의되지 않은 변수를 참조하면 오류 메시지가 반환되고 스크립트 실행이 중지됩니다. 자세한 내용은 **sqlcmd 유틸리티** 의 [-b](../../tools/sqlcmd-utility.md)옵션을 참조하세요.  
  
## <a name="variable-precedence-low-to-high"></a>변수 우선 순위(낮은 순위에서 높은 순위)  
 같은 이름의 변수 유형이 둘 이상인 경우 우선 순위가 가장 높은 변수가 사용됩니다.  
  
1.  시스템 수준 환경 변수  
  
2.  사용자 수준 환경 변수  
  
3.  **SET X=Y**를 시작하기 전에 명령 프롬프트에서 설정된 명령 셸( **SET X=Y**)  
  
4.  **sqlcmd-v** X=Y  
  
5.  **:Setvar** X Y  
  
> [!NOTE]  
>  환경 변수를 보려면 **제어판**에서 **시스템**을 연 다음 **고급** 탭을 클릭합니다.  
  
## <a name="implicitly-setting-scripting-variables"></a>암시적 스크립팅 변수 설정  
 관련 **sqlcmd** 변수가 있는 옵션을 사용하여 **sqlcmd** 를 시작하면 **sqlcmd** 변수는 옵션을 사용하여 지정한 값으로 암시적으로 설정됩니다. 다음 예에서는 `sqlcmd` 를 `-l` 옵션으로 시작합니다. 이 경우 암시적으로 SQLLOGINTIMEOUT 변수가 설정됩니다.  
  
 `c:\> sqlcmd -l 60`  
  
 **-v** 옵션을 사용하여 스크립트에 있는 스크립팅 변수를 설정할 수도 있습니다. 파일 이름이 `testscript.sql`인 다음 스크립트에서 `ColumnName` 이 스크립팅 변수입니다.  
  
 `USE AdventureWorks2012;`  
  
 `SELECT x.$(ColumnName)`  
  
 `FROM Person.Person x`  
  
 `WHERE c.`BusinessEntityID `< 5;`  
  
 다음과 같이 `-v` 옵션을 사용하여 반환하려는 열의 이름을 지정할 수 있습니다.  
  
 `sqlcmd -v ColumnName ="FirstName" -i c:\testscript.sql`  
  
 같은 스크립트를 사용하여 다른 열을 반환하려면 `ColumnName` 스크립팅 변수 값을 변경합니다.  
  
 `sqlcmd -v ColumnName ="LastName" -i c:\testscript.sql`  
  
## <a name="guidelines-for-scripting-variable-names-and-values"></a>스크립팅 변수 이름 및 값에 대한 지침  
 스크립팅 변수의 이름을 지정하는 경우 다음 지침을 고려합니다.  
  
-   변수 이름은 공백 문자나 따옴표를 포함할 수 없습니다.  
  
-   변수 이름은 *$(var)* 와 같은 변수 식 형태가 될 수 없습니다.  
  
-   스크립팅 변수는 대/소문자를 구분하지 않습니다.  
  
    > [!NOTE]  
    >  **sqlcmd** 환경 변수에 값을 지정하지 않으면 변수가 제거됩니다. 값이 없는 **:setvar VarName** 을 사용하면 변수가 지워집니다.  
  
 스크립팅 변수의 값을 지정하는 경우 다음 지침을 고려합니다.  
  
-   문자열 값에 공백이 포함된 경우 **setvar** 또는 **-v** 옵션을 사용하여 정의한 변수 값을 따옴표로 묶어야 합니다.  
  
-   변수 값에 따옴표가 포함되는 경우 따옴표를 이스케이프 처리해야 합니다. 예를 들면 :`setvar MyVar "spac""e"`와 같습니다.  
  
## <a name="guidelines-for-cmdexe-set-variable-values-and-names"></a>Cmd.exe SET 변수 값 및 이름에 대한 지침  
 SET를 사용하여 정의한 변수는 Cmd.exe 환경의 일부이며 **sqlcmd**에서 참조될 수 있습니다. 다음 지침을 살펴 보십시오.  
  
-   변수 이름은 공백 문자나 따옴표를 포함할 수 없습니다.  
  
-   변수 값은 공백이나 따옴표를 포함할 수 있습니다.  
  
## <a name="sqlcmd-scripting-variables"></a>sqlcmd 스크립팅 변수  
 **sqlcmd** 에서 정의하는 변수를 스크립팅 변수라고 합니다. 다음 표에는 **sqlcmd** 스크립팅 변수가 나와 있습니다.  
  
|변수|관련 옵션|R/W|기본값|  
|--------------|--------------------|----------|-------------|  
|SQLCMDUSER*|-U|R|""|  
|SQLCMDPASSWORD*|-P|--|""|  
|SQLCMDSERVER*|-S|R|"DefaultLocalInstance"|  
|SQLCMDWORKSTATION|-H|R|"ComputerName"|  
|SQLCMDDBNAME|-d|R|""|  
|SQLCMDLOGINTIMEOUT|-l|R/W|"8"(초)|  
|SQLCMDSTATTIMEOUT|-t|R/W|"0" = 무기한 대기|  
|SQLCMDHEADERS|-H|R/W|"0"|  
|SQLCMDCOLSEP|-S|R/W|" "|  
|SQLCMDCOLWIDTH|-w|R/W|"0"|  
|SQLCMDPACKETSIZE|-A|R|"4096"|  
|SQLCMDERRORLEVEL|-M|R/W|"0"|  
|SQLCMDMAXVARTYPEWIDTH|-y|R/W|"256"|  
|SQLCMDMAXFIXEDTYPEWIDTH|-y|R/W|"0" = 제한 없음|  
|SQLCMDEDITOR||R/W|"edit.com"|  
|SQLCMDINI||R|""|  
  
 \* SQLCMDUSER, SQLCMDPASSWORD 및 SQLCMDSERVER는 **:Connect** 가 사용될 때 설정됩니다.  
  
 R은 값이 프로그램 초기화 시 한 번만 설정될 수 있음을 나타냅니다.  
  
 R/W는 **setvar** 명령을 사용하여 값을 다시 설정할 수 있으며 후속 명령에 새 값이 사용됨을 나타냅니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-the-setvar-command-in-a-script"></a>1. 스크립트에서 setvar 명령 사용  
 **setvar** 명령을 사용하면 스크립트에서 여러 **sqlcmd** 옵션을 제어할 수 있습니다. 다음 예에서는 `test.sql` 변수가 `SQLCMDLOGINTIMEOUT` 초로 설정되고 다른 스크립팅 변수인 `60` 가 `server`로 설정된 `testserver`스크립트를 만듭니다. `test.sql`의 코드는 다음과 같습니다.  
  
 `:setvar SQLCMDLOGINTIMEOUT 60`  
  
 `:setvar server "testserver"`  
  
 `:connect $(server) -l $(SQLCMDLOGINTIMEOUT)`  
  
 `USE AdventureWorks2012;`  
  
 `SELECT FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `The script is then called by using sqlcmd:`  
  
 `sqlcmd -i c:\test.sql`  
  
### <a name="b-using-the-setvar-command-interactively"></a>2. 대화식으로 setvar 명령 사용  
 다음 예에서는 `setvar` 명령을 사용하여 대화식으로 스크립팅 변수를 설정하는 방법을 보여 줍니다.  
  
 `sqlcmd`  
  
 `:setvar  MYDATABASE AdventureWorks2012`  
  
 `USE $(MYDATABASE);`  
  
 `GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Changed database context to 'AdventureWorks2012'`  
  
 `1>`  
  
### <a name="c-using-command-prompt-environment-variables-within-sqlcmd"></a>3. sqlcmd 내에서 명령 프롬프트 환경 변수 사용  
 다음 예에서는 환경 변수 4개를 `are` 다음 `sqlcmd`에서 호출합니다.  
  
 `C:\>SET tablename=Person.Person`  
  
 `C:\>SET col1=FirstName`  
  
 `C:\>SET col2=LastName`  
  
 `C:\>SET title=Ms.`  
  
 `C:\>sqlcmd -d AdventureWorks2012`  
  
 `1> SELECT TOP 5 $(col1) + ' ' + $(col2) AS Name`  
  
 `2> FROM $(tablename)`  
  
 `3> WHERE Title ='$(title)'`  
  
 `4> GO`  
  
### <a name="d-using-user-level-environment-variables-within-sqlcmd"></a>4. sqlcmd 내에서 사용자 수준 환경 변수 사용  
 다음 예에서는 명령 프롬프트에서 사용자 수준 환경 변수인 `%Temp%` 를 설정하고 `sqlcmd` 입력 파일로 전달합니다. 사용자 수준 환경 변수를 얻으려면 **제어판**에서 **시스템**을 두 번 클릭하고 **고급** 탭을 클릭한 다음 **환경 변수**를 클릭합니다.  
  
 입력 파일 `c:\testscript.txt`의 코드는 다음과 같습니다.  
  
 `:OUT $(MyTempDirectory)`  
  
 `USE AdventureWorks2012;`  
  
 `SELECT FirstName`  
  
 `FROM AdventureWorks2012.Person.Person`  
  
 `WHERE BusinessEntityID` `< 5;`  
  
 명령 프롬프트에서 입력되는 코드는 다음과 같습니다.  
  
 `C:\ >SET MyTempDirectory=%Temp%\output.txt`  
  
 `C:\ >sqlcmd -i C:\testscript.txt`  
  
 출력 파일 C:\Documents and Settings\\<user\>\Local Settings\Temp\output.txt로 보내지는 결과는 다음과 같습니다.  
  
 `Changed database context to 'AdventureWorks2012'.`  
  
 `FirstName`  
  
 `--------------------------------------------------`  
  
 `Gustavo`  
  
 `Catherine`  
  
 `Kim`  
  
 `Humberto`  
  
 `(4 rows affected)`  
  
### <a name="e-using-a-startup-script"></a>5. 시작 스크립트 사용  
 **sqlcmd** 시작 스크립트는 **sqlcmd** 가 시작될 때 실행됩니다. 다음 예에서는 `SQLCMDINI`환경 변수를 설정합니다. 다음은 `init.sql.`  
  
 `SET NOCOUNT ON`  
  
 `GO`  
  
 `DECLARE @nt_username nvarchar(128)`  
  
 `SET @nt_username = (SELECT rtrim(convert(nvarchar(128), nt_username))`  
  
 `FROM sys.dm_exec_sessions WHERE spid = @@SPID)`  
  
 `SELECT  @nt_username + ' is connected to ' +`  
  
 `rtrim(CONVERT(nvarchar(20), SERVERPROPERTY('servername'))) +`  
  
 `' (' +`  
  
 `rtrim(CONVERT(nvarchar(20), SERVERPROPERTY('productversion'))) +`  
  
 `')'`  
  
 `:setvar SQLCMDMAXFIXEDTYPEWIDTH 100`  
  
 `SET NOCOUNT OFF`  
  
 `GO`  
  
 `:setvar SQLCMDMAXFIXEDTYPEWIDTH`  
  
 다음은 `init.sql` 가 시작될 때 `sqlcmd` 파일을 호출합니다.  
  
 `C:\> SET sqlcmdini=c:\init.sql`  
  
 `>1 Sqlcmd`  
  
 다음은 출력입니다.  
  
 `>1 < user > is connected to < server > (9.00.2047.00)`  
  
> [!NOTE]  
>  **-X** 옵션은 시작 스크립트 기능을 사용하지 않도록 설정합니다.  
  
### <a name="f-variable-expansion"></a>6. 변수 확장  
 다음 예에서는 **sqlcmd** 변수 형식의 데이터로 작업하는 방법을 보여 줍니다.  
  
 `USE AdventureWorks2012;`  
  
 `CREATE TABLE AdventureWorks2012.dbo.VariableTest`  
  
 `(`  
  
 `Col1 nvarchar(50)`  
  
 `);`  
  
 `GO`  
  
 `Col1` 값을 포함하는 `dbo.VariableTest` 의 `$(tablename)`에 하나의 행을 삽입합니다.  
  
 `INSERT INTO AdventureWorks2012.dbo.VariableTest(Col1)`  
  
 `VALUES('$(tablename)');`  
  
 `GO`  
  
 `sqlcmd` 프롬프트에서 `$(tablename)`와 같게 설정된 변수가 없을 경우 다음 문은 행을 반환합니다.  
  
 `C:\> sqlcmd`  
  
 `>1 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = '$(tablename)';`  
  
 `>2 GO`  
  
 `>3 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = N'$(tablename)';`  
  
 `>4 GO`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `>1 Col1`  
  
 `>2 ------------------`  
  
 `>3 $(tablename)`  
  
 `>4`  
  
 `>5 (1 rows affected)`  
  
 `MyVar` 변수가 `$(tablename)`으로 설정된 경우  
  
 `>6 :setvar MyVar $(tablename)`  
  
 다음 문은 행을 반환하며 "'tablename' 스크립팅 변수가 정의되지 않습니다"라는 메시지도 반환합니다.  
  
 `>6 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = '$(tablename)';`  
  
 `>7 GO`  
  
 `>1 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = N'$(tablename)';`  
  
 `>2 GO`  
  
 다음 문은 행을 반환합니다.  
  
 `>1 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = '$(MyVar)';`  
  
 `>2 GO`  
  
 `>1 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = N'$(MyVar)';`  
  
 `>2 GO`  
  
## <a name="see-also"></a>관련 항목  
 [sqlcmd 유틸리티 사용](sqlcmd-use-the-utility.md)   
 [-b](../../tools/sqlcmd-utility.md)   
 [명령 프롬프트 유틸리티 참조&#40;데이터베이스 엔진#41;](../../tools/command-prompt-utility-reference-database-engine.md)  
  
  
