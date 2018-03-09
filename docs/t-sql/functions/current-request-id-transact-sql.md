---
title: CURRENT_REQUEST_ID (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a10b0b4f5d45cb486da414c1ed29f4996e717349
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="currentrequestid-transact-sql"></a>CURRENT_REQUEST_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
  
