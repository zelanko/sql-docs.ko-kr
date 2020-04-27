---
title: 새 피어 초기화(피어 투 피어 복제) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.p2pwizard.init.f1
ms.assetid: 050c00e1-78bd-4d9c-affe-40e22feb4d94
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 51e5ec3832d497f342c4fc3132a75261f6c3c154
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63022683"
---
# <a name="new-peer-initialization-peer-to-peer-replication"></a>새 피어 초기화(피어 투 피어 복제)
  **새 피어 초기화** 페이지를 사용하여 피어 데이터베이스가 초기화된 방법을 지정할 수 있습니다. 이 마법사를 완료 하기 전에 피어를 초기화 해야 합니다. 피어는 수동으로 초기화 되거나 트랜잭션 복제에서 제공 하는 **initialize with backup** 기능을 사용 하 여 초기화 됩니다. 피어 투 피어 트랜잭션 복제는 스냅숏을 사용한 피어 초기화를 지원 하지 않습니다. 다른 메서드를 사용 하 여 다른 피어를 초기화 해야 하는 경우 마법사를 여러 번 실행 하 여 개별적으로 피어를 추가 해야 합니다.  
  
## <a name="options"></a>옵션  
 **새 피어 데이터베이스가 초기화된 방법을 지정하십시오.**  
 게시된 모든 개체의 스키마와 데이터가 각 피어에 있어야 합니다. 다음 옵션 중 하나를 선택합니다.  
  
-   게시된 개체의 스키마를 수동으로 만들었거나 백업을 복원했으며 백업이 만들어진 이후 첫 번째 게시 데이터베이스에서 데이터가 변경되지 않은 경우 첫 번째 옵션을 선택합니다. 스키마를 수동으로 만든 경우 필요한 모든 데이터가 각 피어에 있는지 확인해야 합니다. 이 옵션은 구독 속성 **sync_type** 의 **replication support only**값에 해당합니다.  
  
-   백업을 복원했으며 백업이 수행된 후 첫 번째 게시 데이터베이스에서 데이터가 변경된 경우 두 번째 옵션을 선택합니다. 이제 복제에서 백업에 포함되지 않은 첫 번째 게시 데이터베이스의 변경 내용을 배달합니다. 이 옵션은 구독 속성 **sync_type** 의 **initialize with backup**값에 해당합니다.  
  
     게시에 피어 투 피어 복제를 설정하면 **allow_initialize_from_backup** 게시 속성이 설정됩니다. 복제에서 즉시 첫 번째 게시 데이터베이스의 변경 내용을 추적하기 시작하므로 **initialize with backup** 옵션을 선택하면 하나 이상의 피어에 있는 복원된 데이터베이스에 변경 내용이 배달될 수 있습니다. **찾아보기** 단추를 클릭하여 사용된 백업을 찾으면 복제 기능은 백업에서 LSN(로그 시퀀스 번호)을 읽습니다. 첫 번째 게시 데이터베이스에서 LSN이 높은 모든 변경 내용이 각 피어로 배달됩니다.  
  
     [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]가 포함된 토폴로지를 만들거나 해당 토폴로지에 추가할 경우 이 옵션을 사용하지 못할 수 있습니다. 다음 표에서는 기존 토폴로지에 노드를 추가할 때 이 옵션을 사용할 수 있는지 여부를 보여 줍니다.  
  
    |새 노드|첫 번째 노드|추가 노드|옵션|  
    |--------------|----------------|----------------------|------------|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|사용 안 함|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|없음|사용 안 함|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|사용 안 함|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|없음|사용|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|없음|사용|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|사용|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|없음|사용|  
  
## <a name="see-also"></a>참고 항목  
 [피어 투 피어 토폴로지 관리 &#40;복제 Transact-sql 프로그래밍&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [피어 투 피어 트랜잭션 복제](transactional/peer-to-peer-transactional-replication.md)  
  
  
