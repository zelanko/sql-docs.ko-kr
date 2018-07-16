---
title: 병합 테이블 아티클 (복제 TRANSACT-SQL 프로그래밍)의 처리 순서 지정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
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
caps.latest.revision: 32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c2327f90e3ff8b8ad33d7766fec48596d4461611
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299942"
---
# <a name="specify-the-processing-order-of-merge-table-articles-replication-transact-sql-programming"></a>병합 테이블 아티클에 대한 처리 순서 지정(복제 Transact-SQL 프로그래밍)
  병합 복제를 사용하면 동기화 프로세스 중에 병합 에이전트에서 아티클을 처리하는 순서를 지정할 수 있습니다. 아티클을 작성할 때 복제 저장 프로시저를 사용하여 각 아티클 순서를 프로그래밍 방식으로 할당할 수 있습니다. 아티클은 최하위에서 최상위의 순서로 처리됩니다. 두 아티클의 값이 같으면 동시에 처리됩니다. 자세한 내용은 [병합 아티클의 처리 순서 지정](../merge/specify-the-processing-order-of-merge-articles.md)을 참조하세요.  
  
### <a name="to-specify-the-processing-order-for-a-new-merge-article"></a>새 병합 아티클의 처리 순서를 지정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addmergearticle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)을 실행합니다. 이때 **@processing_order**을 참조하세요. 자세한 내용은 [아티클을 정의](define-an-article.md)을 참조하세요.  
  
    > [!NOTE]  
    >  정렬된 아티클을 만들려면 아티클 순서 값 사이에 간격을 두어야 합니다. 그러면 나중에 새 값을 쉽게 설정할 수 있습니다. 예를 들어 3개 아티클의 고정 처리 순서를 지정해야 하는 경우 **@processing_order** 값을 각각 1, 2, 3이 아닌 10, 20, 30으로 설정합니다.  
  
### <a name="to-change-the-processing-order-of-a-merge-article"></a>병합 아티클의 처리 순서를 변경하려면  
  
1.  아티클의 처리 순서를 결정하려면 [sp_helpmergearticle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)을 실행하고 결과 집합에서 **processing_order** 값을 확인합니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_changemergearticle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)을 실행합니다. 이때 **processing_order** 에 **@property** 값을 지정하고 **@value**을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [병합 아티클의 처리 순서 지정](../merge/specify-the-processing-order-of-merge-articles.md)  
  
  
