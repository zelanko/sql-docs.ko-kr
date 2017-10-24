---
title: '@@PACK_RECEIVED (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@PACK_RECEIVED_TSQL'
- '@@PACK_RECEIVED'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@PACK_RECEIVED function'
- number of packets read
- packets [SQL Server], number read
ms.assetid: 5c0b3d36-bfad-4f0b-abb8-e8f6391b32cd
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a4d0bfea159c945dab24060144783221513e9fcd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40packreceived-transact-sql"></a>& #x 40; & #x 40; PACK_RECEIVED (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  마지막으로 시작한 이후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 네트워크에서 읽은 입력 패킷 수를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@PACK_RECEIVED  
```  
  
## <a name="return-types"></a>반환 형식  
 **integer**  
  
## <a name="remarks"></a>주의  
 몇 가지를 포함 하는 보고서를 표시 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 통계를 보내고 받은 패킷에 포함 하 여 **sp_monitor**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `@@PACK_RECEIVED`의 사용법을 보여 줍니다.  
  
```  
SELECT @@PACK_RECEIVED AS 'Packets Received';   
```  
  
 결과 집합의 예는 다음과 같습니다.  
  
```  
Packets Received  
----------------  
128  
```  
  
## <a name="see-also"></a>관련 항목:  
 [@@PACK_SENT](../../t-sql/functions/pack-sent-transact-sql.md)   
 [sp_monitor](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [시스템 통계 함수](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  

