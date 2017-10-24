---
title: CURRENT_REQUEST_ID (Transact SQL) | Microsoft Docs
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
- CURRENT_REQUEST_ID_TSQL
- CURRENT_REQUEST_ID
dev_langs:
- TSQL
helpviewer_keywords:
- CURRENT_REQUEST_ID
ms.assetid: 949f6e5f-bf5f-49d6-a763-c443d1d51fe2
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 606597ee99c8939d7e0cb098f7279402c0f512af
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="currentrequestid-transact-sql"></a>CURRENT_REQUEST_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

현재 세션 내 현재 요청의 ID를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CURRENT_REQUEST_ID()  
```  
  
## <a name="return-types"></a>반환 형식
**smallint**
  
## <a name="remarks"></a>주의  
현재 세션 및 현재 요청에 대 한 정확한 정보를 찾기 위해 사용 하 여@SPID 및 current_request_id (), 각각.
  
## <a name="see-also"></a>참고 항목
[@@SPID&#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md)
  
  

