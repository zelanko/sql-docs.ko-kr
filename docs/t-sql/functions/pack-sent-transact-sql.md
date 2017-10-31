---
title: '@@PACK_SENT (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@PACK_SENT'
- '@@PACK_SENT_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- number of output packets written
- '@@PACK_SENT function'
- packets [SQL Server], ouput
- networking [SQL Server], output packets
- connections [SQL Server], packets
- output packets written to network [SQL Server]
ms.assetid: 8a322162-24c9-48e9-bfa4-c060e4e11dba
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 212f5ad5bbe56ab994ee50baba81b8a650bf0a93
ms.contentlocale: ko-kr
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40packsent-transact-sql"></a>& #x 40; & #x 40; PACK_SENT (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 마지막으로 시작된 후 네트워크에 쓴 출력 패킷 수를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@PACK_SENT  
```  
  
## <a name="return-types"></a>반환 형식  
 **integer**  
  
## <a name="remarks"></a>주의  
 몇 가지를 포함 하는 보고서를 표시 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 통계를 보내고 받은 패킷에 포함 하 여 **sp_monitor**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `@@PACK_SENT`의 사용법을 보여 줍니다.  
  
```  
SELECT @@PACK_SENT AS 'Pack Sent';  
```  
  
 결과 집합의 예는 다음과 같습니다.  
  
```  
Pack Sent  
-----------  
291  
```  
  
## <a name="see-also"></a>관련 항목:  
 [@@PACK_RECEIVED&#40;Transact-SQL&#41;](../../t-sql/functions/pack-received-transact-sql.md)   
 [sp_monitor &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [시스템 통계 함수 &#40; Transact SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  

