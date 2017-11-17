---
title: "money 및 smallmoney (TRANSACT-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- money_TSQL
- money
- smallmoney
- smallmoney_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- money data type, about money data type
- money data type
- smallmoney data type
- values [SQL Server], monetary
- currency [SQL Server]
ms.assetid: 57861137-89ea-4b89-b361-390597d7bccc
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bd07ecd1cdacc686e0f831320fd5e939c0c174da
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="money-and-smallmoney-transact-sql"></a>money 및 smallmoney(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

통화 또는 통화 값을 나타내는 데이터 형식입니다.
  
## <a name="remarks"></a>주의  
  
|데이터 형식|범위|저장소|  
|---|---|---|
|**money**|-922,337,203,685,477.5808를 922337203685, 477.5807 (-922,337,203,685,477.58<br />Informatica에 대 한 922,337,203,685,477.58 to.  Informatica 지원 두 자리, 4 개 없습니다.)|8바이트|  
|**smallmoney**|- 214,748.3648 - 214,748.3647|4 바이트|  
  
**money** 및 **smallmoney** 데이터 형식을 나타내는 통화 단위의 1/10, 000 정확 하 게 합니다. Informatica에 대 한는 **money** 및 **smallmoney** 데이터 형식을 나타내는 통화 단위의 1 / 100을 정확 하 게 합니다.
  
전체 통화 단위에서 부분 통화 단위(예: 센트)를 구분하려면 마침표를 사용합니다. 예를 들어 2.15는 2달러 15센트를 나타냅니다.
  
이러한 데이터 형식은 다음 통화 기호 중 하나를 사용합니다.
  
![통화 기호, 16 진수 값 표](../../t-sql/data-types/media/money01.gif "통화 기호, 16 진수 값 표")
  
통화 데이터는 작은따옴표로 묶지 않아도 됩니다. 통화 값 앞에 통화 기호를 붙일 수 있지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 기호와 관련된 통화 정보를 저장하지 않으며 숫자 값만 저장합니다.
  
## <a name="converting-money-data"></a>Money 데이터 변환
변환할 때 **money** 정수 데이터 형식에서 단위는 통화 단위로 것으로 간주 됩니다. 정수 값 4 변환할 예를 들어는 **money** 는 4 통화 단위와 동일 합니다.
  
다음 예제에서는 변환 **smallmoney** 및 **money** 값을 **varchar** 및 **10 진수** 각각의 데이터 형식입니다.
  
```sql
DECLARE @mymoney_sm smallmoney = 3148.29,  
        @mymoney    money = 3148.29;  
SELECT  CAST(@mymoney_sm AS varchar) AS 'SM_MONEY varchar',  
        CAST(@mymoney AS decimal)    AS 'MONEY DECIMAL';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
SM_MONEY VARCHAR               MONEY DECIMAL  
------------------------------ ----------------------  
3148.29                        3148    
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목
[ALTER table&#40; Transact SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md) 
 [CAST 및 convert&#40; Transact SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md) 
 [테이블 만들기 &#40; Transact SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md) 
 [데이터 형식 &#40; Transact SQL &#41; ](../../t-sql/data-types/data-types-transact-sql.md) 
 [DECLARE @local_variable &#40; Transact SQL &#41; ](../../t-sql/language-elements/declare-local-variable-transact-sql.md) 
 [설정 @local_variable &#40; Transact SQL &#41; ](../../t-sql/language-elements/set-local-variable-transact-sql.md) 
 [sys.types &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  

