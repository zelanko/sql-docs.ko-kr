---
title: SMALLDATETIMEFROMPARTS (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SMALLDATETIMEFROMPARTS
- SMALLDATETIMEFROMPARTS_TSQL
dev_langs: TSQL
helpviewer_keywords: SMALLDATETIMEFROMPARTS function
ms.assetid: 7467fdab-e588-419c-9e29-42caec34a9ea
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 07eaaf385e0227f3e5ddf7d0c1ee506aecca211a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="smalldatetimefromparts-transact-sql"></a>SMALLDATETIMEFROMPARTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  반환 된 **smalldatetime** 지정 된 날짜 및 시간에 대 한 값입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SMALLDATETIMEFROMPARTS ( year, month, day, hour, minute )  
```  
  
## <a name="arguments"></a>인수  
 *연도*  
 연도를 지정하는 정수 식입니다.  
  
 *월*  
 월을 지정하는 정수 식입니다.  
  
 *일*  
 일을 지정하는 정수 식입니다.  
  
 *1 시간*  
 시간을 지정하는 정수 식입니다.  
  
 *분*  
 분을 지정하는 정수 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 **smalldatetime**  
  
## <a name="remarks"></a>주의  
 이 함수는 완전히 초기화 된에 대 한 생성자 처럼 작동 **smalldatetime** 값입니다. 인수가 유효하지 않으면 오류가 발생합니다. 필수 인수가 Null일 경우에는 Null이 반환됩니다.  
  
 이 함수는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이상 서버에 대해서는 원격으로 실행할 수 있지만 이전 버전에 있는 서버에 원격화 없으면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]합니다.  
  
## <a name="examples"></a>예  
  
```  
SELECT SMALLDATETIMEFROMPARTS ( 2010, 12, 31, 23, 59 ) AS Result  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------------------  
2011-01-01 00:00:00  
  
(1 row(s) affected)  
```  
  

