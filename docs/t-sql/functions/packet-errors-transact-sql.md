---
title: '@@PACKET_ERRORS(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@PACKET_ERRORS'
- '@@PACKET_ERRORS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@PACKET_ERRORS function'
- number of packet errors
- packets [SQL Server], errors
- networking [SQL Server], packet errors
- connections [SQL Server], packets
ms.assetid: f7da1b80-5cbe-42fa-be71-40c6af16383a
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: aa6a8629790c1f0fd3208ecfd4b2e0517f9bb86c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65943543"
---
# <a name="x40x40packeterrors-transact-sql"></a>&#x40;&#x40;PACKET_ERRORS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 마지막으로 시작된 이후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결에서 발생한 네트워크 패킷 오류 수를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
@@PACKET_ERRORS  
```  
  
## <a name="return-types"></a>반환 형식  
 **integer**  
  
## <a name="remarks"></a>Remarks  
 패킷 오류를 비롯하여 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 통계가 포함된 보고서를 표시하려면 **sp_monitor**를 실행합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `@@PACKET_ERRORS`를 사용하는 방법을 보여 줍니다.  
  
```  
SELECT @@PACKET_ERRORS AS 'Packet Errors';  
```  
  
 결과 집합의 예는 다음과 같습니다.  
  
```  
Packet Errors  
-------------  
0  
```  
  
## <a name="see-also"></a>참고 항목  
 [@@PACK_RECEIVED&#40;Transact-SQL&#41;](../../t-sql/functions/pack-received-transact-sql.md)   
 [@@PACK_SENT&#40;Transact-SQL&#41;](../../t-sql/functions/pack-sent-transact-sql.md)   
 [sp_monitor&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [시스템 통계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
