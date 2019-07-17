---
title: MSSQL_ENG021330 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021330 error
ms.assetid: e2bb2e21-62a7-4689-b68b-bdfba3fdd985
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 84a01d34e8158d69eb00618cd02ebd1b9923a115
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54126625"
---
# <a name="mssqleng021330"></a>MSSQL_ENG021330
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
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
 이 오류는 구독을 수동으로 초기화하는 경우와 복제 스크립트가 저장되는 디렉터리를 만드는 데 문제가 생기는 경우에 발생할 수 있습니다. 이 오류는 권한 문제로 인해 발생할 수도 있습니다. 예를 들어 스냅샷을 사용하지 않고 구독을 초기화할 경우 게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 실행하는 계정에는 배포자의 스냅샷 폴더에 대한 쓰기 권한이 있어야 합니다.  
  
## <a name="user-action"></a>사용자 동작  
 스냅샷 폴더에 대해 올바른 경로가 지정되었는지 확인하고 게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 실행하는 계정에 충분한 사용 권한이 있는지 확인하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [스냅숏 옵션 수정](../../relational-databases/replication/snapshot-options.md)   
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [스냅숏 없이 트랜잭션 구독 초기화](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
