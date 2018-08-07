---
title: float 및 real(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- float
- real_TSQL
- real
- float_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- numeric data type, floating point
- float data type
- floating point data [SQL Server]
- real data type
ms.assetid: 08ea66b7-624e-4d8b-86bc-750ff76cdfc5
caps.latest.revision: 40
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 4dbe0f65cd06b9f9ad3ff5b164c16317a8fd5080
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39452507"
---
# <a name="float-and-real-transact-sql"></a>float 및 real(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

부동 소수점 숫자 데이터에 사용하는 근사 숫자 데이터 형식입니다. 부동 소수점 데이터는 근사값이므로 해당 데이터 형식 범위에 있는 모든 값을 정확하게 표현할 수는 없습니다. **real**의 ISO 동의어는 **float(24)** 입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
**float** [ **(***n***)** ] 여기서 *n*은 과학적 표기법으로 **float** 숫자의 가수를 저장하는 데 사용되는 비트 수로서, 전체 자릿수 및 저장소 크기를 결정합니다. *n*이 지정된 경우 그 값은 **1**에서 **53** 사이여야 합니다. *n*의 기본값은 **53**입니다.
  
|*n* 값|전체 자릿수|저장소 크기|  
|---|---|---|
|**1-24**|7자리|4바이트|  
|**25-53**|15자리|8바이트|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 *n*을 가능한 두 값 중 하나로 처리합니다. **1**<=n<=**24**이면 *n*은 **24**로 처리됩니다. **25**<=n<=**53**이면 *n*은 **53**으로 처리됩니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 **float**[**(n)**] 데이터 형식은 **1**부터 **53**까지 *n*의 모든 값에 대해 ISO 표준을 준수합니다. **double precision**의 동의어는 **float(53)** 입니다.
  
## <a name="remarks"></a>Remarks  
  
|데이터 형식|범위|저장소|  
|---|---|---|
|**float**|- 1.79E+308에서 -2.23E-308, 0과 2.23E-308에서 1.79E+308|이 값은 *n*의 값에 따라 달라집니다.|  
|**real**|- 3.40E+38에서 -1.18E - 38, 0과 1.18E-38에서 3.40E + 38|4바이트|  
  
##  <a name="converting-float-and-real-data"></a>float 및 real 데이터 변환  
**float**의 값은 정수 형식으로 변환될 때 잘립니다.
  
**float** 또는 **real**에서 문자 데이터로 변환할 때 일반적으로 STR 문자열 함수를 사용하는 것이 CAST( )를 사용하는 것보다 유용합니다. 이는 STR을 사용하면 서식을 더 많이 제어할 수 있기 때문입니다. 자세한 내용은 [STR&#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md) 및 [함수&#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)를 참조하세요.
  
과학적 표기법을 사용하는 **float** 값을 **decimal** 또는 **numerci**로 변환할 경우 전체 자릿수 값이 17자리로 제한됩니다. <5E-18의 값은 0으로 내림합니다.
  
## <a name="see-also"></a>관련 항목:
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[데이터 형식 변환&#40;데이터베이스 엔진&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  
