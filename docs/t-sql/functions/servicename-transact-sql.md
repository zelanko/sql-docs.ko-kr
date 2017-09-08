---
title: '@@SERVICENAME (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8e93602aed47f8b5147d39eaf41503488f57a855
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="servicename-transact-sql"></a>@@SERVICENAME (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 실행되고 있는 레지스트리 키의 이름을 반환합니다. @@SERVICENAME 경우 'MSSQLSERVER'를 반환 합니다. 현재 인스턴스가 기본 인스턴스가;이 함수는 현재 인스턴스가 명명 된 인스턴스인 경우 인스턴스 이름을 반환 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
@@SERVICENAME  
```  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar**  
  
## <a name="remarks"></a>주의  
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
  
## <a name="see-also"></a>관련 항목:  
 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [데이터베이스 엔진 서비스 관리](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  
