---
title: Hello World 예제 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
ms.assetid: fed6c358-f5ee-4d4c-9ad6-089778383ba7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b679c93d8e946092518ca9bc020c3fbcfca834d5
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53366765"
---
# <a name="hello-world-sample"></a>Hello World 예제
  Hello World 예제는 간단한 CLR(공용 언어 런타임) 통합 기반 저장 프로시저의 만들기, 배포 및 테스트와 관련된 기본 작업을 보여 줍니다. 이 예제는 저장 프로시저에 의해 동적으로 생성되고 호출자로 반환되는 레코드를 통해 데이터를 반환하는 방법도 보여 줍니다.  
  
 `HelloWorld` "Hello world!" 프로시저가 문자열을 반환 합니다. 결과 하나의 행으로 구성 된 집합입니다. 이 예제에는 클래스에 대 한 몇 가지 사용 방법을 보여 줍니다. [Microsoft.SqlServer.Server.SqlMetaData](https://go.microsoft.com/fwlink/?LinkID=193572)하십시오 [Microsoft.SqlServer.Server.SqlDataRecord](https://go.microsoft.com/fwlink/?LinkID=193573) 고 [ Microsoft.SqlServer.Server.Pipe](https://go.microsoft.com/fwlink/?LinkID=193571)합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 프로젝트를 만들고 실행하려면 다음 소프트웨어가 설치되어 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 설명서 및 예제 [웹 사이트](https://go.microsoft.com/fwlink/?LinkId=31046)에서 무료로 구할 수 있습니다.  
  
-    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개발자 [웹 사이트](https://go.microsoft.com/fwlink/?linkid=62796)에서 제공되는 AdventureWorks 데이터베이스  
  
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
  
-   사용하고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 관리자가 아닌 경우 설치를 완료하기 위해 관리자로부터 **CreateAssembly** 권한을 부여 받아야 합니다.  
  
## <a name="building-the-sample"></a>예제 빌드  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>다음 지침을 사용하여 예제를 만들고 실행합니다.  
  
1.  Visual Studio 또는 .NET Framework 명령 프롬프트를 엽니다.  
  
2.  필요한 경우 예제에 대한 디렉터리를 만듭니다. 이 예에서는 C:\MySample을 사용합니다.  
  
3.  c:\MySample에서 `HelloWorld.vb`(Visual Basic 예제용) 또는 `HelloWorld.cs`(C# 예제용)를 만들고 적합한 Visual Basic 또는 C# 예제 코드(아래)를 파일에 복사합니다.  
  
4.  선택하는 언어에 따라 다음 중 하나를 실행하여 명령줄 프롬프트에서 예제 코드를 컴파일합니다.  
  
    -   `vbc C:HelloWorld.vb /target:library`  
  
    -   `csc /target:library HelloWorld.cs`  
  
5.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 설치 코드를 파일에 복사하고 해당 파일을 예제 디렉터리에 `Install.sql` 로 저장합니다.  
  
6.  다음을 실행하여 어셈블리 및 저장 프로시저를 배포합니다.  
  
    -   `sqlcmd -E -I -i install.sql -v root = "C:\MySample\"`  
  
7.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 테스트 명령 스크립트를 파일에 복사하고 해당 파일을 예제 디렉터리에 `test.sql` 로 저장합니다.  
  
8.  다음 명령으로 테스트 스크립트를 실행합니다.  
  
    -   `sqlcmd -E -I -i test.sql`  
  
9. [!INCLUDE[tsql](../../includes/tsql-md.md)] 정리 스크립트를 파일에 복사하고 해당 파일을 예제 디렉터리에 `cleanup.sql` 로 저장합니다.  
  
10. 다음 명령으로 스크립트를 실행합니다.  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>예제 코드  
 다음은 이 예제에 대한 코드 목록입니다.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
public partial class StoredProcedures  
{  
    [Microsoft.SqlServer.Server.SqlProcedure]  
    public static void HelloWorld()  
    {  
        Microsoft.SqlServer.Server.SqlMetaData columnInfo  
                = new Microsoft.SqlServer.Server.SqlMetaData("Column1", SqlDbType.NVarChar, 12);  
        SqlDataRecord greetingRecord  
            = new SqlDataRecord(new Microsoft.SqlServer.Server.SqlMetaData[] { columnInfo });  
        greetingRecord.SetString(0, "Hello world!");  
        SqlContext.Pipe.Send(greetingRecord);  
    }  
};  
  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Partial Public NotInheritable Class StoredProcedures  
    <Microsoft.SqlServer.Server.SqlProcedure()> _  
    Public Shared Sub HelloWorld()  
        Dim columnInfo As New Microsoft.SqlServer.Server.SqlMetaData("Column1", _  
            SqlDbType.NVarChar, 12)  
        Dim greetingRecord As New SqlDataRecord(New  _  
            Microsoft.SqlServer.Server.SqlMetaData() {columnInfo})  
        greetingRecord.SetString(0, "Hello World!")  
        SqlContext.Pipe.Send(greetingRecord)  
    End Sub  
End Class  
```  
  
 이는 어셈블리를 배포하고 데이터베이스 내에서 저장 프로시저를 만드는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 설치 스크립트(`Install.sql`)입니다.  
  
```  
USE AdventureWorks  
GO  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_HelloWorld')  
DROP PROCEDURE usp_HelloWorld;  
GO  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorld')  
DROP ASSEMBLY HelloWorld;  
GO  
DECLARE @SamplesPath nvarchar(1024)  
set @SamplesPath = '$(root)'  
CREATE ASSEMBLY HelloWorld   
FROM @SamplesPath + 'HelloWorld.dll'  
WITH permission_set = Safe;  
GO  
  
CREATE PROCEDURE usp_HelloWorld  
--(  
--    @Greeting nvarchar(12) OUTPUT  
--)  
AS EXTERNAL NAME HelloWorld.[StoredProcedures].HelloWorld;  
GO  
```  
  
 이는 저장 프로시저를 실행하여 예제를 테스트하는 `test.sql`입니다.  
  
```  
use AdventureWorks  
go  
execute usp_HelloWorld  
  
USE AdventureWorks;  
GO  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_HelloWorld')  
DROP PROCEDURE usp_HelloWorld;  
GO  
```  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 은 데이터베이스에서 어셈블리 및 저장 프로시저를 제거합니다.  
  
```  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_HelloWorld')  
DROP PROCEDURE usp_HelloWorld;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorld')  
DROP ASSEMBLY HelloWorld;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [공용 언어 런타임 &#40;CLR&#41; 통합에 대한 사용 시나리오 및 예제](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
