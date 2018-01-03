---
title: "작업 관리 작업"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/12/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.openlocfilehash: 70f70c504aab81f490ee39d244555022bf73d91b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="workload-management-tasks"></a>작업 관리 작업

## <a name="view-login-members-of-each-resource-class"></a>각 리소스 클래스의 로그인 멤버 보기
SQL Server PDW에서 각 리소스 클래스 서버 역할의 로그인 멤버를 표시 하는 방법에 설명 합니다. 이 쿼리를 사용 하 여 각 로그인에 의해 제출 된 요청에 허용 되는 리소스의 클래스를 파악 합니다.  
  
리소스 클래스 설명에 대 한 참조 [작업 관리](workload-management.md)합니다.  
  
이 쿼리는 각 리소스 클래스에 대 한 구성원 목록을 표시합니다. 리소스 클래스, mediumrc, largerc, 및 xlargerc 세 가지가 있습니다.  
  
```sql  
SELECT l.name AS [member], r.name AS [server role]  
FROM sys.server_role_members AS rm  
JOIN sys.server_principals AS l  
  ON l.principal_id = rm.member_principal_id  
JOIN  
  sys.server_principals AS r  
  ON r.principal_id = rm.role_principal_id  
WHERE  
  ( l.[type] = 'S' OR l.[type] = 'U' OR l.[type] = 'G' )  
  AND r.[type] = 'R'  
  AND r.[name] in ('mediumrc', 'largerc', 'xlargerc');  
```  
  
로그인이이 목록에 없는 경우 해당 요청에는 기본 리소스 받게 됩니다. 둘 이상의 리소스 클래스의 멤버인 로그인을 사용 하는 경우 가장 큰 클래스 우선 순위가 있습니다.  
  
리소스 할당에 나열 된는 [작업 관리](workload-management.md) 항목입니다.  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>변경 요청에 할당 된 시스템 리소스
리소스를 파악 하는 방법을 설명 합니다. SQL Server PDW 요청이 실행 되는 클래스 및 해당 요청에 대 한 시스템 리소스를 변경 하는 방법입니다. 요청을 사용 하 여 요청을 제출 하는 로그인의 리소스 클래스 멤버 자격을 변경 해야에 대 한 리소스를 변경는 [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) 문.  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>1 단계: 요청을 실행 하는 로그인에 대 한 리소스 클래스를 확인 합니다.  
이 쿼리는 리소스 클래스 서버 역할 멤버 자격의 구성원 인 로그인을 표시 합니다. 세 가지 리소스 클래스는 **mediumrc**, **largerc**, 및 **xlargerc**합니다.  
  
> [!IMPORTANT]  
> 이 쿼리를 실행 하 여 로그인을 해야 **제어 서버** 권한. 로그인 하지 않고 실행 하면 **제어 서버** 권한,이 쿼리는 현재 로그인에 대 한 역할 멤버 자격만 반환 합니다.  
  
```sql  
SELECT l.name AS [member], r.name AS [server role]  
FROM sys.server_role_members AS rm  
JOIN sys.server_principals AS l  
  ON l.principal_id = rm.member_principal_id  
JOIN  
  sys.server_principals AS r  
  ON r.principal_id = rm.role_principal_id  
WHERE  
  l.[type] = 'S'   
  AND r.[type] = 'R'  
  AND r.[name] in ('mediumrc', 'largerc', 'xlargerc');  
GO  
```  
  
리소스 클래스 서버 역할의 멤버인 로그인이 없습니다가 없을 경우 결과 테이블은 비어 있게 됩니다. 이 경우 쿼리에서 Ching 이라는 로그인을 반환 하는 경우 다음 Ching는 요청을 제출 하는 경우 요청이 받습니다 기본 시스템 리소스를 리소스 클래스 시스템 리소스 보다 작은. 둘 이상의 리소스 클래스의 멤버인 로그인을 사용 하는 경우 가장 큰 클래스 우선 순위가 있습니다.  
  
목록이 각 리소스 클래스에 대 한 리소스 할당에 대 한 참조 [작업 관리](workload-management.md) 항목입니다.  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>다른 리소스 클래스 멤버는 로그인 요청을 실행 하는 2 단계:  
더 크거나 작게 시스템 리소스 중 하나를 사용 하 여 요청을 실행 하는 두 가지 있습니다.  
  
-   더 크거나 작게 리소스 클래스의 구성원 인 다른 로그인에서 요청을 실행 합니다.  
  
-   리소스 클래스 역할 중 하나에 필요한 로그인을 추가 합니다. 를 주의 해 서이 옵션을 선택 로그인에 대 한 리소스 클래스를 변경 하면 로그인에서 제출 된 모든 요청에 대 한 시스템 리소스 수준을 변경 됩니다.  
  
Ching largerc 서버 역할의 멤버인 가정 합니다. 다음 예에서는 로그인 Ching xlargerc 서버 역할에 추가 하는 방법을 보여 줍니다.  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
Ching는 largerc 및 xlargerc 서버 역할의 멤버인 되었습니다. Ching가 요청을 제출 된 요청 xlargerc 시스템 리소스를 받게 됩니다.  
  
다음 예제에서는 Ching mediumrc 서버 역할에 다시 이동합니다.  이 위해 그녀 여야 xlargerc, 및 largerc 서버 역할에서 제거 하며 mediumrc 서버 역할에 추가 합니다.  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
Ching은 mediumrc 서버 역할의 구성원이 됩니다.  다음 예에서는 Ching 그녀의 요청에 대 한 기본 시스템 리소스를 포함할 수를 변경 합니다.  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
리소스 클래스에 대 한 역할 멤버 자격을 변경 하는 방법에 대 한 자세한 내용은 참조 [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)합니다.  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>해당 요청에 대 한 기본 시스템 리소스에 로그인을 변경 합니다.
기본 금액에 대 한 SQL Server PDW 로그인에 할당 된 시스템 리소스 할당을 변경 하는 방법에 설명 합니다. 이 SQL Server PDW 로그인에서 제출 된 요청에 할당 된 시스템 리소스를 영향을 줍니다.  
  
리소스 클래스 설명에 대 한 참조 [작업 관리](workload-management.md)  
  
리소스 클래스 서버 역할의 멤버인 로그인 없는 경우 로그인 하 여 제출 된 요청 기본 양을 시스템 리소스를 받습니다.  
  
Matt 현재 리소스는 모든 클래스 서버 역할의 멤버 이므로 다시를 지정 하는 기본 리소스를 수신 하는 그의 요청으로 되돌리려면 원하는 로그인을 가정 합니다.  다음 예제에서는 세 가지 리소스는 모든 클래스 서버 역할에서 구성원을 삭제 하 여 Matt의 요청에 기본 리소스를 할당 합니다.  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>동시성 슬롯 개수는 데 필요한 대기 중에 대 한 요청 표시
동시성 SQL Server PDW에서를 실행 하려고 대기 하는 요청에 필요한 슬롯 수를 파악 하는 방법에 설명 합니다.  
  
자세한 내용은 참조 [작업 관리](workload-management.md)합니다.  
  
너무 오래 실행 없이 요청을 기다리고 있을 수 없습니다. 이 문제를 해결 하는 방법 중 하나를 요구 하는 동시성 슬롯 수를 살펴보는입니다.  다음 예제에서는 각 대기 중인 요청에 필요한 동시성 슬롯 수를 보여 줍니다.  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>관련 항목:  
[작업 관리](workload-management.md)  
  
