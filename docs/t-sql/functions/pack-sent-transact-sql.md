---
title: '@@PACK_SENT(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@PACK_SENT'
- '@@PACK_SENT_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- number of output packets written
- '@@PACK_SENT function'
- packets [SQL Server], output
- networking [SQL Server], output packets
- connections [SQL Server], packets
- output packets written to network [SQL Server]
ms.assetid: 8a322162-24c9-48e9-bfa4-c060e4e11dba
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a9acc45cf23878582f39fffc72a9c19ba01f9729
ms.sourcegitcommit: 98324d9803edfa52508b6d5d3554614d0350a0b9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52321629"
---
# <a name="x40x40packsent-transact-sql"></a>&#x40;&#x40;PACK_SENT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 마지막으로 시작된 후 네트워크에 쓴 출력 패킷 수를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql
@@PACK_SENT  
```  
  
## <a name="return-types"></a>반환 형식  
 **integer**  
  
## <a name="remarks"></a>Remarks  
 보낸 패킷과 받은 패킷을 포함하여 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 통계가 들어 있는 보고서를 표시하려면 **sp_monitor**를 실행합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `@@PACK_SENT`의 사용법을 보여 줍니다.  
  
```sql
SELECT @@PACK_SENT AS 'Pack Sent';  
```  
  
 결과 집합의 예는 다음과 같습니다.  
  
```  
Pack Sent  
-----------  
291  
```  
  
## <a name="see-also"></a>참고 항목  
 [@@PACK_RECEIVED&#40;Transact-SQL&#41;](../../t-sql/functions/pack-received-transact-sql.md)   
 [sp_monitor&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [시스템 통계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
