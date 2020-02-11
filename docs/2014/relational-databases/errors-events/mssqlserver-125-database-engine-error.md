---
title: MSSQLSERVER_125 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "125"
helpviewer_keywords:
- 125 (Database Engine error)
ms.assetid: 0f58338d-2ea0-48b8-8a20-c438b0940433
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8287572d31dc136f21717ba45b730936b4fb78ae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62870460"
---
# <a name="mssqlserver_125"></a>MSSQLSERVER_125
    
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
 [CASE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/case-transact-sql)  
  
  
