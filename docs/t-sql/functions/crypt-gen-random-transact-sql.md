---
title: CRYPT_GEN_RANDOM(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CRYPT_GEN_RANDOM_TSQL
- CRYPT_GEN_RANDOM
dev_langs:
- TSQL
helpviewer_keywords:
- CRYPT_GEN_RANDOM function
ms.assetid: b74bd9d4-758e-4b94-89a0-76dcda6d8c42
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 70df8f06eb1561dd186d5be643a5863ffab5981a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68026455"
---
# <a name="crypt_gen_random-transact-sql"></a>CRYPT_GEN_RANDOM(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이 함수는 CAPI(Crypto API)에서 임의로 생성된 암호화 수를 반환합니다. `CRYPT_GEN_RANDOM`은 지정된 수의 바이트 길이로 16진수를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CRYPT_GEN_RANDOM ( length [ , seed ] )   
```  
  
## <a name="arguments"></a>인수  
*length*  
`CRYPT_GEN_RANDOM`에서 만들 숫자의 길이(바이트)입니다. *length* 인수에는 **int** 데이터 형식 및 1~8000 사이의 값 범위가 있습니다. `CRYPT_GEN_RANDOM`은 이 범위 이외의 **int** 값에 NULL을 반환합니다. 
  
*seed*  
임의 초기값으로 사용할 선택적인 16진수입니다. *seed*의 길이는 *length* 인수의 값과 일치해야 합니다. *seed* 인수에는 **varbinary(8000)** 데이터 형식이 포함됩니다.
  
## <a name="returned-types"></a>반환 형식  
**varbinary(8000)**
  
## <a name="permissions"></a>사용 권한  
이 함수는 공개 함수이며 특별한 사용 권한이 필요하지 않습니다.
  
## <a name="examples"></a>예  
  
### <a name="a-generating-a-random-number"></a>A. 난수 생성  
이 함수는 길이 50바이트인 임의의 수를 생성합니다.
  
```sql
SELECT CRYPT_GEN_RANDOM(50) ;  
```  
  
이 함수는 4바이트 초기값을 사용하여 길이 4바이트인 임의의 수를 생성합니다.
  
```sql
SELECT CRYPT_GEN_RANDOM(4, 0x25F18060) ;  
```  
  
## <a name="see-also"></a>참고 항목
[RAND&#40;Transact-SQL&#41;](../../t-sql/functions/rand-transact-sql.md)
  
  
