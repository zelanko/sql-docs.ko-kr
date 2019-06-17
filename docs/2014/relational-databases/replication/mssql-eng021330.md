---
title: MSSQL_ENG021330 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021330 error
ms.assetid: e2bb2e21-62a7-4689-b68b-bdfba3fdd985
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e3640999842c7bd61c368bf967f74183f5d57099
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63023388"
---
# <a name="mssqleng021330"></a>MSSQL_ENG021330
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21330|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|복제 작업 디렉터리(%ls)에 하위 디렉터리를 만들지 못했습니다.|  
  
## <a name="explanation"></a>설명  
 이 오류는 구독을 수동으로 초기화하는 경우와 복제 스크립트가 저장되는 디렉터리를 만드는 데 문제가 생기는 경우에 발생할 수 있습니다. 이 오류는 권한 문제로 인해 발생할 수도 있습니다. 예를 들어 스냅숏을 사용하지 않고 구독을 초기화할 경우 게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 실행하는 계정에는 배포자의 스냅숏 폴더에 대한 쓰기 권한이 있어야 합니다.  
  
## <a name="user-action"></a>사용자 동작  
 스냅숏 폴더에 대해 올바른 경로가 지정되었는지 확인하고 게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 실행하는 계정에 충분한 사용 권한이 있는지 확인하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [기본 스냅숏 위치 지정](snapshot-options.md#snapshot-folder-locations)   
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)   
 [스냅숏 없이 트랜잭션 구독 초기화](initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
