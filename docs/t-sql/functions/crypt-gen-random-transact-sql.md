---
title: CRYPT_GEN_RANDOM (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CRYPT_GEN_RANDOM_TSQL
- CRYPT_GEN_RANDOM
dev_langs:
- TSQL
helpviewer_keywords:
- CRYPT_GEN_RANDOM function
ms.assetid: b74bd9d4-758e-4b94-89a0-76dcda6d8c42
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f2732196567dc98dc768e81b305ffa72ed453a94
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="cryptgenrandom-transact-sql"></a>CRYPT_GEN_RANDOM(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

CAPI(Crypto API)로 생성된 암호화 난수를 반환합니다. 출력은 지정된 바이트 수의 16진수입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CRYPT_GEN_RANDOM ( length [ , seed ] )   
```  
  
## <a name="arguments"></a>인수  
*length*  
만들려는 숫자의 길이입니다. 최대값은 8000입니다. *길이* 형식이 **int**합니다.
  
*시드*  
임의 초기값으로 사용할 선택적 데이터입니다.  있어야 이상 *길이* 데이터의 바이트입니다. *시드* 은 **varbinary (8000)**합니다.
  
## <a name="returned-types"></a>반환 형식  
**varbinary (8000)**
  
## <a name="permissions"></a>Permissions  
이 함수는 공개 함수이며 특별한 사용 권한이 필요하지 않습니다.
  
## <a name="examples"></a>예  
  
### <a name="a-generating-a-random-number"></a>1. 난수 생성  
다음 예에서는 50바이트 길이의 난수를 생성합니다.
  
```sql
SELECT CRYPT_GEN_RANDOM(50) ;  
```  
  
다음 예에서는 4바이트 초기값을 사용하여 4바이트 길이의 난수를 생성합니다.
  
```sql
SELECT CRYPT_GEN_RANDOM(4, 0x25F18060) ;  
```  
  
## <a name="see-also"></a>참고 항목
[RAND &#40; Transact SQL &#41;](../../t-sql/functions/rand-transact-sql.md)
  
  

