---
title: SET STATISTICS PROFILE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
manager: craigg
ms.openlocfilehash: 6494f792c1dcfbb92bfe48d3063df533d0ff1510
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33069670"
---
# <a name="set-statistics-profile-transact-sql"></a>SET STATISTICS PROFILE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  문에 대한 프로필 정보를 표시합니다. STATISTICS PROFILE은 임의 쿼리, 뷰 및 저장 프로시저에서 작동합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SET STATISTICS PROFILE { ON | OFF }  
```  
  
## <a name="remarks"></a>Remarks  
 STATISTICS PROFILE 옵션을 설정하면 실행된 각 쿼리가 일반 결과 집합을 반환하고 그 뒤에는 쿼리 실행 프로필을 보여 주는 추가 결과 집합을 반환합니다.  
  
 추가 결과 집합에는 쿼리에 대한 SHOWPLAN_ALL 열과 다음 열이 포함됩니다.  
  
|열 이름|Description|  
|-----------------|-----------------|  
|**행**|각 연산자에서 만든 실제 행 수|  
|**Executes**|연산자가 실행된 횟수|  
  
## <a name="permissions"></a>사용 권한  
 SET STATISTICS PROFILE을 사용하여 출력을 보려면 다음 권한이 있어야 합니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있는 적절한 권한  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 참조하는 개체가 포함된 모든 데이터베이스에 대한 SHOWPLAN 권한  
  
 STATISTICS PROFILE 결과 집합을 생성하지 않는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있는 적절한 권한만 있으면 됩니다. STATISTICS PROFILE 결과 집합을 생성하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 경우에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 실행 권한과 SHOWPLAN 권한이 모두 있어야 합니다. 그렇지 않으면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 실행이 중단되고 실행 계획 정보도 생성되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET STATISTICS TIME &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)   
 [SET STATISTICS IO &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  
