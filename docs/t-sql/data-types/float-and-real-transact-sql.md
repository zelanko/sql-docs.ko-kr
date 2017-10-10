---
title: "float 및 real (TRANSACT-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: dd20fe12af6f1dcaf378d737961bc2ba354aabe5
ms.openlocfilehash: 0ce2e3272c30057f533796e0822256c6235de0c1
ms.contentlocale: ko-kr
ms.lasthandoff: 10/04/2017

---
# <a name="float-and-real-transact-sql"></a>float 및 real(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

부동 소수점 숫자 데이터에 사용하는 근사 숫자 데이터 형식입니다. 부동 소수점 데이터는 근사값이므로 해당 데이터 형식 범위에 있는 모든 값을 정확하게 표현할 수는 없습니다. ISO 동의어는 **실제** 은 **float(24)**합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
**float** [ **(***n***)** ] 여기서  *n*  저장 하는 데 사용 되는 비트 수 가 수는 **float** 과학적 표기법으로 숫자 및 이므로 전체 자릿수 및 저장소 크기를 지정 합니다. 경우  *n*  지정, 사이의 값 이어야 **1** 및 **53**합니다. 기본값  *n*  은 **53**합니다.
  
|*n*값|전체 자릿수|저장소 크기|  
|---|---|---|
|**1-24**|7 자리|4 바이트|  
|**25-53**|15자리|8바이트|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]처리  *n*  가능한 두 값 중 하나로 합니다. 경우 **1**<=n<=**24**,  *n*  로 처리 **24**합니다. 경우 **25**<=n<=**53**,  *n*  로 처리 **53**합니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float**[**(n)**] 데이터 형식은 모든 값에 대 한 ISO 표준 준수  *n*  에서 **1** 통해 **53**합니다. 에 대 한 동의어 **전체 자릿수를 두 번** 은 **float(53)**합니다.
  
## <a name="remarks"></a>주의  
  
|데이터 형식|범위|저장소|  
|---|---|---|
|**float**|- 1.79E+308에서 -2.23E-308, 0과 2.23E-308에서 1.79E+308|값에 따라 달라 집니다.*n*|  
|**real**|- 3.40E+38에서 -1.18E - 38, 0과 1.18E-38에서 3.40E + 38|4 바이트|  
  
##  <a name="converting-float-and-real-data"></a>Float 및 real 데이터 변환  
값 **float** 정수 형식으로 변환 될 때 잘립니다.
  
변환 하려는 경우 **float** 또는 **실제** 문자 데이터에 CAST () 보다 더 유용한 일반적으로 STR 문자열 함수를 사용 하 여 합니다. 이는 STR을 사용하면 서식을 더 많이 제어할 수 있기 때문입니다. 자세한 내용은 참조 [STR &#40; Transact SQL &#41; ](../../t-sql/functions/str-transact-sql.md) 및 [함수 &#40; Transact SQL &#41; ](../../t-sql/functions/functions.md).
  
변환 **float** 과학적 표기법을 사용 하는 값 **10 진수** 또는 **숫자** 전체 자릿수가 17 자리로의 값으로 제한 됩니다. 값 < 0으로 5E-18 내림 합니다.
  
## <a name="see-also"></a>참고 항목
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[데이터 형식 변환 &#40; 데이터베이스 엔진 &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  

