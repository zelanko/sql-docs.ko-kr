---
title: MSSQL_ENG021331 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021331 error
ms.assetid: 9acd75d9-fda1-44cd-ba17-20295ad53ea0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 63becb9b07114b6e0ae0589664ae80d82f8babb2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63023381"
---
# <a name="mssqleng021331"></a>MSSQL_ENG021331
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21331|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|사용자 스크립트 파일을 배포자(%ls)에 복사하지 못했습니다.|  
  
## <a name="explanation"></a>설명  
 구독을 수동으로 초기화할 경우와 복제로 생성된 스크립트 또는 복제 명령에서 지정된 스크립트를 지정한 디렉터리에 저장할 수 없는 경우 이 오류가 발생할 수 있습니다. 이 오류는 권한 문제로 인해 발생할 수도 있습니다. 예를 들어 스냅숏을 사용하지 않고 구독을 초기화할 경우 게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 실행하는 계정에는 배포자의 스냅숏 폴더에 대한 쓰기 권한이 있어야 합니다.  
  
## <a name="user-action"></a>사용자 동작  
 스냅숏 폴더에 대해 올바른 경로가 지정되었는지 확인하고 게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 실행하는 계정에 충분한 사용 권한이 있는지 확인하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [기본 스냅숏 위치 지정](snapshot-options.md#snapshot-folder-locations)   
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)   
 [스냅숏 없이 트랜잭션 구독 초기화](initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
