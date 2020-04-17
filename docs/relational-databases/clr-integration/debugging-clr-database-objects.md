---
title: CLR 데이터베이스 개체 디버깅 | 마이크로 소프트 문서
description: SQL Server는 SQL Server 디버거를 Microsoft Visual Studio 디버거와 통합하는 데이터베이스의 Transact-SQL 및 CLR 개체 디버깅을 지원합니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- database objects [CLR integration], debugging
- permissions [CLR integration]
- debugging [CLR integration]
- building database objects [CLR integration], debugging
- common language runtime [SQL Server], debugging
ms.assetid: 1332035c-d6ed-424d-8234-46ad21168319
author: rothja
ms.author: jroth
ms.openlocfilehash: 71a766dc473c1bef47a8104ae76c0e70bd8b31b8
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488399"
---
# <a name="debugging-clr-database-objects"></a>CLR 데이터베이스 개체 디버깅
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 데이터베이스의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 CLR(공용 언어 런타임) 개체 디버깅을 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디버깅에서 중요한 점은, 설치 및 사용이 쉽고 SQL Server 디버거를 Microsoft Visual Studio 디버거와 통합할 수 있다는 것입니다. 또한 디버깅이 여러 언어에서 작동합니다. 사용자는 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 CLR 개체로 매끄럽게 한 단계씩 코드를 실행할 수 있으며 그 반대의 경우도 가능합니다. 관리되는 데이터베이스 개체를 디버깅할 때는 SQL Server Management Studio의 Transact-SQL 디버거를 사용할 수 없지만 Visual Studio의 디버거를 사용하여 개체를 디버깅할 수 있습니다. Visual Studio의 관리되는 데이터베이스 개체 디버깅은 서버에서 실행 중인 루틴에서 "step into" 및 "step over" 문과 같은 대부분의 일반적인 디버깅 기능을 지원합니다. 디버거는 디버깅하는 동안 중단점을 설정하고, 호출 스택을 검사하고, 변수를 검사하고, 변수 값을 수정할 수 있습니다. Visual Studio .NET 2003은 CLR 통합 프로그래밍 또는 디버깅에 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 .NET Framework가 미리 설치되어 있으며 Visual Studio .NET 2003에서는 .NET Framework 2.0 어셈블리를 사용할 수 없습니다.  
  
 Visual Studio를 사용하여 관리되는 코드 디버깅에 대한 자세한 내용은 Visual Studio 설명서의["디버깅 관리 코드"](https://go.microsoft.com/fwlink/?LinkId=120377)항목을 참조하십시오.  
  
## <a name="debugging-permissions-and-restrictions"></a>디버깅 권한 및 제한 사항  
 디버깅은 권한이 높은 작업이므로 **에서 sysadmin** 고정 서버 역할의 구성원만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]허용됩니다.  
  
 디버깅하는 동안에는 다음 제한 사항이 적용됩니다.  
  
-   CLR 루틴 디버깅은 한 번에 하나의 디버거 인스턴스로 제한됩니다. 이 제한이 적용되는 이유는, 중단점에 도달하면 모든 CLR 코드 실행이 중지되고 이 중단점에서 디버거가 전진할 때까지 실행이 멈추기 때문입니다. 하지만 다른 연결에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버깅을 계속할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버깅은 서버의 다른 실행을 중지하지는 않지만 잠금을 보유함으로써 다른 연결들을 기다리게 만드는 원인이 됩니다.  
  
-   기존 연결은 디버깅할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 연결을 만들려면 클라이언트 및 디버거 환경에 대한 정보가 필요하므로 새 연결만 디버깅할 수 있습니다.  
  
 위의 제한 사항으로 인해 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 CLR 코드를 테스트 서버에서 디버깅하는 것이 좋습니다. 프로덕션 서버는 사용하지 마십시오.  
  
## <a name="overview-of-debugging-managed-database-objects"></a>관리되는 데이터베이스 개체 디버깅 개요  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 디버깅은 각 연결 모델을 따릅니다. 디버거는 자신이 연결된 클라이언트 연결에 대해서만 작업을 감지하고 디버깅할 수 있습니다. 디버거 기능은 연결 유형의 제한을 받지 않으므로 TDS(Tabular Data Stream) 및 HTTP 연결을 모두 디버깅할 수 있습니다. 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기존 연결 디버깅은 허용되지 않습니다. 디버깅은 서버에서 실행 중인 루틴에서 대부분의 일반적인 디버깅 기능을 지원합니다. 디버거와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 간의 상호 작용은 분산 COM(구성 요소 개체 모델)을 통해 이루어집니다.  
  
 관리되는 저장 프로시저, 함수, 트리거, 사용자 정의 형식 및 집계 디버깅에 대한 자세한 정보 및 시나리오는 Visual Studio 설명서의["SQL Server CLR 통합 데이터베이스 디버깅"](https://go.microsoft.com/fwlink/?LinkId=120378)항목을 참조하십시오.  
  
 Visual Studio를 원격 개발, 디버깅 및 개발에 사용하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 TCP/IP 네트워크 프로토콜을 사용할 수 있어야 합니다. 서버에서 TCP/IP 프로토콜을 사용하도록 설정하는 방법에 대한 자세한 내용은 [클라이언트 프로토콜 구성](../../database-engine/configure-windows/configure-client-protocols.md)을 참조하십시오.  
  
#### <a name="to-debug-a-managed-database-object"></a>관리되는 데이터베이스 개체를 디버깅하려면  
  
1.  Microsoft Visual Studio를 열고 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로젝트를 만든 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 데이터베이스에 대한 연결을 설정합니다.  
  
2.  새 형식을 만듭니다. **솔루션 탐색기에서**프로젝트를 마우스 오른쪽 단추로 클릭하고 새 항목 추가 및 **새 항목 선택...** **Add** 새 **항목 추가** 창에서 **저장 프로시저,** **사용자 정의 함수,** **사용자 정의 유형,** **트리거,** **집계**또는 **클래스를**선택합니다. 새 형식의 원본 파일에 대한 이름을 지정하고 **추가 를**클릭합니다.  
  
3.  새 형식의 코드를 텍스트 편집기에 추가합니다. 저장 프로시저의 예제 코드는 이 항목의 뒷부분에 나오는 섹션을 참조하십시오.  
  
4.  형식을 테스트하는 스크립트를 추가합니다. **솔루션 탐색기에서** **TestScripts** 디렉터리를 두 번 클릭하여 **Test.sql을** 확장하여 기본 테스트 스크립트 원본 파일을 엽니다. 디버깅할 코드를 호출하는 테스트 스크립트 하나를 텍스트 편집기에 추가합니다. 예제 스크립트는 아래를 참조하십시오.  
  
5.  원본 코드에 중단점을 하나 이상 배치합니다. 디버깅하려는 함수 또는 루틴 내에서 텍스트 편집기의 코드 줄을 마우스 오른쪽 단추로 클릭하고 **중단점** 및 **중단점 삽입을**선택합니다. 중단점이 추가되어 코드 줄이 빨간색으로 강조 표시됩니다.  
  
6.  **디버그** 메뉴에서 **디버깅 시작을** 선택하여 프로젝트를 컴파일, 배포 및 테스트합니다. Test.sql의 테스트 스크립트가 실행되고 관리되는 데이터베이스 개체가 호출됩니다.  
  
7.  명령 포인터를 가리키는 노란색 화살표가 중단점에 나타나면 코드 실행이 중지되고 관리되는 데이터베이스 개체의 디버깅을 시작할 수 있습니다. **디버그** 메뉴에서 **단계별로 이동하여** 명령 포인터를 다음 코드 줄로 진행할 수 있습니다. **지역 창은** 현재 명령 포인터에 의해 강조 표시된 개체의 상태를 관찰하는 데 사용됩니다. **변수를 보기** 창에 추가할 수 있습니다. 그러면 변수가 현재 명령 포인터로 강조 표시된 코드 줄에 있을 때뿐만 아니라 전체 디버깅 세션에 걸쳐 조사 변수의 상태를 관찰할 수 있습니다. 명령 포인터를 다음 중단점으로 전진하려면 디버그 메뉴에서 계속을 선택하고, 또는 더 이상 중단점이 없으면 루틴 실행을 완료합니다.  
  
### <a name="example"></a>예제  
 다음 예에서는 호출자에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 반환합니다.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void GetVersion()  
   {  
   using(SqlConnection connection = new SqlConnection("context connection=true"))   
   {  
      connection.Open();  
      SqlCommand command = new SqlCommand("select @@version",  
                                           connection);  
      SqlContext.Pipe.ExecuteAndSend(command);  
      }  
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
Imports System.Data.SqlClient  
  
Partial Public Class StoredProcedures   
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub GetVersion()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            SqlContext.Pipe.ExecuteAndSend(command)  
        End Using  
    End Sub  
End Class  
```  
  
 다음은 위에 정의된 GetVersion 저장 프로시저를 호출하는 테스트 스크립트입니다.  
  
```  
EXEC GetVersion  
```  
  
## <a name="see-also"></a>참고 항목  
 [CLR&#40;공용 언어 런타임&#41; 통합 프로그래밍 개요](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
