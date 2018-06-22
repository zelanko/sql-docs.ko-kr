---
title: Hello World Ready 예제 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 1cb94266-f702-4a57-a1ae-689a89c98757
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e4fed72859ff91a9a0056529893c7f5664fe6254
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088915"
---
# <a name="hello-world-ready-sample"></a>Hello World Ready 예제
  Hello World Ready 예제는 간단한 World Ready CLR(공용 언어 런타임) 통합 기반 저장 프로시저 만들기, 배포 및 테스트와 관련된 기본 작업을 보여 줍니다. World Ready 구성 요소는 구성 요소의 원본 코드를 변경할 필요 없이 세계 곳곳의 다양한 시장에서 다양한 언어로 쉽게 지역화할 수 있습니다. 또한 이 예제에서는 저장 프로시저에 의해 동적으로 생성되고 클라이언트로 반환되는 레코드 및 출력 매개 변수를 통해 데이터를 반환하는 방법을 보여 줍니다. 이 예제는 Hello World 예제와 거의 동일하지만 훨씬 더 쉽고 안전하게 이 응용 프로그램을 지역화할 수 있습니다. 지역화된 텍스트를 변경하려면 다음을 수행해야 합니다.  
  
1.  (오류로 인해 XML 파일을 변경합니다.`resx` 리소스 디렉터리에서 특정 culture에 대 한 파일)  
  
2.  `resgen`을 사용하여 해당 culture의 리소스 파일 빌드  
  
3.  해당 culture에 대한 업데이트된 위성 DLL 빌드  
  
4.  SQL Server에서 해당 어셈블리 삭제 및 추가  
  
 CLR 저장 프로시저 자체에 대한 원본 코드 및 어셈블리는 변경되지 않습니다. 리소스 어셈블리를 컴파일하고 연결하는 방법을 보여 주는 `build.cmd` 스크립트가 제공됩니다. 응용 프로그램의 원본 코드는 현재 실행 중인 어셈블리에 기반하는 리소스 관리자를 만들지만 저장 프로시저를 포함하는 DLL에 culture 중립 리소스를 포함해야 할 필요는 없습니다. `System.Resources.NeutralResourcesLanguage attribute` 특성이 있으면 위성 DLL에 culture 중립 리소스가 존재할 수 있습니다. 이 경우 지역화된 텍스트를 추가 또는 변경할 때 CLR 저장 프로시저가 포함된 기본 DLL을 변경할 필요가 없도록 별도의 DLL을 사용하는 것이 좋습니다. 특히 열 및 기타 종속성을 갖고 있어 유형을 삭제하고 다시 추가하기가 어려운 CLR 사용자 정의 형식의 경우 이 방법이 유용합니다. 일반적으로 위성 DLL 버전은 주 어셈블리 버전과 동일해야 합니다. 하지만 `SatelliteContractVersion` 특성을 사용하여 위성 어셈블리를 업데이트하지 않고 주 어셈블리만 업데이트하도록 할 수도 있습니다. 자세한 내용은 Microsoft .NET 설명서에서 `ResourceManager` 클래스를 참조하십시오.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 예제는 SQL Server 2005 이상 버전에서만 작동합니다.  
  
 이 프로젝트를 만들고 실행하려면 다음 소프트웨어가 설치되어 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 설명서 및 예제 [웹 사이트](http://go.microsoft.com/fwlink/?LinkId=31046)에서 무료로 구할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개발자 [웹 사이트](http://go.microsoft.com/fwlink/?linkid=62796)에서 제공되는 AdventureWorks 데이터베이스  
  
-   .NET Framework SDK 2.0 이상 또는 Microsoft Visual Studio 2005 이상. .NET Framework SDK는 무료로 구할 수 있습니다.  
  
-   또한 다음 조건을 충족해야 합니다.  
  
-   사용하고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 CLR 통합이 설정되어 있어야 합니다.  
  
-   CLR 통합을 설정하려면 다음 단계를 수행합니다.  
  
    #### <a name="enabling-clr-integration"></a>CLR 통합 사용  
  
    -   다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 실행합니다.  
  
     `sp_configure 'clr enabled', 1`  
  
     `GO`  
  
     `RECONFIGURE`  
  
     `GO`  
  
    > [!NOTE]  
    >  CLR을 사용하도록 설정하려면 `ALTER SETTINGS` 서버 수준 사용 권한이 있어야 합니다. 이 사용 권한은 `sysadmin` 및 `serveradmin` 고정 서버 역할의 멤버가 암시적으로 소유합니다.  
  
-   사용하고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 AdventureWorks 데이터베이스를 설치해야 합니다.  
  
-   사용하고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 관리자가 아닌 경우 설치를 완료하기 위해 관리자로부터 **CreateAssembly**  권한을 부여 받아야 합니다.  
  
## <a name="building-the-sample"></a>예제 빌드  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>다음 지침을 사용하여 예제를 만들고 실행합니다.  
  
1.  Visual Studio 또는 .NET Framework 명령 프롬프트를 엽니다.  
  
2.  필요한 경우 예제에 대한 디렉터리를 만듭니다. 이 예에서는 C:\MySample을 사용합니다.  
  
3.  c:\MySample에서 `HelloWorld.vb`(Visual Basic 예제용) 또는 `HelloWorld.cs`(C# 예제용)를 만들고 적합한 Visual Basic 또는 C# 예제 코드(아래)를 파일에 복사합니다.  
  
4.  c:\MySample에서 `messages.resx` 파일을 만들고 예제 코드를 파일에 복사합니다.  
  
5.  C:\mysample에서 파일을 만들 `messages.de.resx` 파일을 저장 하 여 `messages.resx` 으로 `messages.de.resx` 줄을 변경한 후  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   아래와 같이 읽으려면  
  
    -   `<value xml:space="preserve">Hallo Welt!</value>`  
  
6.  C:\mysample에서 파일을 만들 `messages.es.resx` 파일을 저장 하 여 `messages.resx` 으로 `messages.es.resx` 줄을 변경한 후  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   아래와 같이 읽으려면  
  
    -   `<value xml:space="preserve">Hola a todos</value>`  
  
7.  C:\mysample에서 파일을 만들 `messages.fr.resx` 파일을 저장 하 여 `messages.resx` 으로 `messages.fr.resx` 줄을 변경한 후  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   아래와 같이 읽으려면  
  
    -   `<value xml:space="preserve">BonjourÂ !</value>`  
  
8.  C:\mysample에서 파일을 만들 `messages.fr-FR.resx` 파일을 저장 하 여 `messages.resx` 으로 `messages.fr-FR.resx` 줄을 변경한 후  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   아래와 같이 읽으려면  
  
    -   `<value xml:space="preserve">Bonjour de France!</value>`  
  
9. C:\mysample에서 파일을 만들 `messages.it.resx` 파일을 저장 하 여 `messages.resx` 으로 `messages.it.resx` 줄을 변경한 후  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   아래와 같이 읽으려면  
  
    -   `<value xml:space="preserve">Buongiorno</value>`  
  
10. C:\mysample에서 파일을 만들 `messages.ja.resx` 파일을 저장 하 여 `messages.resx` 으로 `messages.ja.resx` 줄을 변경한 후  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   아래와 같이 읽으려면  
  
    -   `<value xml:space="preserve">` `ã“ã‚“ã«ã¡ã¯</value>`  
  
11. c:\MySample에서 `build.com` 파일을 만들고 예제 코드를 파일에 복사합니다.  
  
12. 명령 프롬프트에서 파일 빌드를 실행하여 위성 어셈블리를 빌드합니다.  
  
13. 다음 중 하나를 실행하여 명령줄 프롬프트에서 예제 코드를 컴파일합니다.  
  
    -   `Vbc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /out:HelloWorldReady.dll /target:library HelloWorld.vb`  
  
    -   `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.XML.dll /out:HelloWorldReady.dll /target:library Hello.csCopy the tsql installation code into a file and save it as Install.sql in the sample directory.`  
  
14. 예제가 `C:\MySample\`이외의 디렉터리에 설치된 경우 해당 위치를 가리키도록 표시된 대로 `Install.sql` 파일을 편집합니다.  
  
15. 다음을 실행하여 어셈블리 및 저장 프로시저를 배포합니다.  
  
    -   `sqlcmd -E -I -i install.sql`  
  
16. [!INCLUDE[tsql](../../includes/tsql-md.md)] 테스트 명령 스크립트를 파일에 복사하고 해당 파일을 예제 디렉터리에 `test.sql` 로 저장합니다.  
  
17. 다음 명령으로 테스트 스크립트를 실행합니다.  
  
    -   `sqlcmd -E -I -i test.sql`  
  
18. [!INCLUDE[tsql](../../includes/tsql-md.md)] 정리 스크립트를 파일에 복사하고 해당 파일을 예제 디렉터리에 `cleanup.sql` 로 저장합니다.  
  
19. 다음 명령으로 스크립트를 실행합니다.  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>예제 코드  
 다음은 이 예제에 대한 코드 목록입니다.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Globalization;  
using System.Threading;  
using System.Resources;  
using System.Reflection;  
using System.Runtime.CompilerServices;  
  
[assembly: System.Resources.NeutralResourcesLanguage("", System.Resources.UltimateResourceFallbackLocation.Satellite)]  
[assembly: System.Security.Permissions.SecurityPermissionAttribute(System.Security.Permissions.SecurityAction.RequestMinimum)]  
[assembly: System.Runtime.ConstrainedExecution.ReliabilityContract(System.Runtime.ConstrainedExecution.Consistency.MayCorruptInstance, System.Runtime.ConstrainedExecution.Cer.None)]  
  
    public sealed partial class StoredProcedures  
    {  
        private StoredProcedures()  
        {  
        }  
  
        [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1021:AvoidOutParameters"), Microsoft.SqlServer.Server.SqlProcedure]  
        public static void HelloWorldReady(string culture, out string greeting)  
        {  
ResourceManager rm   
= new ResourceManager("Messages",   
Assembly.GetExecutingAssembly());  
  
string message = rm.GetString("HelloWorld", CultureInfo.GetCultureInfo(culture));  
  
            Microsoft.SqlServer.Server.SqlMetaData columnInfo  
                = new Microsoft.SqlServer.Server.SqlMetaData("Column1", SqlDbType.NVarChar, 24);  
            SqlDataRecord greetingRecord  
                = new SqlDataRecord(new Microsoft.SqlServer.Server.SqlMetaData[] { columnInfo });  
            greetingRecord.SetString(0, message);  
            SqlContext.Pipe.Send(greetingRecord);  
            greeting = message;  
        }  
    }  
  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Globalization  
Imports System.Resources  
Imports System.Reflection  
Imports System.Runtime.InteropServices  
<Assembly: AssemblyVersion("1.0.*")>   
<Assembly: System.Runtime.InteropServices.ComVisible(False)>   
<Assembly: System.CLSCompliant(True)>   
<Assembly: System.Resources.NeutralResourcesLanguage("", System.Resources.UltimateResourceFallbackLocation.Satellite)>   
<Assembly: System.Security.Permissions.SecurityPermissionAttribute(System.Security.Permissions.SecurityAction.RequestMinimum)>   
<Assembly: System.Runtime.ConstrainedExecution.ReliabilityContract(System.Runtime.ConstrainedExecution.Consistency.WillNotCorruptState, Runtime.ConstrainedExecution.Cer.None)>   
  
Partial Public NotInheritable Class StoredProcedures  
    Private Sub New()  
    End Sub  
    <Microsoft.SqlServer.Server.SqlProcedure()> _  
    Public Shared Sub HelloWorldReady(ByVal culture As String, ByRef greeting As String)  
        Dim rm As New ResourceManager("Messages", Assembly.GetExecutingAssembly())  
        Dim message As String = rm.GetString("HelloWorld", CultureInfo.GetCultureInfo(culture))  
        Dim columnInfo As New Microsoft.SqlServer.Server.SqlMetaData("Column1", _  
            SqlDbType.NVarChar, 24)  
        Dim greetingRecord As New SqlDataRecord(New  _  
            Microsoft.SqlServer.Server.SqlMetaData() {columnInfo})  
        greetingRecord.SetString(0, message)  
        SqlContext.Pipe.Send(greetingRecord)  
        greeting = message  
    End Sub  
End Class  
  
```  
  
 이는 위성 어셈블리를 빌드하는 `build.com`입니다.  
  
```  
resgen Messages.resx  
resgen Messages.de.resx  
resgen Messages.es.resx  
resgen Messages.fr.resx  
resgen Messages.fr-Fr.resx  
resgen Messages.it.resx  
resgen Messages.ja.resx  
if not exist de/ mkdir de  
if not exist es/ mkdir es  
if not exist fr/ mkdir fr  
if not exist fr-FR/ mkdir fr-FR  
if not exist it/ mkdir it  
if not exist ja/ mkdir ja  
al /t:lib /culture:de /embed:Messages.de.resources /out:de\HelloWorldReady.resources.dll  
al /t:lib /culture:es /embed:Messages.es.resources /out:es\HelloWorldReady.resources.dll  
al /t:lib /culture:fr /embed:Messages.fr.resources /out:fr\HelloWorldReady.resources.dll  
al /t:lib /culture:fr-FR /embed:Messages.fr-FR.resources /out:fr-FR\HelloWorldReady.resources.dll  
al /t:lib /culture:it /embed:Messages.it.resources /out:it\HelloWorldReady.resources.dll  
al /t:lib /culture:ja /embed:Messages.ja.resources /out:ja\HelloWorldReady.resources.dll  
al /t:lib /culture:"" /embed:Messages.resources /out:HelloWorldReady.resources.dll  
```  
  
 이는 어셈블리를 배포하고 데이터베이스 내에서 저장 프로시저를 만드는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 설치 스크립트(`Install.sql`)입니다.  
  
```  
USE AdventureWorks  
GO  
  
-- Drop existing sproc and assembly if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_HelloWorldReady')  
DROP PROCEDURE usp_HelloWorldReady;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady')  
DROP ASSEMBLY HelloWorldReady;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.neutral')  
DROP ASSEMBLY [HelloWorldReady.resources.neutral]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.de')  
DROP ASSEMBLY [HelloWorldReady.resources.de]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.es')  
DROP ASSEMBLY [HelloWorldReady.resources.es]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.fr')  
DROP ASSEMBLY [HelloWorldReady.resources.fr]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.fr-FR')  
DROP ASSEMBLY [HelloWorldReady.resources.fr-FR]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.it')  
DROP ASSEMBLY [HelloWorldReady.resources.it]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.ja')  
DROP ASSEMBLY [HelloWorldReady.resources.ja]  
GO  
  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of this variable if you have installed the sample someplace other than the default location.  
Set @SamplesPath = N'C:\MySample\'  
  
-- Add the assembly and CLR integration based stored procedure  
  
CREATE ASSEMBLY HelloWorldReady  
FROM @SamplesPath + 'HelloWorldReady.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.neutral]  
FROM @SamplesPath + 'HelloWorldReady.resources.dll'  
WITH permission_set = Safe;   
  
CREATE ASSEMBLY [HelloWorldReady.resources.de]  
FROM @SamplesPath + '\de\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.es]  
FROM @SamplesPath + '\es\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.fr]  
FROM @SamplesPath + '\fr\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.fr-FR]  
FROM @SamplesPath + '\fr-FR\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.it]  
FROM @SamplesPath + '\it\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.ja]  
FROM @SamplesPath + '\ja\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
GO  
  
CREATE PROCEDURE usp_HelloWorldReady  
(  
@Culture NVarchar(12),  
@Greeting NVarchar(24) OUTPUT  
)  
AS EXTERNAL NAME HelloWorldReady.StoredProcedures.HelloWorldReady;  
GO  
  
USE master;  
GO  
```  
  
 이는 각 로캘에서 함수를 실행하여 예제를 테스트하는 `test.sql`입니다.  
  
```  
USE AdventureWorks  
GO  
  
DECLARE @GreetingDe nvarchar(24);  
DECLARE @GreetingDe_CH nvarchar(24);  
DECLARE @GreetingEn nvarchar(24);  
DECLARE @GreetingEs nvarchar(24);  
DECLARE @GreetingFr nvarchar(24);  
DECLARE @GreetingFr_FR nvarchar(24);  
DECLARE @GreetingIt nvarchar(24);  
DECLARE @GreetingJa nvarchar(24);  
  
--German as spoken anywhere in the world (the neutral German culture)  
EXEC usp_HelloWorldReady 'de', @GreetingDe OUTPUT;  
--German as spoken in Switzerland.  Because we don't have a specific assembly  
--for this case, the .NET Framework will automatically fall back to the neutral German culture DLL.  
EXEC usp_HelloWorldReady 'de-CH', @GreetingDe_CH OUTPUT;  
EXEC usp_HelloWorldReady 'en', @GreetingEn OUTPUT;  
EXEC usp_HelloWorldReady 'es', @GreetingEs OUTPUT;  
--French as spoken anywhere in the world (the neutral French culture)  
EXEC usp_HelloWorldReady 'fr', @GreetingFr OUTPUT  
--French as spoken in France.  Since we do have a specific assembly for this case, a specific   
--greeting is provided from that DLL.  The neutral French culture DLL is not used in this case.  
EXEC usp_HelloWorldReady 'fr-FR', @GreetingFr_FR OUTPUT  
EXEC usp_HelloWorldReady 'it', @GreetingIt OUTPUT;  
EXEC usp_HelloWorldReady 'ja', @GreetingJa OUTPUT;  
  
SELECT @GreetingDe AS OUTPUT_PARAMETER_DE;  
SELECT @GreetingDe_CH AS OUTPUT_PARAMETER_De_CH;  
SELECT @GreetingEn AS OUTPUT_PARAMETER_EN;  
SELECT @GreetingEs AS OUTPUT_PARAMETER_ES;  
SELECT @GreetingFr AS OUTPUT_PARAMETER_FR;  
SELECT @GreetingFr_FR AS OUTPUT_PARAMETER_Fr_FR;  
SELECT @GreetingIt AS OUTPUT_PARAMETER_IT;  
SELECT @GreetingJa AS OUTPUT_PARAMETER_JA;  
  
GO  
```  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)]은 데이터베이스에서 어셈블리 및 저장 프로시저를 제거합니다.  
  
```  
USE AdventureWorks;  
GO  
  
-- Drop existing sproc and assembly if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_HelloWorldReady')  
DROP PROCEDURE usp_HelloWorldReady;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady')  
DROP ASSEMBLY HelloWorldReady;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.neutral')  
DROP ASSEMBLY [HelloWorldReady.resources.neutral]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.de')  
DROP ASSEMBLY [HelloWorldReady.resources.de]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.es')  
DROP ASSEMBLY [HelloWorldReady.resources.es]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.fr')  
DROP ASSEMBLY [HelloWorldReady.resources.fr]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.fr-FR')  
DROP ASSEMBLY [HelloWorldReady.resources.fr-FR]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.it')  
DROP ASSEMBLY [HelloWorldReady.resources.it]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.ja')  
DROP ASSEMBLY [HelloWorldReady.resources.ja]  
GO  
  
USE master;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [공용 언어 런타임 &#40;CLR&#41; 통합에 대한 사용 시나리오 및 예제](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  