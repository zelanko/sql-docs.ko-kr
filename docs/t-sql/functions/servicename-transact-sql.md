---
title: '@@SERVICENAME(Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@SERVICENAME_TSQL'
- '@@SERVICENAME'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@SERVICENAME function'
- names [SQL Server], registry keys
- registry keys [SQL Server]
ms.assetid: 5b0b35be-50ae-411d-a607-bf7464b73624
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2f08aa295a5c6bcd3a76a350e2cd9b0ec2a84d10
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40servicename-transact-sql"></a>&#x40;&#x40;SERVICENAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 실행되고 있는 레지스트리 키의 이름을 반환합니다. @@SERVICENAME은 현재 인스턴스가 기본 인스턴스인 경우에는 'MSSQLSERVER'를 반환하고 현재 인스턴스가 명명된 인스턴스인 경우에는 인스턴스 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@SERVICENAME  
```  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar**  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 MSSQLServer라는 서비스로 실행됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `@@SERVICENAME`를 사용하는 방법을 보여 줍니다.  
  
```  
SELECT @@SERVICENAME AS 'Service Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Service Name                    
------------------------------  
MSSQLSERVER                     
```  
  
## <a name="see-also"></a>참고 항목  
 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [데이터베이스 엔진 서비스 관리](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  
