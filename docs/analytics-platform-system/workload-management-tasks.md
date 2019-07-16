---
title: 워크 로드 관리 작업-Analytics Platform System | Microsoft Docs
description: Analytics Platform System의 워크 로드 관리 작업입니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ea6b3785914781e73a8570c1282741f7c4b56298
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959752"
---
# <a name="workload-management-tasks-in-analytics-platform-system"></a>분석 플랫폼 시스템에 워크 로드 관리 작업
Analytics Platform System의 워크 로드 관리 작업입니다.

## <a name="view-login-members-of-each-resource-class"></a>각 리소스 클래스의 로그인 멤버 보기
SQL Server PDW에서 각 리소스 클래스 서버 역할의 로그인 멤버를 표시 하는 방법에 설명 합니다. 이 쿼리를 사용 하 여 각 로그인에 의해 전송 된 요청만 허용 하는 리소스 클래스를 파악 합니다.  
  
리소스 클래스 설명을 보려면 [워크 로드 관리](workload-management.md)합니다.  
  
이 쿼리는 각 리소스 클래스에 대 한 멤버 자격 목록이 표시 됩니다. 세 가지 리소스 클래스, mediumrc, largerc 및 xlargerc 있습니다.  
  
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
  
로그인이이 목록에 없는 경우 해당 요청에는 기본 리소스를 받게 됩니다. 둘 이상의 리소스 클래스의 멤버인 로그인을 사용 하는 경우 가장 큰 클래스 우선 순위를 가집니다.  
  
리소스 할당에 나와 [워크 로드 관리](workload-management.md)합니다.  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>변경 요청에 할당 된 시스템 리소스
리소스를 파악 하는 방법에 설명 합니다. SQL Server PDW 요청 중인 클래스 차례로 해당 요청에 대 한 시스템 리소스를 변경 하는 방법입니다. 리소스 변경 요청을 사용 하 여 요청을 제출 하는 로그인의 리소스 클래스 멤버 자격을 변경 해야 합니다 [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) 문입니다.  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>1단계: 요청을 실행 하는 로그인에 대 한 리소스 클래스를 결정 합니다.  
이 쿼리는 리소스 클래스 서버 역할 멤버 자격의 멤버인 로그인을 표시 합니다. 세 가지 리소스 클래스를 **mediumrc**하십시오 **largerc**, 및 **xlargerc**합니다.  
  
> [!IMPORTANT]  
> 로그인 하 여이 쿼리를 실행 해야 합니다 **CONTROL SERVER** 권한. 로그인 하지 않고 실행 하는 경우 **CONTROL SERVER** 권한이이 쿼리는 현재 로그인의 역할 멤버 자격만 반환 합니다.  
  
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
  
리소스 클래스 서버 역할의 멤버인 로그인이 더 있으면 결과 테이블은 비어 있게 됩니다. 이 경우 쿼리에서 Ching 이라는 로그인을 반환 하는 경우 다음 Ching 요청을 제출 하는 경우 요청 받을 리소스 클래스 시스템 리소스를 보다 작은 기본 시스템 리소스를 합니다. 둘 이상의 리소스 클래스의 멤버인 로그인을 사용 하는 경우 가장 큰 클래스 우선 순위를 가집니다.  
  
각 리소스 클래스에 대 한 리소스 할당의 목록을 참조 하세요 [워크 로드 관리](workload-management.md)합니다.  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>2단계: 다른 리소스 클래스 멤버 자격을 사용 하 여 로그인에서 요청을 실행 합니다.  
두 가지 방법으로 더 크거나 더 작은 시스템 리소스 중 하나를 사용 하 여 요청을 실행 하려면:  
  
-   더 크거나 더 작은 리소스 클래스의 구성원 인 다른 로그인에서 요청을 실행 합니다.  
  
-   리소스 클래스 역할 중 하나에 필요한 로그인을 추가 합니다. 주의 사용 하 여이 옵션을 선택 로그인에 대 한 리소스 클래스를 변경 하면 로그인 하 여 제출 된 모든 요청에 대 한 시스템 리소스 수준을 변경 됩니다.  
  
Ching largerc 서버 역할의 멤버인 가정 합니다. 다음 예에서는 로그인 Ching xlargerc 서버 역할을 추가 하는 방법을 보여 줍니다.  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
Ching는 largerc 및 xlargerc 서버 역할의 멤버인 되었습니다. Ching가 요청을 제출 하면 요청이 xlargerc 시스템 리소스를 받게 됩니다.  
  
다음 예제에서는 Ching mediumrc 서버 역할에 다시 이동합니다.  새 역할을 변경 하려면 로그인 해야에서 제거 xlargerc 및 largerc 서버 역할을 하 고 mediumrc 서버 역할에 추가 합니다.  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
Ching은 mediumrc 서버 역할의 멤버인 되었습니다.  다음 예제에서는 요청에 대 한 기본 시스템 리소스가 있어야 Ching를 변경 합니다.  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
리소스 클래스에 대 한 역할 멤버 자격을 변경 하는 방법에 대 한 자세한 내용은 참조 하세요. [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)합니다.  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>해당 요청에 대 한 기본 시스템 리소스에는 로그인을 변경 합니다.
SQL Server PDW 로그인을 기본 용량에 할당 된 시스템 리소스 할당을 변경 하는 방법에 설명 합니다. 
  
리소스 클래스 설명을 보려면 [워크 로드 관리](workload-management.md)  
  
리소스 클래스 서버 역할의 멤버인 로그인 없는 경우 로그인 하 여 제출 된 요청이 시스템 리소스의 기본 크기를 받습니다.  
  
Matt는 현재 모든 리소스 클래스 서버 역할의 멤버 및 기본 리소스에만 수신 요청에 다시 되돌리려는 로그인을 가정 합니다.  다음 예제에서는 모든 세 가지 리소스 클래스 서버 역할의 구성원 자격을 삭제 하 여 Matt의 요청에 기본 리소스를 할당 합니다.  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>동시성 슬롯 수가 필요한 대기 중에 대 한 요청 표시
동시성 슬롯 SQL Server PDW에서 실행 되기를 기다리고 있는 요청에 필요한 수를 파악 하는 방법에 설명 합니다.  
  
자세한 내용은 [워크 로드 관리](workload-management.md)합니다.  
  
요청을 실행 하지 않고 너무 오래 대기 중일 수 있습니다. 요청 문제를 해결 하는 방법 중 하나에 요청 되어야 하는 동시성 슬롯의 수를 확인 하는 것입니다.  다음 예제에서는 각 대기 중인 요청에 필요한 동시성 슬롯 수를 보여 줍니다.  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>관련 항목  
[워크 로드 관리](workload-management.md)  
  
