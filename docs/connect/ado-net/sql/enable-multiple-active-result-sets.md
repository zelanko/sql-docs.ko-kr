---
title: MARS(Multiple Active Result Sets) 사용
description: SQL Server에서 MARS를 사용하는 방법을 설명합니다.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 576079e4-debe-4ab5-9204-fcbe2ca7a5e2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d0c40df5ec7648b7073f9efa369428b8d88f6d11
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452223"
---
# <a name="enabling-multiple-active-result-sets"></a>MARS(Multiple Active Result Sets) 사용

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

MARS(Multiple Active Result Sets)는 단일 연결에서 여러 배치를 실행할 수 있도록 하는 SQL Server의 기능입니다. SQL Server에 MARS가 활성화되어 있으면 명령 개체를 사용할 때마다 연결에 세션이 추가됩니다.  
  
> [!NOTE]
>  단일 MARS 세션에서 MARS가 사용할 하나의 논리적 연결을 열고 각 활성 명령에 대해 하나의 논리적 연결을 엽니다.  
  
## <a name="enabling-and-disabling-mars-in-the-connection-string"></a>연결 문자열에서 MARS 사용 및 사용 안 함  
  
> [!NOTE]
>  다음 연결 문자열에서는 SQL Server에 포함된 샘플 **AdventureWorks** 데이터베이스를 사용합니다. 제공 된 연결 문자열은 데이터베이스가 MSSQL1 라는 서버에 설치 되어 있다고 가정 합니다. 사용자 환경에 필요한 경우 연결 문자열을 수정 합니다.  
  
MARS 기능은 기본적으로 해제되어 있습니다. 연결 문자열에 "MultipleActiveResultSets = True" 키워드 쌍을 추가 하 여 사용할 수 있습니다. MARS를 활성화하는 유일한 유효 값은 "True"입니다. 다음 예에서는 SQL Server 인스턴스에 연결 하는 방법과 MARS를 사용 하도록 지정 하는 방법을 보여 줍니다. 
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=True";  
```  
  
연결 문자열에 "MultipleActiveResultSets = False" 키워드 쌍을 추가 하 여 MARS를 사용 하지 않도록 설정할 수 있습니다. MARS를 비활성화하는 유일한 유효 값은 "False"입니다. 다음 연결 문자열에서는 MARS를 사용 하지 않도록 설정 하는 방법을 보여 줍니다.  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=False";  
```  
  
## <a name="special-considerations-when-using-mars"></a>MARS를 사용할 때 특별히 고려할 사항  
일반적으로 기존 응용 프로그램은 MARS 사용 연결을 사용 하기 위해 수정할 필요가 없습니다. 그러나 응용 프로그램에서 MARS 기능을 사용 하려는 경우 다음과 같은 특별 한 고려 사항을 이해 해야 합니다.  
  
### <a name="statement-interleaving"></a>문 인터리빙  
MARS 작업은 서버에서 동기적으로 실행 됩니다. SELECT 및 BULK INSERT 문의 문 인터리빙이 허용 됩니다. 그러나 DML (데이터 조작 언어) 및 DDL (데이터 정의 언어) 문은 원자적으로 실행 됩니다. 원자성 일괄 처리가 실행 되는 동안 실행 하려는 모든 문은 차단 됩니다. 서버에서의 병렬 실행은 MARS 기능이 아닙니다.  
  
MARS 연결에서 두 개의 일괄 처리를 제출 하는 경우 하나는 SELECT 문을 포함 하 고 다른 하나는 DML 문을 포함 하는 경우 DML은 SELECT 문을 실행 하는 동안 실행을 시작할 수 있습니다. 그러나 SELECT 문이 진행 되기 전에 DML 문을 실행 하 여 완료 해야 합니다. 두 문이 동일한 트랜잭션에서 실행 되는 경우 SELECT 문 실행이 시작 된 후 DML 문에의 한 변경 내용은 읽기 작업에 표시 되지 않습니다.  
  
SELECT 문 내부의 WAITFOR 문은 첫 번째 행이 생성 될 때까지 대기 하는 동안 트랜잭션을 생성 하지 않습니다. 이는 WAITFOR 문이 대기 중인 동안 동일한 연결 내에서 다른 일괄 처리를 실행할 수 없음을 의미 합니다.  
  
### <a name="mars-session-cache"></a>MARS 세션 캐시  
MARS가 활성화 된 상태에서 연결이 열리면 논리 세션이 만들어지고 오버 헤드가 추가 됩니다. 오버헤드를 최소화하고 성능을 높이기 위해 **SqlClient**가 연결 내에서 MARS 세션을 캐시합니다. 캐시에는 최대 10 개의 MARS 세션이 있습니다. 이 값은 사용자가 조정할 수 없습니다. 세션 제한에 도달하면 새 세션이 만들어지며, 이때 오류는 생성되지 않습니다. 캐시와 여기에 포함 된 세션은 연결당입니다. 연결 간에 공유 되지 않습니다. 세션을 해제 하면 풀의 상한에 도달 하지 않으면 풀로 반환 됩니다. 캐시 풀이 꽉 차면 세션이 닫힙니다. MARS 세션은 만료 되지 않습니다. 연결 개체가 삭제 될 때만 정리 됩니다. MARS 세션 캐시는 미리 로드 되지 않습니다. 응용 프로그램에 더 많은 세션이 필요할 때 로드 됩니다.  
  
### <a name="thread-safety"></a>스레드 보안  
MARS 작업은 스레드로부터 안전 하지 않습니다.  
  
### <a name="connection-pooling"></a>연결 풀링  
MARS 사용 연결은 다른 연결과 마찬가지로 풀링되지 않습니다. 응용 프로그램에서 MARS를 사용 하는 두 개의 연결 및 mars를 사용 하지 않도록 설정 된 연결을 여는 경우 두 연결은 별도의 풀에 있습니다.
  
### <a name="sql-server-batch-execution-environment"></a>일괄 처리 실행 환경 SQL Server  
연결이 열리면 기본 환경이 정의 됩니다. 그런 다음이 환경은 논리적 MARS 세션에 복사 됩니다.  
  
일괄 처리 실행 환경에는 다음 구성 요소가 포함 됩니다.  
  
- Set 옵션 (예: ANSI_NULLS, DATE_FORMAT, LANGUAGE, TEXTSIZE)  
  
- 보안 컨텍스트 (사용자/응용 프로그램 역할)  
  
- 데이터베이스 컨텍스트 (현재 데이터베이스)  
  
- 실행 상태 변수 (예: @ @ERROR, @ @ROWCOUNT, @ @FETCH_STATUS @ @IDENTITY)  
  
- 최상위 임시 테이블  
  
MARS를 사용 하면 기본 실행 환경이 연결에 연결 됩니다. 특정 연결에서 실행을 시작하는 각각의 새 일괄 처리는 기본 환경의 복사본을 받습니다. 지정 된 일괄 처리에서 코드가 실행 될 때마다 해당 환경에 대 한 모든 변경 사항은 특정 일괄 처리로 범위가 지정 됩니다. 실행이 완료되면 실행 설정이 기본 환경에 복사됩니다. 동일한 트랜잭션에서 순차적으로 실행 되는 여러 명령을 실행 하는 단일 일괄 처리의 경우 의미 체계는 이전 클라이언트 또는 서버와 관련 된 연결에서 노출 하는 것과 동일 합니다.  
  
### <a name="parallel-execution"></a>병렬 실행  
MARS는 응용 프로그램의 여러 연결에 대 한 모든 요구 사항을 제거 하도록 설계 되지 않았습니다. 응용 프로그램에서 서버에 대 한 명령의 진정한 병렬 실행이 필요한 경우 여러 연결을 사용 해야 합니다.  
  
예를 들어 다음의 시나리오를 고려해보세요. 결과 집합을 처리 하 고 데이터를 업데이트 하기 위한 두 개의 명령 개체가 생성 됩니다. MARS를 통해 공통 연결을 공유 합니다. 시나리오 내용: `Transaction` `Commit` 첫 번째 명령 개체에서 모든 결과를 읽을 때까지 업데이트를 수행하지 못하므로 다음과 같은 예외가 발생합니다.  
  
메시지: 다른 세션에서 트랜잭션 컨텍스트를 사용 중입니다.  
  
원본: Microsoft SqlClient Data Provider  
  
예상: (null)  
  
수신: SqlException  
  
이 시나리오를 처리 하는 세 가지 옵션이 있습니다.  
  
- 트랜잭션이 트랜잭션에 포함 되지 않도록 판독기를 만든 후 트랜잭션을 시작 합니다. 그러면 모든 업데이트가 자체 트랜잭션이 됩니다.  
  
- 판독기를 닫은 후 모든 작업을 커밋합니다. 이렇게 하면 대량의 업데이트를 처리할 가능성이 있습니다.  
  
- MARS를 사용 하지 않습니다. MARS 이전 처럼 각 명령 개체에 대해 별도의 연결을 사용 합니다.  
  
### <a name="detecting-mars-support"></a>MARS 지원 검색  
응용 프로그램은 `SqlConnection.ServerVersion` 값을 읽어 MARS 지원을 확인할 수 있습니다. 주 번호는 SQL Server 2005의 경우 9, SQL Server 2008의 경우 10입니다.  
  
## <a name="next-steps"></a>다음 단계
- [MARS(Multiple Active Result Sets)](multiple-active-result-sets-mars.md)
