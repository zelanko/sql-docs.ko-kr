---
title: 작업 관리 작업
description: 분석 플랫폼 시스템의 작업 관리 작업.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 88d95eb0a2e0805930cb5f01f5af05b8fc6b3f2e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74399409"
---
# <a name="workload-management-tasks-in-analytics-platform-system"></a>분석 플랫폼 시스템의 작업 관리 작업
분석 플랫폼 시스템의 작업 관리 작업.

## <a name="view-login-members-of-each-resource-class"></a>각 리소스 클래스의 로그인 멤버 보기
SQL Server PDW에서 각 리소스 클래스 서버 역할의 로그인 멤버를 표시 하는 방법을 설명 합니다. 이 쿼리를 사용 하 여 각 로그인에서 제출 된 요청에 허용 되는 리소스 클래스를 파악 합니다.  
  
리소스 클래스에 대 한 설명은 [워크 로드 관리](workload-management.md)를 참조 하세요.  
  
이 쿼리는 각 리소스 클래스에 대 한 멤버 자격 목록을 표시 합니다. Mediumrc, largerc 및 xlargerc의 세 가지 리소스 클래스가 있습니다.  
  
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
  
로그인이이 목록에 없는 경우 해당 요청은 기본 리소스를 받게 됩니다. 로그인이 둘 이상의 리소스 클래스의 멤버인 경우 가장 큰 클래스가 우선적으로 적용 됩니다.  
  
리소스 할당은 [작업 관리](workload-management.md)에 나열 됩니다.  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>요청에 할당 된 시스템 리소스를 변경 합니다.
SQL Server PDW 요청이 실행 되는 리소스 클래스를 확인 하는 방법 및 해당 요청에 대 한 시스템 리소스를 변경 하는 방법을 설명 합니다. 요청에 대 한 리소스를 변경 하려면 [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) 문을 사용 하 여 요청을 제출 하는 로그인의 리소스 클래스 멤버 자격을 변경 해야 합니다.  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>1 단계: 요청을 실행 하는 로그인에 대 한 리소스 클래스를 확인 합니다.  
이 쿼리는 리소스 클래스 서버 역할 멤버 자격의 멤버인 로그인을 표시 합니다. **Mediumrc**, **largerc**및 **xlargerc**의 세 가지 리소스 클래스가 있습니다.  
  
> [!IMPORTANT]  
> 이 쿼리는 **CONTROL SERVER** 권한이 있는 로그인에 의해 실행 되어야 합니다. **CONTROL SERVER** 권한이 없는 로그인에 의해 실행 되는 경우이 쿼리는 현재 로그인에 대 한 역할 멤버 자격만 반환 합니다.  
  
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
  
리소스 클래스 서버 역할의 멤버인 로그인이 없으면 결과 테이블이 비어 있게 됩니다. 이 경우 쿼리가 Ching 이라는 로그인을 반환 하는 경우 Ching에서 요청을 제출 하면 리소스 클래스 시스템 리소스 보다 작은 기본 시스템 리소스가 요청에 수신 됩니다. 로그인이 둘 이상의 리소스 클래스의 멤버인 경우 가장 큰 클래스가 우선적으로 적용 됩니다.  
  
각 리소스 클래스에 대 한 리소스 할당 목록은 [워크 로드 관리](workload-management.md)를 참조 하세요.  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>2 단계: 다른 리소스 클래스 멤버 자격이 있는 로그인으로 요청 실행  
더 크거나 작은 시스템 리소스를 사용 하 여 요청을 실행 하는 방법에는 두 가지가 있습니다.  
  
-   더 크거나 작은 리소스 클래스의 멤버인 다른 로그인에서 요청을 실행 합니다.  
  
-   리소스 클래스 역할 중 하나에 필요한 로그인을 추가 합니다. 이 옵션을 신중 하 게 선택 합니다. 로그인에 대 한 리소스 클래스를 변경 하면 로그인에서 제출한 모든 요청에 대 한 시스템 리소스 수준이 변경 됩니다.  
  
Ching가 largerc 서버 역할의 멤버 라고 가정 합니다. 다음 예에서는 xlargerc 서버 역할에 로그인 Ching를 추가 하는 방법을 보여 줍니다.  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
Ching는 이제 largerc 및 xlargerc 서버 역할의 멤버입니다. Ching가 요청을 제출 하면 요청은 xlargerc 시스템 리소스를 수신 합니다.  
  
다음 예에서는 Ching를 mediumrc 서버 역할로 다시 이동 합니다.  새 역할로 변경 하려면 xlargerc 및 largerc 서버 역할에서 로그인을 제거 하 고 mediumrc 서버 역할에 추가 해야 합니다.  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
Ching는 이제 mediumrc 서버 역할의 멤버입니다.  다음 예에서는 Ching를 변경 하 여 요청에 대 한 기본 시스템 리소스를 포함 합니다.  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
리소스 클래스 역할 멤버 자격을 변경 하는 방법에 대 한 자세한 내용은 [ALTER SERVER role](../t-sql/statements/alter-server-role-transact-sql.md)을 참조 하세요.  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>요청에 대 한 기본 시스템 리소스에 대 한 로그인 변경
SQL Server PDW 로그인에 할당 된 시스템 리소스 할당을 기본 양만큼 변경 하는 방법을 설명 합니다. 
  
리소스 클래스에 대 한 설명은 [워크 로드 관리](workload-management.md) 를 참조 하세요.  
  
로그인이 리소스 클래스 서버 역할의 멤버가 아닌 경우 로그인에 의해 전송 된 요청은 시스템 리소스의 기본 크기를 수신 합니다.  
  
로그인 Matt가 현재 모든 리소스 클래스 서버 역할의 멤버 이며 요청에서 기본 리소스만 수신 하도록 되돌려야 한다고 가정 합니다.  다음 예제에서는 세 가지 리소스 클래스 서버 역할의 멤버 자격을 삭제 하 여 Matt 요청에 기본 리소스를 할당 합니다.  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>대기 중인 요청에 필요한 동시성 슬롯 수를 표시 합니다.
SQL Server PDW에서 실행 되기를 기다리는 요청에 필요한 동시성 슬롯 수를 파악 하는 방법을 설명 합니다.  
  
자세한 내용은 [워크 로드 관리](workload-management.md)를 참조 하세요.  
  
요청을 실행 하지 않고 너무 오래 기다릴 수 있습니다. 요청 문제를 해결 하는 방법 중 하나는 요청에 필요한 동시성 슬롯 수를 확인 하는 것입니다.  다음 예에서는 대기 중인 각 요청에 필요한 동시성 슬롯 수를 보여 줍니다.  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>참고 항목  
[워크 로드 관리](workload-management.md)  
  
