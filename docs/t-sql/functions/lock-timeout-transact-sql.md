---
title: '@@LOCK_TIMEOUT (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@LOCK_TIMEOUT'
- '@@LOCK_TIMEOUT_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- '@@LOCK_TIMEOUT function'
- current lock time-out setting
- locking [SQL Server], time-outs
ms.assetid: 6bf8bf97-60b8-40c1-b89d-8f5a00bcae2e
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: c9e15fae306d313e667aa3c727f96e6fdfb0aa34
ms.contentlocale: ko-kr
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40locktimeout-transact-sql"></a>&#x40;&#x40;LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 세션의 현재 잠금 시간 제한 설정(밀리초)을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@LOCK_TIMEOUT  
```  
  
## <a name="return-types"></a>반환 형식  
 **integer**  
  
## <a name="remarks"></a>주의  
 SET LOCK_TIMEOUT을 통해 응용 프로그램은 문이 차단된 리소스를 기다리는 최대 시간을 설정할 수 있습니다. 문이 LOCK_TIMEOUT 설정보다 오래 대기한 경우 차단된 문은 자동으로 취소되고 오류 메시지가 응용 프로그램으로 반환됩니다.  
  
 @@LOCK_TIMEOUT SET LOCK_TIMEOUT 현재 세션에서 아직 실행 되지 않은 경우-1의 값을 반환 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 LOCK_TIMEOUT 값이 설정되지 않은 경우의 결과 집합을 보여 줍니다.  
  
```  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 결과 집합은 다음과 같습니다.  
  
```  
Lock Timeout  
------------  
-1  
```  
  
 이 예에서는 LOCK_TIMEOUT을 1800 밀리초로 설정 하 고 다음 호출@LOCK_TIMEOUT 합니다.  
  
```  
SET LOCK_TIMEOUT 1800;  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 결과 집합은 다음과 같습니다.  
  
```  
Lock Timeout  
------------  
1800          
```  
  
## <a name="see-also"></a>관련 항목:  
 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SET LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  

