---
title: MSSQL_ENG020572 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020572 error
ms.assetid: 636566db-ffcf-4109-8c11-15b8c7cb9cd9
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 07bd8dfb40c9832c55b6b0d21e11f3f0684c9a54
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770407"
---
# <a name="mssqleng020572"></a>MSSQL_ENG020572
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|20572|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|게시 '%s'의 아티클 '%s'에 대한 구독자 '%s'의 구독이 유효성 검사 실패 후 다시 초기화되었습니다.|  
  
## <a name="explanation"></a>설명  
 구독자의 데이터를 게시자의 데이터와 비교하여 유효성을 검사했는데 데이터가 일치하지 않아 유효성 검사가 실패했습니다. 유효성 검사를 수행해야 함을 지정할 경우 유효성 검사가 실패하면 구독을 다시 초기화해야 한다는 옵션을 선택했습니다. 구독을 다시 초기화하면 구독자에서 새 스냅샷을 적용하게 됩니다. 유효성 검사에 대한 자세한 내용은 [Validate Replicated Data](../../relational-databases/replication/validate-data-at-the-subscriber.md)를 참조하십시오.  
  
## <a name="user-action"></a>사용자 동작  
 새 스냅샷이 구독자에 적용된 후에는 게시자와 구독자의 데이터가 일치할 것입니다.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
