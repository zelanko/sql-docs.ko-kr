---
title: 쿼리 알림 사용
description: 쿼리 알림을 사용 하도록 설정 하 고 사용 하기 위한 요구 사항을 포함 하 여 쿼리 알림을 사용 하는 방법을 설명 합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: a5333e19-8e55-4aa9-82dc-ca8745e516ed
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 94b472a1fe040aa3a684d9f7b523ba09c82a651e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452237"
---
# <a name="enabling-query-notifications"></a>쿼리 알림 사용

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

쿼리 알림을 사용 하는 응용 프로그램에는 일반적인 요구 사항 집합이 있습니다. SQL 쿼리 알림을 지원하도록 데이터 원본을 올바르게 구성해야 하며, 사용자는 올바른 클라이언트측 및 서버측 권한을 가지고 있어야 합니다.  
  
쿼리 알림을 사용 하려면 다음을 수행 해야 합니다.  
  
- 데이터베이스에 대해 쿼리 알림을 사용 하도록 설정 합니다.  
  
- 데이터베이스에 연결 하는 데 사용 되는 사용자 ID에 필요한 사용 권한이 있는지 확인 합니다.  
  
- <xref:Microsoft.Data.SqlClient.SqlCommand> 개체를 사용하여 <xref:Microsoft.Data.SqlClient.SqlDependency> 또는 <xref:Microsoft.Data.Sql.SqlNotificationRequest> 같은 관련된 알림 개체로 올바른 SELECT 문을 실행합니다.  
  
- 모니터링 되는 데이터가 변경 될 경우 알림을 처리 하는 코드를 제공 합니다.  
  
## <a name="query-notifications-requirements"></a>쿼리 알림 요구 사항  
쿼리 알림은 특정 요구 사항 목록을 충족 하는 SELECT 문에 대해서만 지원 됩니다. 다음 표에서는 SQL Server 온라인 설명서 Service Broker 및 쿼리 알림 설명서에 대 한 링크를 제공 합니다.  
  
**SQL Server 설명서**  
  
- [알림에 대한 쿼리 만들기](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [Service Broker에 대한 보안 고려 사항](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166059(v=sql.90))  
  
- [보안 및 보호(Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522911(v=sql.105))  
  
- [Notifications Services에 대한 보안 고려 사항](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms172604(v=sql.90))  
  
- [쿼리 알림 사용 권한](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms188311(v=sql.105))  
  
- [Service Broker에 대한 국가별 고려 사항](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms166028(v=sql.90))  
  
- [솔루션 디자인 고려 사항(Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522899(v=sql.105))  
  
- [Service Broker 개발자 정보 센터](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [개발자 가이드(Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="enabling-query-notifications-to-run-sample-code"></a>쿼리 알림을 사용 하 여 샘플 코드 실행  
SQL Server Management Studio를 사용하여 **AdventureWorks** 데이터베이스에 대해 Service Broker를 활성화하려면 다음 Transact-SQL 문을 실행합니다.  
  
`ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
쿼리 알림 샘플이 올바르게 실행 되려면 데이터베이스 서버에서 다음 Transact-sql 문을 실행 해야 합니다.  
  
```sql
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## <a name="query-notifications-permissions"></a>쿼리 알림 사용 권한  
알림을 요청 하는 명령을 실행 하는 사용자에 게는 서버에 대 한 구독 쿼리 알림 데이터베이스 권한이 있어야 합니다.  
  
부분 신뢰 상황에서 실행 되는 클라이언트 쪽 코드에는 <xref:Microsoft.Data.SqlClient.SqlClientPermission> 필요 합니다.  
  
다음 코드는 <xref:Microsoft.Data.SqlClient.SqlClientPermission> 개체를 만들고 <xref:System.Security.Permissions.PermissionState>를 <xref:System.Security.Permissions.PermissionState.Unrestricted>로 설정 합니다. 호출 스택의 상위 호출자에 게 권한이 부여 되지 않은 경우 <xref:System.Security.CodeAccessPermission.Demand%2A>는 런타임에 <xref:System.Security.SecurityException>를 강제 적용 합니다.  
  
[!code-csharp[DataWorks SqlClientPermission_Demand#1](~/../sqlclient/doc/samples/SqlClientPermission_Demand.cs#1)]
  
## <a name="choosing-a-notification-object"></a>알림 개체 선택  
쿼리 알림 API에서는 알림을 처리하기 위한 두 개의 개체인 <xref:Microsoft.Data.SqlClient.SqlDependency> 및 <xref:Microsoft.Data.Sql.SqlNotificationRequest>입니다.
  
### <a name="using-sqldependency"></a>SqlDependency 사용  
<xref:Microsoft.Data.SqlClient.SqlDependency>를 사용하려면 사용 중인 SQL Server 데이터베이스에 대해 Service Broker를 활성화해야 하며 사용자는 알림을 수신할 수 있는 권한이 있어야 합니다. 알림 큐와 같은 Service Broker 개체는 미리 정의 되어 있습니다.  
  
또한 <xref:Microsoft.Data.SqlClient.SqlDependency>는 작업자 스레드를 자동으로 실행 하 여 큐에 게시 될 때 알림을 처리 합니다. 또한 Service Broker 메시지를 구문 분석 하 여 정보를 이벤트 인수 데이터로 노출 합니다. `Start` 메서드를 호출 하 여 데이터베이스에 대 한 종속성을 설정 하 여 <xref:Microsoft.Data.SqlClient.SqlDependency>을 초기화 해야 합니다. 이 메서드는 필요한 각 데이터베이스 연결에 대해 응용 프로그램을 초기화 하는 동안 한 번만 호출 해야 하는 정적 메서드입니다. 만들어진 각 종속성 연결에 대해 애플리케이션이 종료될 때 `Stop` 메서드를 호출해야 합니다.  
  
### <a name="using-sqlnotificationrequest"></a>SqlNotificationRequest 사용  
반면 <xref:Microsoft.Data.Sql.SqlNotificationRequest>에서는 전체 수신 인프라를 직접 구현 해야 합니다. 또한 큐, 서비스 및 큐에서 지 원하는 메시지 유형과 같은 모든 지원 Service Broker 개체를 정의 해야 합니다. 이 수동 접근 방식은 응용 프로그램에 특별 한 알림 메시지나 알림 동작이 필요 하거나 응용 프로그램이 대규모 Service Broker 응용 프로그램의 일부인 경우에 유용 합니다.  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server의 쿼리 알림](query-notifications-sql-server.md)
