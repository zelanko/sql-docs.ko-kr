---
title: "MSSQLSERVER_125 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- "125"
helpviewer_keywords:
- 125 (Database Engine error)
ms.assetid: 0f58338d-2ea0-48b8-8a20-c438b0940433
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c311a94b0af4c36fbcdfc4abefdc175752d5addf
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver125"></a>MSSQLSERVER_125
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|125|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름||  
|메시지 텍스트|CASE 식은 수준 %d까지만 중첩할 수 있습니다.|  
  
## <a name="explanation"></a>설명  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 CASE 식의 중첩을 10개 수준까지만 허용합니다.  
  
## <a name="user-action"></a>사용자 동작  
CASE 문의 수준을 10개 이하로 줄입니다.  
  
## <a name="see-also"></a>참고 항목  
[CASE&#40;Transact-SQL&#41;](~/t-sql/language-elements/case-transact-sql.md)  
  

