---
title: 쿼리 알림 작업 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버에서 쿼리 알림 작업
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], query notifications
- rowsets [SQL Server], notifications
- OLE DB Driver for SQL Server, query notifications
- notifications [OLE DB Driver for SQL Server]
- query notifications [SQL Server], OLE DB Driver for SQL Server
- canceling rowset changes
- IRowsetNotify interface
- MSOLEDBSQL, query notifications
- OLE DB Driver for SQL Server, query notifications
- consumer notification for rowset changes [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 8fb1e0ffcacad7b4b3733b3009df3909ac0aef89
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39109175"
---
# <a name="working-with-query-notifications"></a>쿼리 알림 작업
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  에 도입 된 쿼리 알림 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 및 OLE DB Driver for SQL Server입니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 도입된 Service Broker 인프라를 기반으로 구축된 쿼리 알림을 통해 응용 프로그램은 데이터 변경 시 알림을 받을 수 있습니다. 이 기능은 데이터베이스의 정보 캐시를 제공하며 원본 데이터 변경 시 알림을 받아야 하는 응용 프로그램(예: 웹 응용 프로그램)에 특히 유용합니다.  
  
 쿼리 알림을 사용하면 쿼리의 기본 데이터가 변경될 때 지정한 제한 시간 내에 알림을 요청할 수 있습니다. 알림 요청은 서비스 이름, 메시지 텍스트 및 제한 시간 값을 비롯한 알림 옵션을 서버에 지정합니다. 알림은 응용 프로그램에서 사용 가능한 알림을 폴링할 수 있는 Service Broker 큐를 통해 배달됩니다.  
  
 쿼리 알림 옵션 문자열의 구문은 다음과 같습니다.  
  
 `service=<service-name>[;(local database=<database> | broker instance=<broker instance>)]`  
  
 예를 들어 다음과 같이 사용할 수 있습니다.  
  
 `service=mySSBService;local database=mydb`  
  
 응용 프로그램에서 알림 구독을 만든 다음 종료할 수 있으므로 알림 구독의 수명은 이러한 알림 구독을 시작하는 프로세스보다 깁니다. 구독은 유효한 상태로 유지되며, 구독을 만들 때 지정한 제한 시간 내에 데이터가 변경될 경우 알림이 발생합니다. 알림은 실행된 쿼리, 알림 옵션 및 메시지 텍스트로 식별되며 제한 시간 값을 0으로 설정하여 취소할 수 있습니다.  
  
 알림은 한 번만 전달됩니다. 데이터 변경을 연속해서 알리려면 각 알림이 처리된 후 쿼리를 다시 실행하여 새 구독을 만들어야 합니다.  
  
 일반적으로 OLE DB Driver for SQL Server 응용 프로그램은 알림을 받을 때 [!INCLUDE[tsql](../../../includes/tsql-md.md)] [RECEIVE](../../../t-sql/statements/receive-transact-sql.md) 명령을 사용하여 알림 옵션에 지정된 서비스와 연결된 큐에서 알림을 읽습니다.  
  
> [!NOTE]  
>  쿼리에서 알림이 필요한 테이블 이름을 정규화해야 합니다(예: `dbo.myTable`). 두 부분으로 구성된 이름을 사용하여 테이블 이름을 정규화해야 합니다. 세 부분이나 네 부분으로 구성된 이름을 사용하면 구독이 유효하지 않습니다.  
  
 알림 인프라는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서 도입된 큐 기능을 기반으로 합니다. 일반적으로 서버에서 생성된 알림은 나중에 처리하기 위해 이러한 큐를 통해 전송됩니다.  
  
 쿼리 알림을 사용하려면 서버에 큐와 서비스가 있어야 합니다. 다음과 유사한 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 사용하여 이러한 항목을 만들 수 있습니다.  
  
```  
CREATE QUEUE myQueue  
CREATE SERVICE myService ON QUEUE myQueue   
  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification])  
```  
  
> [!NOTE]  
>  서비스에서 위에 표시된 미리 정의된 계약을 사용해야 합니다.  
  
## <a name="ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버  
 OLE DB Driver for SQL Server 행 집합 수정에 소비자 알림을 지원합니다. 소비자는 모든 행 집합 수정 단계와 변경 시도에 대해 알림을 받습니다.  
  
> [!NOTE]  
>  **ICommand::Execute**를 사용하여 알림 쿼리를 서버로 전달해야만 SQL Server OLE DB 드라이버에서 쿼리 알림을 구독할 수 있습니다.  
  
### <a name="the-dbpropsetsqlserverrowset-property-set"></a>DBPROPSET_SQLSERVERROWSET 속성 집합  
 OLE DB를 통해 쿼리 알림을 지원하기 위해 SQL Server OLE DB 드라이버에서는 DBPROPSET_SQLSERVERROWSET 속성 집합에 다음과 같은 새 속성을 추가합니다.  
  
|속성|형식|설명|  
|----------|----------|-----------------|  
|SSPROP_QP_NOTIFICATION_TIMEOUT|VT_UI4|쿼리 알림이 활성 상태로 유지되는 시간(초)입니다.<br /><br /> 기본값은 432,000초(5일)입니다. 최소값은 1초이고 최대값은 2^31-1초입니다.|  
|SSPROP_QP_NOTIFICATION_MSGTEXT|VT_BSTR|알림의 메시지 메시지입니다. 사용자가 정의하며 미리 정의된 형식은 없습니다.<br /><br /> 기본값은 빈 문자열입니다. 1-2000자를 사용하여 메시지를 지정할 수 있습니다.|  
|SSPROP_QP_NOTIFICATION_OPTIONS|VT_BSTR|쿼리 알림 옵션입니다. *이름*=*값* 구문을 사용하여 문자열에 지정됩니다. 사용자가 서비스를 만들고 큐에서 알림을 읽어야 합니다.<br /><br /> 기본값은 빈 문자열입니다.|  
  
 구독 알림은 문이 사용자 트랜잭션 또는 자동 커밋에서 실행되었는지 여부나 문이 실행된 트랜잭션이 커밋 또는 롤백되었는지 여부에 관계없이 항상 커밋됩니다. 서버 알림은 잘못된 알림 조건, 즉 기본 데이터 또는 스키마 변경이나 제한 시간에 도달한 경우 중 더 빠른 시간에 발생합니다. 알림 등록은 발생하는 즉시 삭제됩니다. 따라서 알림을 받을 때 응용 프로그램에서 추가 업데이트를 가져오려는 경우 다시 구독해야 합니다.  
  
 다른 연결이나 스레드에서 알림의 대상 큐를 확인할 수 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
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
  
 DBPROPSET_SQLSERVERROWSET 속성 집합에 대 한 자세한 내용은 참조 하세요. [행 집합 속성 및 동작](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)합니다.  
  

  
## <a name="see-also"></a>참고 항목  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)     
  
  
