---
title: CLR (공용 언어 런타임) 데이터베이스 개체 디버그
description: SQL Server는 SQL Server 디버거를 Microsoft Visual Studio 디버거와 통합 하는 데이터베이스에서 Transact-sql 및 CLR 개체 디버깅을 지원 합니다.
ms.date: 10/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: how-to
helpviewer_keywords:
- database objects [CLR integration], debugging
- permissions [CLR integration]
- debugging [CLR integration]
- building database objects [CLR integration], debugging
- common language runtime [SQL Server], debugging
ms.assetid: 1332035c-d6ed-424d-8234-46ad21168319
author: rothja
ms.author: jroth
ms.openlocfilehash: 2a6e723c8ad5ff8c97a3b57edb554092211da4d7
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91785161"
---
# <a name="how-to-debug-clr-database-objects"></a>CLR 데이터베이스 개체를 디버깅 하는 방법

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 데이터베이스의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 CLR(공용 언어 런타임) 개체 디버깅을 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디버깅에서 중요한 점은, 설치 및 사용이 쉽고 SQL Server 디버거를 Microsoft Visual Studio 디버거와 통합할 수 있다는 것입니다. 또한 디버깅이 여러 언어에서 작동합니다. 사용자는 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 CLR 개체로 매끄럽게 한 단계씩 코드를 실행할 수 있으며 그 반대의 경우도 가능합니다. 관리되는 데이터베이스 개체를 디버깅할 때는 SQL Server Management Studio의 Transact-SQL 디버거를 사용할 수 없지만 Visual Studio의 디버거를 사용하여 개체를 디버깅할 수 있습니다. Visual Studio의 관리되는 데이터베이스 개체 디버깅은 서버에서 실행 중인 루틴에서 "step into" 및 "step over" 문과 같은 대부분의 일반적인 디버깅 기능을 지원합니다. 디버거는 디버깅하는 동안 중단점을 설정하고, 호출 스택을 검사하고, 변수를 검사하고, 변수 값을 수정할 수 있습니다. 

> [!NOTE]
> Visual Studio .NET 2003은 CLR 통합 프로그래밍 또는 디버깅에 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 .NET Framework가 미리 설치되어 있으며 Visual Studio .NET 2003에서는 .NET Framework 2.0 어셈블리를 사용할 수 없습니다.  
  
## <a name="debugging-permissions-and-restrictions"></a>디버깅 권한 및 제한 사항

디버깅은 높은 권한의 작업 이므로 **sysadmin** 고정 서버 역할의 멤버만에서이 작업을 수행할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
디버깅하는 동안에는 다음 제한 사항이 적용됩니다.  
  
- CLR 루틴 디버깅은 한 번에 하나의 디버거 인스턴스로 제한됩니다. 이 제한이 적용되는 이유는, 중단점에 도달하면 모든 CLR 코드 실행이 중지되고 이 중단점에서 디버거가 전진할 때까지 실행이 멈추기 때문입니다. 하지만 다른 연결에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버깅을 계속할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버깅은 서버의 다른 실행을 중지하지는 않지만 잠금을 보유함으로써 다른 연결들을 기다리게 만드는 원인이 됩니다.  
  
- 기존 연결은 디버깅할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 연결을 만들려면 클라이언트 및 디버거 환경에 대한 정보가 필요하므로 새 연결만 디버깅할 수 있습니다.  
  
위의 제한 사항으로 인해 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 CLR 코드를 테스트 서버에서 디버깅하는 것이 좋습니다. 프로덕션 서버는 사용하지 마십시오.  
  
## <a name="overview"></a>개요

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 디버깅은 각 연결 모델을 따릅니다. 디버거는 자신이 연결된 클라이언트 연결에 대해서만 작업을 감지하고 디버깅할 수 있습니다. 디버거 기능은 연결 유형의 제한을 받지 않으므로 TDS(Tabular Data Stream) 및 HTTP 연결을 모두 디버깅할 수 있습니다. 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 기존 연결 디버깅은 허용되지 않습니다. 디버깅은 서버에서 실행 중인 루틴에서 대부분의 일반적인 디버깅 기능을 지원합니다. 디버거와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 간의 상호 작용은 분산 COM(구성 요소 개체 모델)을 통해 이루어집니다.  
  
관리 되는 저장 프로시저, 함수, 트리거, 사용자 정의 형식 및 집계를 디버깅 하는 방법에 대 한 자세한 내용 및 시나리오는 Visual Studio 설명서의 [CLR 통합 데이터베이스 디버깅 SQL Server](https://go.microsoft.com/fwlink/?LinkId=120378) 을 참조 하세요.  
  
Visual Studio를 원격 개발, 디버깅 및 개발에 사용하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 TCP/IP 네트워크 프로토콜을 사용할 수 있어야 합니다. 서버에서 TCP/IP 프로토콜을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [클라이언트 프로토콜 구성](../../database-engine/configure-windows/configure-client-protocols.md)을 참조 하세요.  
  
## <a name="debugging-steps"></a>디버깅 단계

Microsoft Visual Studio에서 CLR 데이터베이스 개체를 디버깅 하려면 다음 단계를 사용 합니다.

1. Microsoft Visual Studio를 열고 새 SQL Server 프로젝트를 만듭니다. Visual Studio와 함께 제공 되는 SQL LocalDB 인스턴스를 사용할 수 있습니다.

2. 새 SQL CLR 형식 만들기 (c #):

   1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 항목**...을 차례로 선택 합니다. 
   1. **새 항목 추가** 창에서 **Sql Clr c # 저장 프로시저**, **Sql Clr c # 사용자 정의 함수**, **sql clr c # 사용자 정의 형식**, **Sql Clr c # 트리거**, **sql clr c # 집계**또는 **클래스**를 선택 합니다.
   1. 새 형식의 원본 파일에 대 한 이름을 지정 하 고 **추가**를 선택 합니다.

3. 새 형식의 코드를 텍스트 편집기에 추가합니다. 예제 저장 프로시저에 대 한 예제 코드는이 문서의 다음 예 섹션을 참조 하세요.

4. 형식을 테스트 하는 스크립트를 추가 합니다. 

   1. **솔루션 탐색기**에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 **추가**, **스크립트**...를 차례로 선택 합니다. 
   1. **새 항목 추가** 창에서 **스크립트 (빌드에 없음)** 를 선택 하 고와 같은 이름을 지정 `Test.sql` 합니다. **추가** 단추를 선택합니다.
   1. **솔루션 탐색기**에서 노드를 두 번 클릭 `Test.sql` 하 여 기본 테스트 스크립트 원본 파일을 엽니다.
   1. 디버깅할 코드를 호출 하는 테스트 스크립트를 텍스트 편집기에 추가 합니다. 샘플 스크립트에 대해서는 다음 섹션의 예제를 참조 하세요.

5. 원본 코드에 중단점을 하나 이상 배치합니다. 디버그 하려는 함수 또는 루틴의 텍스트 편집기에서 코드 줄을 마우스 오른쪽 단추로 클릭 합니다. **중단점**, **중단점 삽입**을 선택 합니다. 중단점이 추가되어 코드 줄이 빨간색으로 강조 표시됩니다.

6. **디버그** 메뉴에서 **디버깅 시작** 을 선택 하 여 프로젝트를 컴파일, 배포 및 테스트 합니다. 의 테스트 스크립트가 `Test.sql` 실행 되 고 관리 되는 데이터베이스 개체가 호출 됩니다.

7. 중단점에 노란색 화살표 (명령 포인터 지정)가 표시 되 면 코드 실행이 일시 중지 됩니다. 그런 다음 관리 되는 데이터베이스 개체를 디버그할 수 있습니다.

   1. **디버그** 메뉴에서 **프로시저 단위 실행** 을 사용 하 여 명령 포인터를 다음 코드 줄로 이동 합니다.
   1. **지역** 창을 사용 하 여 명령 포인터로 현재 강조 표시 된 개체의 상태를 관찰할 수 있습니다.
   1. **조사식** 창에 변수를 추가 합니다. 명령 포인터에서 현재 강조 표시 된 코드 줄에 변수가 없는 경우에도 디버깅 세션 전체에서 조사 변수의 상태를 관찰할 수 있습니다. 
   1. **디버그** 메뉴에서 **계속** 을 선택 하 여 명령 포인터를 다음 중단점으로 이동 하거나 더 이상 중단점이 없는 경우 루틴의 실행을 완료 합니다.
  
## <a name="example-code"></a>예제 코드

다음 예에서는 호출자에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 반환합니다.  
  
```csharp
using System.Data.SqlClient;
using Microsoft.SqlServer.Server;

public class StoredProcedures
{
    [Microsoft.SqlServer.Server.SqlProcedure]
    public static void GetVersion()
    {
        using (var connection = new SqlConnection("context connection=true"))
        {
            connection.Open();
            var command = new SqlCommand("select @@version", connection);
            SqlContext.Pipe.ExecuteAndSend(command);
        }
    }
}
```

## <a name="example-test-script"></a>예제 테스트 스크립트

다음 테스트 스크립트는 `GetVersion` 이전 예제에 정의 된 저장 프로시저를 호출 하는 방법을 보여 줍니다.  
  
```sql
EXEC GetVersion  
```  

## <a name="next-steps"></a>다음 단계
  
Visual Studio를 사용 하 여 관리 코드를 디버깅 하는 방법에 대 한 자세한 내용은 Visual Studio 설명서에서 [관리 코드 디버깅](https://go.microsoft.com/fwlink/?LinkId=120377) 을 참조 하세요.  

자세한 내용은 [공용 언어 런타임 통합 프로그래밍 개념](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md) 을 참조 하세요.  
