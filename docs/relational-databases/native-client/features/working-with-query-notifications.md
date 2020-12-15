---
title: 쿼리 알림 사용 | Microsoft Docs
description: 쿼리 알림을 사용 하면 쿼리의 기본 데이터가 SQL Server Native Client 변경 될 때 시간 제한 기간 동안 알림을 요청할 수 있습니다.
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], query notifications
- rowsets [SQL Server], notifications
- SQL Server Native Client, query notifications
- notifications [SQL Server Native Client]
- query notifications [SQL Server], SQL Server Native Client
- canceling rowset changes
- IRowsetNotify interface
- SQLNCLI, query notifications
- SQL Server Native Client OLE DB provider, query notifications
- consumer notification for rowset changes [SQL Server Native Client]
ms.assetid: 2f906fff-5ed9-4527-9fd3-9c0d27c3dff7
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6182c18b9f85b2b11a5813a11131b7a5efb3bbbd
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463364"
---
# <a name="working-with-query-notifications"></a>쿼리 알림 작업
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]

  쿼리 알림은 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 도입되었습니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 도입된 Service Broker 인프라를 기반으로 구축된 쿼리 알림을 통해 애플리케이션은 데이터 변경 시 알림을 받을 수 있습니다. 이 기능은 데이터베이스의 정보 캐시를 제공하며 원본 데이터 변경 시 알림을 받아야 하는 애플리케이션(예: 웹 애플리케이션)에 특히 유용합니다.  
  
 쿼리 알림을 사용하면 쿼리의 기본 데이터가 변경될 때 지정한 제한 시간 내에 알림을 요청할 수 있습니다. 알림 요청은 서비스 이름, 메시지 텍스트 및 제한 시간 값을 비롯한 알림 옵션을 서버에 지정합니다. 알림은 애플리케이션에서 사용 가능한 알림을 폴링할 수 있는 Service Broker 큐를 통해 배달됩니다.  
  
 쿼리 알림 옵션 문자열의 구문은 다음과 같습니다.  
  
 `service=<service-name>[;(local database=<database> | broker instance=<broker instance>)]`  
  
 다음은 그 예입니다.  
  
 `service=mySSBService;local database=mydb`  
  
 애플리케이션에서 알림 구독을 만든 다음 종료할 수 있으므로 알림 구독의 수명은 이러한 알림 구독을 시작하는 프로세스보다 깁니다. 구독은 유효한 상태로 유지되며, 구독을 만들 때 지정한 제한 시간 내에 데이터가 변경될 경우 알림이 발생합니다. 알림은 실행된 쿼리, 알림 옵션 및 메시지 텍스트로 식별되며 제한 시간 값을 0으로 설정하여 취소할 수 있습니다.  
  
 알림은 한 번만 전달됩니다. 데이터 변경을 연속해서 알리려면 각 알림이 처리된 후 쿼리를 다시 실행하여 새 구독을 만들어야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 일반적으로 네이티브 클라이언트 응용 프로그램은 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 알림 옵션에 지정 된 서비스와 연결 된 큐에서 알림을 읽도록 [receive](../../../t-sql/statements/receive-transact-sql.md) 명령을 사용 하 여 알림을 받습니다.  
  
> [!NOTE]  
>  쿼리에서 알림이 필요한 테이블 이름을 정규화해야 합니다(예: `dbo.myTable`). 두 부분으로 구성된 이름을 사용하여 테이블 이름을 정규화해야 합니다. 세 부분이나 네 부분으로 구성된 이름을 사용하면 구독이 유효하지 않습니다.  
  
 알림 인프라는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 도입된 큐 기능을 기반으로 합니다. 일반적으로 서버에서 생성된 알림은 나중에 처리하기 위해 이러한 큐를 통해 전송됩니다.  
  
 쿼리 알림을 사용하려면 서버에 큐와 서비스가 있어야 합니다. 다음과 유사한 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 사용하여 이러한 항목을 만들 수 있습니다.  
  
```  
CREATE QUEUE myQueue  
CREATE SERVICE myService ON QUEUE myQueue   
  
([https://schemas.microsoft.com/SQL/Notifications/PostQueryNotification])  
```  
  
> [!NOTE]  
>  서비스에서 위에 표시된 미리 정의된 계약 `https://schemas.microsoft.com/SQL/Notifications/PostQueryNotification`을 사용해야 합니다.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 공급자  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 행 집합 수정에 대 한 소비자 알림을 지원 합니다. 소비자는 모든 행 집합 수정 단계와 변경 시도에 대해 알림을 받습니다.  
  
> [!NOTE]  
>  **ICommand:: Execute** 를 사용 하 여 서버에 알림 쿼리를 전달 하는 것은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용 하 여 쿼리 알림을 구독 하는 유일한 유효한 방법입니다.  
  
### <a name="the-dbpropset_sqlserverrowset-property-set"></a>DBPROPSET_SQLSERVERROWSET 속성 집합  
 OLE DB를 통해 쿼리 알림을 지원 하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 DBPROPSET_SQLSERVERROWSET 속성 집합에 다음과 같은 새 속성을 추가 합니다.  
  
|Name|유형|Description|  
|----------|----------|-----------------|  
|SSPROP_QP_NOTIFICATION_TIMEOUT|VT_UI4|쿼리 알림이 활성 상태로 유지되는 시간(초)입니다.<br /><br /> 기본값은 432000초(5일)입니다. 최소값은 1초이고 최대값은 2^31-1초입니다.|  
|SSPROP_QP_NOTIFICATION_MSGTEXT|VT_BSTR|알림의 메시지 메시지입니다. 사용자가 정의하며 미리 정의된 형식은 없습니다.<br /><br /> 기본값은 빈 문자열입니다. 1-2000자를 사용하여 메시지를 지정할 수 있습니다.|  
|SSPROP_QP_NOTIFICATION_OPTIONS|VT_BSTR|쿼리 알림 옵션입니다. *이름*=*값* 구문을 사용하여 문자열에 지정됩니다. 사용자가 서비스를 만들고 큐에서 알림을 읽어야 합니다.<br /><br /> 기본값은 빈 문자열입니다.|  
  
 구독 알림은 문이 사용자 트랜잭션 또는 자동 커밋에서 실행되었는지 여부나 문이 실행된 트랜잭션이 커밋 또는 롤백되었는지 여부에 관계없이 항상 커밋됩니다. 서버 알림은 잘못된 알림 조건, 즉 기본 데이터 또는 스키마 변경이나 제한 시간에 도달한 경우 중 더 빠른 시간에 발생합니다. 알림 등록은 발생하는 즉시 삭제됩니다. 따라서 알림을 받을 때 애플리케이션에서 추가 업데이트를 가져오려는 경우 다시 구독해야 합니다.  
  
 다른 연결이나 스레드에서 알림의 대상 큐를 확인할 수 있습니다. 다음은 그 예입니다.  
  
```  
WAITFOR (RECEIVE * FROM MyQueue);   // Where MyQueue is the queue name.   
```  
  
 SELECT *는 큐에서 항목을 삭제하지 않지만 RECEIVE \* FROM은 삭제합니다. 큐가 비어 있으면 서버 스레드가 중지됩니다. 호출 시 큐 항목이 있으면 해당 항목이 즉시 반환되고, 그렇지 않으면 큐 항목이 만들어질 때까지 호출이 대기합니다.  
  
```  
RECEIVE * FROM MyQueue  
```  
  
 이 문은 큐가 비어 있을 경우 즉시 빈 결과 집합을 반환하고, 그렇지 않으면 모든 큐 알림을 반환합니다.  
  
 SSPROP_QP_NOTIFICATION_MSGTEXT 및 SSPROP_QP_NOTIFICATION_OPTIONS가 NULL이 아니고 비어 있지도 않으면 명령을 실행할 때마다 위에 정의된 3개의 속성이 포함된 쿼리 알림 TDS 헤더가 서버로 전달됩니다. 둘 중 하나가 Null이나 비어 있으면 헤더가 전달되지 않고 DB_E_ERRORSOCCURRED(또는 속성이 모두 옵션으로 표시된 경우 DB_S_ERRORSOCCURRED)가 발생하며, 상태 값이 DBPROPSTATUS_BADVALUE로 설정됩니다. 유효성 검사는 실행/준비 시 수행됩니다. 마찬가지로, [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전 연결에 대해 쿼리 알림 속성이 설정되어 있으면 DB_S_ERRORSOCCURED가 발생합니다. 이 경우 상태 값은 DBPROPSTATUS_NOTSUPPORTED입니다.  
  
 구독을 시작한다고 해서 반드시 후속 메시지가 성공적으로 배달되는 것은 아닙니다. 또한 지정된 서비스 이름의 유효성이 검사되지 않습니다.  
  
> [!NOTE]  
>  문을 준비할 때는 구독이 시작되지 않습니다. 문을 실행해야 구독이 시작되며 쿼리 알림은 OLE DB 핵심 서비스 사용의 영향을 받지 않습니다.  
  
 DBPROPSET_SQLSERVERROWSET 속성 집합에 대 한 자세한 내용은 [행 집합 속성 및 동작](../../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)을 참조 하세요.  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 드라이버  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 [SQLGetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) 및 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 함수에 세 개의 새 특성을 추가 하 여 쿼리 알림을 지원 합니다.  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT  
  
 SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT 및 SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS가 NULL이 아니면 명령을 실행할 때마다 위에 정의된 3개의 특성이 포함된 쿼리 알림 TDS 헤더가 서버로 전달됩니다. 둘 중 하나가 Null이면 헤더가 전달되지 않고 SQL_SUCCESS_WITH_INFO가 반환됩니다. 유효성 검사는 [Sqlprepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md), **Sqlexecdirect** 및 **sqlprepare** 에서 수행 되며, 특성이 유효 하지 않으면 모두 실패 합니다. 마찬가지로, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 버전에 대해 이러한 쿼리 알림 특성이 설정되어 있으면 SQL_SUCCESS_WITH_INFO로 인해 실행이 실패합니다.  
  
> [!NOTE]  
>  문을 준비할 때는 구독이 시작되지 않습니다. 문을 실행해야 구독을 시작할 수 있습니다.  
  
## <a name="special-cases-and-restrictions"></a>특수 상황과 제한  
 알림에서 다음 데이터 형식은 지원되지 않습니다.  
  
-   **text**  
  
-   **ntext**  
  
-   **image**  
  
 이러한 유형을 반환하는 쿼리에 대해 알림 요청이 수행되면 알림 구독을 사용할 수 없음을 지정하는 알림이 즉시 발생합니다.  
  
 일괄 처리 및 저장 프로시저에 대해 구독을 요청하면 일괄 처리 또는 저장 프로시저 내에서 실행되는 각 문에 대해 별도의 구독 요청이 수행됩니다. EXECUTE 문은 알림을 등록하지 않고 알림 요청을 실행된 명령으로 보냅니다. 일괄 처리인 경우 컨텍스트가 실행된 문에 적용되고 위에서 설명한 것과 같은 규칙이 적용됩니다.  
  
 동일한 데이터베이스 컨텍스트에서 동일한 사용자가 제출한 알림에 대 한 쿼리를 제출 하 고 동일한 템플릿, 동일한 매개 변수 값, 동일한 알림 ID 및 기존 활성 구독의 배달 위치를 모두 포함 하는 알림은 기존 구독을 갱신 하 고 지정 된 새 시간 제한 값을 다시 설정 합니다. 즉, 동일한 쿼리에 대해 알림을 요청 하면 하나의 알림만 전송 됩니다. 이는 일괄 처리에서 중복된 쿼리나 여러 번 호출된 저장 프로시저의 쿼리에 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 기능](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
