---
title: MSSQL_ENG020574 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG02574 error
ms.assetid: 4e98f8de-287c-4090-81ee-dc8f80dfa6a1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4788e7696b9bb986ab5a16fb2fea618d0b996cc9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62938608"
---
# <a name="mssql_eng020574"></a>MSSQL_ENG020574
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|20574|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|게시 '%s'의 아티클 '%s'에 대한 구독자 '%s'의 구독이 데이터 유효성 검사에 실패했습니다.|  
  
## <a name="explanation"></a>설명  
 구독자의 데이터를 게시자의 데이터와 비교하여 유효성을 검사했는데 데이터가 일치하지 않아 유효성 검사가 실패했습니다. 유효성 검사에 대한 자세한 내용은 [Validate Replicated Data](validate-data-at-the-subscriber.md)를 참조하십시오.  
  
## <a name="user-action"></a>사용자 동작  
 다음을 수행하는 것이 좋습니다.  
  
-   유효성 검사 실패 원인을 확인합니다.  
  
-   실패 원인의 기본 문제를 수정합니다.  
  
-   구독을 다시 초기화하거나 다른 메서드를 통해 데이터를 일치시킵니다.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)  
  
  
