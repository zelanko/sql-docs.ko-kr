---
title: CURRENT_REQUEST_ID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: deafc5812d1fd10cd036612f7d756c44f6f94685
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="currentrequestid-transact-sql"></a>CURRENT_REQUEST_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

이 함수는 현재 세션 내 현재 요청의 ID를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CURRENT_REQUEST_ID()  
```  
  
## <a name="return-types"></a>반환 형식
**smallint**
  
## <a name="remarks"></a>Remarks  
현재 세션에 대한 정확한 정보를 찾으려면 @@SPID을 사용합니다. 현재 요청에 대한 정확한 내용은 CURRENT_REQUEST_ID()를 사용합니다.
  
## <a name="see-also"></a>관련 항목:
[@@SPID&#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md)
  
  
