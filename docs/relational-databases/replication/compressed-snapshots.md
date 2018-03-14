---
title: "압축 스냅숏 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], compressed
- snapshot replication [SQL Server], compressed snapshots
- compressed snapshots [SQL Server replication]
ms.assetid: 979ffa7c-3a88-4e70-8cf2-b8d452fd7a7f
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ab3a2f2834bfa99c8b57b058fba0c8d8c4f3183
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="compressed-snapshots"></a>압축 스냅숏
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  스냅숏을 느린 네트워크를 통해 전송하거나 이동식 미디어에 저장할 때 압축하지 않은 스냅숏이 너무 커서 해당 미디어에 모두 저장할 수 없는 경우 스냅숏 파일을 압축하는 것이 좋습니다. 위와 같은 상황에서는 스냅숏 파일을 압축하는 것이 유용하지만 압축으로 인해 스냅숏 생성과 적용에 더 많은 시간이 걸립니다.  
  
 압축 스냅숏 파일은 2GB 이하의 파일만 압축할 수 있는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 파일 형식으로 작성됩니다. 스냅숏 파일이 2GB보다 크면 압축할 수 없습니다. 파일을 압축하려면 해당 파일을 대체 스냅숏 폴더에 기록해야 합니다. 기본 스냅숏 폴더에 기록한 파일은 압축할 수 없습니다. 대체 스냅숏 폴더에 대한 자세한 내용은 [대체 스냅숏 폴더 위치](../../relational-databases/replication/alternate-snapshot-folder-locations.md)를 참조하세요.  
  
 압축 파일은 배포 에이전트 또는 병합 에이전트가 실행되는 위치에 풀립니다. 압축 파일이 구독자에 풀리도록 압축 스냅숏에는 일반적으로 끌어오기 구독이 사용됩니다. 구독자가 압축 파일을 받으면 이 파일은 일단 임시 위치에 기록됩니다. 압축 파일을 구독자로 복사하고 나면 CAB 유틸리티에 의해 한 번에 한 파일씩 순서대로 파일의 압축이 해제됩니다. 구독자에 필요한 공간은 압축 스냅숏 파일에 가장 큰 압축 해제 파일의 크기를 더한 값입니다.  
  
> [!NOTE]  
>  스냅숏을 압축하면 네트워크에서의 스냅숏 파일 전송 성능이 향상되는 경우도 있습니다. 그러나 스냅숏 에이전트에서 스냅숏 파일을 생성하는 경우와 배포 에이전트 또는 병합 에이전트에서 스냅숏 파일을 적용하는 경우에 스냅숏 파일을 압축하려면 추가 처리 작업이 필요합니다. 이 경우 스냅숏 생성 속도가 느려지거나 스냅숏 적용 시간이 늘어날 수 있습니다. 또한 네트워크 오류가 발생하면 압축 스냅숏은 재개할 수 없으므로 불안정한 네트워크에서는 압축 스냅숏이 적합하지 않습니다. 네트워크에서 압축 스냅숏을 사용하는 경우 이러한 장단점을 신중하게 고려하여 균형을 맞추는 것이 좋습니다.  
  
 **스냅숏 파일을 압축하여 배달하려면**  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [스냅숏 파일 압축 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/publish/compress-snapshot-files-sql-server-management-studio.md)  
  
-   복제 [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로그래밍: [스냅숏 속성 구성&#40;복제 TRANSACT-SQL 프로그래밍&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>참고 항목  
 [스냅숏으로 구독 초기화](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [스냅숏 옵션](../../relational-databases/replication/snapshot-options.md)  
  
  
