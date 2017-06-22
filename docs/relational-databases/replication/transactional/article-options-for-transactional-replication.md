---
title: "트랜잭션 복제를 위한 아티클 옵션 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- articles [SQL Server replication], transactional replication options
- transactional replication, article options
ms.assetid: 3469b185-0ea5-4690-a71c-717230d886b6
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bf9a9b2f8e6d250c313990c384651f0464db777e
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="article-options-for-transactional-replication"></a>트랜잭션 복제를 위한 아티클 옵션
  트랜잭션 게시의 아티클에는 여러 가지 옵션이 있습니다. 트랜잭션 복제를 사용하여 다음 작업을 수행할 수 있습니다.  
  
-   게시자에서 구독자로 변경 내용이 전파되는 방법을 지정합니다. 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.  
  
-   저장 프로시저의 실행 결과를 복제하도록 지정합니다. 이는 많은 데이터에 영향을 주는 유지 관리 관련 저장 프로시저의 결과를 복제할 때 유용합니다. 자세한 내용은 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)을(를) 참조하세요.  
  
-   제약 조건 및 트리거를 구독자로 복사할지 여부와 같은 스키마 옵션을 지정합니다. 자세한 내용은 [스키마 옵션 지정](../../../relational-databases/replication/publish/specify-schema-options.md)을 참조하세요.  
  
-   행 필터와 열 필터를 사용합니다. 테이블 아티클을 필터링하여 게시할 데이터 파티션을 만들 수 있습니다. 자세한 내용은 [게시된 데이터 필터링](../../../relational-databases/replication/publish/filter-published-data.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
