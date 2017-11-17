---
title: SET STATISTICS PROFILE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PROFILE
- SET_STATISTICS_PROFILE_TSQL
- PROFILE_TSQL
- SET STATISTICS PROFILE
dev_langs:
- TSQL
helpviewer_keywords:
- profiles [SQL Server], displaying
- statements [SQL Server], profile information
- SET STATISTICS PROFILE statement
- STATISTICS PROFILE option
- statistical information [SQL Server], profiles
ms.assetid: c635e262-35fa-421a-aa6f-a1c30f351647
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 69ceaedf2cfe62b20217b4e218568cec1bc2a933
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="set-statistics-profile-transact-sql"></a>SET STATISTICS PROFILE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  문에 대한 프로필 정보를 표시합니다. STATISTICS PROFILE은 임의 쿼리, 뷰 및 저장 프로시저에서 작동합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SET STATISTICS PROFILE { ON | OFF }  
```  
  
## <a name="remarks"></a>주의  
 STATISTICS PROFILE 옵션을 설정하면 실행된 각 쿼리가 일반 결과 집합을 반환하고 그 뒤에는 쿼리 실행 프로필을 보여 주는 추가 결과 집합을 반환합니다.  
  
 추가 결과 집합에는 쿼리에 대한 SHOWPLAN_ALL 열과 다음 열이 포함됩니다.  
  
|열 이름|Description|  
|-----------------|-----------------|  
|**행**|각 연산자에서 만든 실제 행 수|  
|**실행**|연산자가 실행된 횟수|  
  
## <a name="permissions"></a>Permissions  
 SET STATISTICS PROFILE을 사용하여 출력을 보려면 다음 권한이 있어야 합니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있는 적절한 권한  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 참조하는 개체가 포함된 모든 데이터베이스에 대한 SHOWPLAN 권한  
  
 STATISTICS PROFILE 결과 집합을 생성하지 않는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있는 적절한 권한만 있으면 됩니다. STATISTICS PROFILE 결과 집합을 생성하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 경우에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 실행 권한과 SHOWPLAN 권한이 모두 있어야 합니다. 그렇지 않으면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 실행이 중단되고 실행 계획 정보도 생성되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET showplan_all 옵션 &#40; Transact SQL &#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [통계 시간 &#40; 설정 합니다. Transact SQL &#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)   
 [SET STATISTICS IO &#40; Transact SQL &#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  

