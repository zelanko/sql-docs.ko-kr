---
title: ad hoc distributed queries 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- OPENROWSET function, ad hoc distributed queries option
- Ad Hoc Distributed Queries option
- ad hoc distributed queries
- 7415 (Database Engine Error)
- OPENDATASOURCE function, ad hoc distributed queries option
- ad hoc access
ms.assetid: 5b982015-e196-44c3-83b8-275fb9d769b2
caps.latest.revision: 27
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: d172024326dd3b5728fa5aa498a77551403bf9b1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36173177"
---
# <a name="ad-hoc-distributed-queries-server-configuration-option"></a>임시 분산 쿼리 서버 구성 옵션
  기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 OPENROWSET 및 OPENDATASOURCE를 사용하는 임시 분산 쿼리를 허용하지 않습니다. 이 옵션을 1로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 임시 액세스가 허용됩니다. 이 옵션을 설정하지 않거나 0로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 임시 액세스가 허용되지 않습니다.  
  
 임시 분산 쿼리에서는 OPENROWSET 및 OPENDATASOURCE 함수를 사용하여 OLE DB를 사용하는 원격 데이터 원본에 연결합니다. OPENROWSET과 OPENDATASOURCE는 자주 사용되지 않는 OLE DB 데이터 원본을 참조하기 위해서만 사용해야 합니다. 여러 번 액세스될 모든 데이터 원본에 대해서는 연결된 서버를 정의해야 합니다.  
  
> [!IMPORTANT]  
>  임시 이름 사용을 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 모든 인증된 로그인에서 공급자에 액세스할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자는 모든 로컬 로그인에서 액세스해도 안전한 공급자에 대해 이 기능을 설정해야 합니다.  
  
## <a name="remarks"></a>Remarks  
 **임시 분산 쿼리** 가 설정되지 않은 임시 연결을 만들려고 하면 Msg 7415, Level 16, State 1, Line 1 오류가 발생합니다.  
  
 OLE DB 공급자 'Microsoft.ACE.OLEDB.12.0'에 대한 임의 액세스가 거부되었습니다. 연결된 서버를 통해 이 공급자에 액세스해야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 임시 분산 쿼리를 실행한 다음 `Seattle1` 함수를 사용하여 `OPENROWSET` 이라는 서버를 쿼리합니다.  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
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
  
## <a name="see-also"></a>관련 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [연결된 서버&#40;데이터베이스 엔진&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [OPENDATASOURCE&#40;Transact-SQL&#41;](/sql/t-sql/functions/opendatasource-transact-sql)   
 [sp_addlinkedserver&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)  
  
  
