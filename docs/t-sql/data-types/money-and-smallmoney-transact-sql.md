---
title: money 및 smallmoney(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 86f834e26e20c729eaa69770eb4da37deb6cf772
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47747491"
---
# <a name="money-and-smallmoney-transact-sql"></a>money 및 smallmoney(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

통화 또는 통화 값을 나타내는 데이터 형식입니다.
  
## <a name="remarks"></a>Remarks  
  
|데이터 형식|범위|저장소|  
|---|---|---|
|**money**|-922,337,203,685,477.5808~922,337,203,685,477.5807(-922,337,203,685,477.58<br />~922,337,203,685,477.58(Informatica의 경우)  Informatica는 4개가 아닌 2개의 소수만 지원합니다.)|8바이트|  
|**smallmoney**|- 214,748.3648 - 214,748.3647|4바이트|  
  
**money** 및 **smallmoney** 데이터 형식은 나타내는 통화 단위의 1/10000까지 정확합니다. Informatica의 경우 **money** 및 **smallmoney** 데이터 형식은 나타내는 통화 단위의 1/100까지 정확합니다.
  
전체 통화 단위에서 부분 통화 단위(예: 센트)를 구분하려면 마침표를 사용합니다. 예를 들어 2.15는 2달러 15센트를 나타냅니다.
  
이러한 데이터 형식은 다음 통화 기호 중 하나를 사용합니다.
  
![통화 기호, 16진수 값 표](../../t-sql/data-types/media/money01.gif "통화 기호, 16진수 값 표")
  
통화 데이터는 작은따옴표로 묶지 않아도 됩니다. 통화 값 앞에 통화 기호를 붙일 수 있지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이 기호와 관련된 통화 정보를 저장하지 않으며 숫자 값만 저장합니다.
  
## <a name="converting-money-data"></a>money 데이터 변환
정수 데이터 형식에서 **money**로 변환할 때 단위는 통화 단위로 간주됩니다. 예를 들어 정수 값 4는 4 통화 단위와 동등한 **money**로 변환됩니다.
  
다음 예에서는 **smallmoney** 및 **money** 값을 각각 **varchar** 및 **decimal** 데이터 형식으로 변환합니다.
  
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
  
## <a name="see-also"></a>관련 항목:
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
[DECLARE@local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
[SET@local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
[sys.types&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  
