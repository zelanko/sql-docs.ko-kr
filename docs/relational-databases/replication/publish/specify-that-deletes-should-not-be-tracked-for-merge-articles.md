---
title: "병합 아티클에 대해 삭제가 추적되지 않도록 지정 | Microsoft 문서"
ms.custom: 
ms.date: 03/07/2017
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
dev_langs:
- TSQL
helpviewer_keywords:
- conditional delete tracking [SQL Server replication]
- merge replication [SQL Server replication], conditional delete tracking
ms.assetid: 0fe330ca-5fb5-422e-ad6f-92fb5d6a3b6c
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d4c6b6a295d40d9a1a5e161bf10d5a61648e49eb
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="specify-that-deletes-should-not-be-tracked-for-merge-articles"></a>병합 아티클에 대해 삭제가 추적되지 않도록 지정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 기본적으로 병합 복제는 게시자와 구독자 간에 DELETE 명령을 동기화합니다. 병합 복제에서는 행을 게시에서 삭제한 경우에도 구독 데이터베이스에는 그대로 유지할 수 있으며 반대의 경우도 마찬가지입니다. 새 아티클을 만들 때 DELETE 명령을 무시할지 여부를 프로그래밍 방식으로 지정할 수 있으며 복제 저장 프로시저를 사용하여 이 기능을 나중에 활성화할 수도 있습니다.  
  
> [!IMPORTANT]  
>  이 기능을 활성화하면 불일치가 발생합니다. 이는 구독자에 있는 데이터가 게시자에 있는 데이터를 정확하게 반영하지 않음을 의미합니다. 이 경우 삭제된 행을 수동으로 제거하기 위한 메커니즘을 직접 구현해야 합니다.  
  
### <a name="to-specify-that-deletes-be-ignored-for-a-new-merge-article"></a>새 병합 아티클에 대해 삭제가 무시되도록 지정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addmergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행합니다. **@delete_tracking**에 **false** 값을 지정합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
    > [!NOTE]  
    >  아티클의 원본 테이블이 이미 다른 게시에 게시된 경우 **delete_tracking** 값은 두 아티클에 대해 동일해야 합니다.  
  
### <a name="to-specify-that-deletes-be-ignored-for-an-existing-merge-article"></a>기존 병합 아티클에 대해 삭제가 무시되도록 지정하려면  
  
1.  아티클에 대해 오류 보정이 설정되어 있는지 확인하려면 [sp_helpmergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)을 실행하고 결과 집합에서 **delete_tracking**의 값을 확인합니다. 이 값이 **0**이면 삭제가 이미 무시되고 있는 것입니다.  
  
2.  1단계의 값이 **1**이면 게시 데이터베이스의 게시자에서 [sp_changemergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)을 실행합니다. **@property**에 **delete_tracking** 값, **@value**에 **false** 값을 지정합니다.  
  
    > [!NOTE]  
    >  아티클의 원본 테이블이 이미 다른 게시에 게시된 경우 **delete_tracking** 값은 두 아티클에 대해 동일해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [조건부 삭제 추적으로 병합 복제 성능 최적화](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  
