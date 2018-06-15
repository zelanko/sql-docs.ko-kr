---
title: 병합 테이블 아티클의 처리 순서 지정 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- articles [SQL Server replication], processing order
- merge replication [SQL Server replication], article processing order
ms.assetid: 9fe576a2-f5fb-4fdf-bd7d-cb322021b669
caps.latest.revision: 33
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6d0a1519c85e1b398fc4be3491b680997cac01b5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32960748"
---
# <a name="specify-the-processing-order-of-merge-table-articles"></a>병합 테이블 아티클의 처리 순서 지정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  병합 복제를 사용하면 동기화 프로세스 중에 병합 에이전트에서 아티클을 처리하는 순서를 지정할 수 있습니다. 아티클을 작성할 때 복제 저장 프로시저를 사용하여 각 아티클 순서를 프로그래밍 방식으로 할당할 수 있습니다. 아티클은 최하위에서 최상위의 순서로 처리됩니다. 두 아티클의 값이 같으면 동시에 처리됩니다. 자세한 내용은 [병합 아티클의 처리 순서 지정](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)을 참조하세요.  
  
### <a name="to-specify-the-processing-order-for-a-new-merge-article"></a>새 병합 아티클의 처리 순서를 지정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addmergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행합니다. 이때 **@processing_order**을 참조하세요. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
    > [!NOTE]  
    >  정렬된 아티클을 만들려면 아티클 순서 값 사이에 간격을 두어야 합니다. 그러면 나중에 새 값을 쉽게 설정할 수 있습니다. 예를 들어 3개 아티클의 고정 처리 순서를 지정해야 하는 경우 **@processing_order** 값을 각각 1, 2, 3이 아닌 10, 20, 30으로 설정합니다.  
  
### <a name="to-change-the-processing-order-of-a-merge-article"></a>병합 아티클의 처리 순서를 변경하려면  
  
1.  아티클의 처리 순서를 결정하려면 [sp_helpmergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)을 실행하고 결과 집합에서 **processing_order** 값을 확인합니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_changemergearticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)을 실행합니다. 이때 **processing_order** 에 **@property** 값을 지정하고 **@value**을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [병합 아티클의 처리 순서 지정](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)  
  
  
