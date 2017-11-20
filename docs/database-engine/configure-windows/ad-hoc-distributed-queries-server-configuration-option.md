---
title: "ad hoc distributed queries 서버 구성 옵션 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OPENROWSET function, ad hoc distributed queries option
- Ad Hoc Distributed Queries option
- ad hoc distributed queries
- 7415 (Database Engine Error)
- OPENDATASOURCE function, ad hoc distributed queries option
- ad hoc access
ms.assetid: 5b982015-e196-44c3-83b8-275fb9d769b2
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f8f43ff2b18872b4d70e02c770706b34cfe12c9d
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="ad-hoc-distributed-queries-server-configuration-option"></a>임시 분산 쿼리 서버 구성 옵션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 OPENROWSET 및 OPENDATASOURCE를 사용하는 임시 분산 쿼리를 허용하지 않습니다. 이 옵션을 1로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 임시 액세스가 허용됩니다. 이 옵션을 설정하지 않거나 0로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 임시 액세스가 허용되지 않습니다.  
  
 임시 분산 쿼리에서는 OPENROWSET 및 OPENDATASOURCE 함수를 사용하여 OLE DB를 사용하는 원격 데이터 원본에 연결합니다. OPENROWSET과 OPENDATASOURCE는 자주 사용되지 않는 OLE DB 데이터 원본을 참조하기 위해서만 사용해야 합니다. 여러 번 액세스될 모든 데이터 원본에 대해서는 연결된 서버를 정의해야 합니다.  
  
> [!IMPORTANT]  
>  임시 이름 사용을 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 모든 인증된 로그인에서 공급자에 액세스할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자는 모든 로컬 로그인에서 액세스해도 안전한 공급자에 대해 이 기능을 설정해야 합니다.  
  
## <a name="remarks"></a>주의  
 **임시 분산 쿼리** 가 설정되지 않은 임시 연결을 만들려고 하면 Msg 7415, Level 16, State 1, Line 1 오류가 발생합니다.  
  
 OLE DB 공급자 'Microsoft.ACE.OLEDB.12.0'에 대한 임의 액세스가 거부되었습니다. 연결된 서버를 통해 이 공급자에 액세스해야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 임시 분산 쿼리를 실행한 다음 `Seattle1` 함수를 사용하여 `OPENROWSET` 이라는 서버를 쿼리합니다.  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;
GO 
sp_configure 'Ad Hoc Distributed Queries', 1;  
RECONFIGURE;  
GO  
  
SELECT a.*  
FROM OPENROWSET('SQLNCLI', 'Server=Seattle1;Trusted_Connection=yes;',  
     'SELECT GroupName, Name, DepartmentID  
      FROM AdventureWorks2012.HumanResources.Department  
      ORDER BY GroupName, Name') AS a;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [연결된 서버&#40;데이터베이스 엔진&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [OPENDATASOURCE&#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
  

