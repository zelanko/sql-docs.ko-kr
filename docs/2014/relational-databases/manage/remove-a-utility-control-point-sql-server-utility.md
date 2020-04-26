---
title: 유틸리티 제어 지점 제거(SQL Server 유틸리티) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: c048a416-900e-4c77-8243-e0f0d8b94068
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 46f440aa6b40d8a2e0ff48c59818b722073b1628
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62640362"
---
# <a name="remove-a-utility-control-point-sql-server-utility"></a>유틸리티 제어 지점 제거(SQL Server 유틸리티)
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스로부터 [!INCLUDE[tsql](../../includes/tsql-md.md)]UCP(유틸리티 제어 지점)를 제거하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 유틸리티 제어 지점을 제거합니다.**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
 이 절차를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 UCP를 제거하기 전에 다음 요구 사항을 확인하세요. 저장 프로시저는 작업의 일부로 필수 구성 요소 검사를 실행합니다.  
  
-   이 절차를 실행하기 전에 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 관리되는 인스턴스를 UCP에서 제거해야 합니다. 즉, UCP가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스입니다. 자세한 내용은 [SQL Server 유틸리티에서 SQL Server 인스턴스 제거](remove-an-instance-of-sql-server-from-the-sql-server-utility.md)를 참조하세요.  
  
-   UCP에 해당하는 컴퓨터에서 이 절차를 실행해야 합니다.  
  
-   UCP가 제거된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 유틸리티 이외의 데이터 컬렉션 집합이 있는 경우 UMDW 데이터베이스(sysutility_mdw)는 이 절차로 삭제되지 않습니다. 이런 경우 UCP를 다시 만들기 전에 UMDW 데이터베이스(sysutility_mdw)를 수동으로 삭제해야 합니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 UCP를 만들 때 필요한 권한인 `sysadmin` 권한의 사용자가 이 절차를 실행해야 합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-remove-a-utility-control-point"></a>유틸리티 제어 지점을 제거하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
```  
EXEC msdb.dbo.sp_sysutility_ucp_remove;  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 유틸리티 기능 및 태스크](sql-server-utility-features-and-tasks.md)   
 [유틸리티 탐색기를 사용하여 SQL Server 유틸리티 관리](use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [SQL Server 유틸리티 문제 해결](../../database-engine/troubleshoot-the-sql-server-utility.md)  
  
  
