---
title: "Oracle 게시자에 대한 관리 고려 사항 | Microsoft 문서"
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
- Oracle publishing [SQL Server replication], administrative considerations
- administering replication, Oracle publishing
ms.assetid: cfd81fb5-419b-4a1b-97c4-be7c9d4ee289
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 058c10375ed15b5375f814199a57d032c5291018
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="administrative-considerations-for-oracle-publishers"></a>Oracle 게시자에 대한 관리 고려 사항
  Oracle 게시자를 구성하고 복제 변경 내용 추적 메커니즘을 설정한 후에도 Oracle 데이터베이스 시스템의 관리자는 표준 Oracle 데이터베이스 유틸리티를 사용하고 일반 시스템 관리 태스크를 수행할 수 있습니다. 그러나 특정 관리 태스크 수행 시 게시된 데이터에 미치는 영향을 알아두어야 합니다.  
  
 복제에 대해 게시된 열을 삭제 또는 수정하거나 복제 개체를 삭제 또는 수정하는 경우를 제외하고 다음 고려 사항은 스냅숏 게시에 적용되지 않습니다.  
  
## <a name="importing-and-loading-data"></a>데이터 가져오기 및 로드  
 트리거는 Oracle의 트랜잭션 게시에 대한 변경 내용 추적에 사용됩니다. 게시된 테이블에 대한 변경 내용은 업데이트, 삽입 또는 삭제가 발생할 때 복제 트리거가 실행되는 경우에만 구독자로 복제될 수 있습니다. Oracle 유틸리티인 Oracle Import 및 SQL*Loader에는 모두 이러한 유틸리티를 사용하여 복제된 테이블에 행을 삽입할 때 트리거의 발생 여부에 영향을 주는 옵션이 있습니다.  
  
### <a name="oracle-import"></a>Oracle Import  
 Oracle Import에서는 **ignore** 옵션을 'y' 또는 'n'으로 설정할 수 있습니다(기본값: 'n'). **ignore** 를 'n'으로 설정하면 가져오기 작업을 수행하는 동안 테이블이 삭제되고 다시 생성됩니다. 이렇게 하면 복제 트리거가 제거되고 복제는 해제됩니다. **ignore** 를 'y'로 설정하면 가져오기 작업에서 행을 기존 테이블로 로드하려고 하며 이로 인해 복제 트리거가 발생됩니다. 그러므로 가져오기 도구를 사용하여 복제된 테이블로 가져올 때는 **ignore** 를 'y'로 설정해야 합니다.  
  
### <a name="sqlloader"></a>SQL*Loader  
 SQL\*Loader에서는 **direct** 옵션을 'true' 또는 'false'로 설정할 수 있습니다(기본값: 'false'). **direct** 를 'false'로 설정하면 기존 INSERT 문을 사용하여 행이 삽입되고 이로 인해 복제 트리거가 발생됩니다. **direct** 를 'true'로 설정하면 로드는 최적화되지만 트리거가 발생되지 않습니다. 그러므로 SQL*Loader 도구를 사용하여 복제된 테이블로 로드할 때는 **direct** 를 'false'로 설정해야 합니다.  
  
## <a name="making-changes-to-published-objects"></a>게시된 개체 변경  
 다음 동작을 수행할 때 특별히 고려할 사항은 없습니다.  
  
-   게시된 테이블에 인덱스 다시 작성  
  
-   게시된 테이블에 사용자 트리거 추가  
  
 다음 동작을 수행하려면 게시된 테이블에서의 모든 활동을 중지해야 합니다.  
  
-   게시된 테이블 이동  
  
 다음 동작을 수행하려면 게시를 삭제하고 작업을 수행한 다음 게시를 다시 만들어야 합니다.  
  
-   게시된 테이블 잘라내기  
  
-   게시된 테이블의 이름 바꾸기  
  
-   게시된 테이블에 열 추가  
  
-   복제에 대해 게시된 열 삭제 또는 수정  
  
-   로그되지 않는 작업 수행  
  
## <a name="dropping-or-modifying-replication-objects"></a>복제 개체 삭제 또는 수정  
 게시자 수준의 추적 테이블, 트리거, 시퀀스 또는 저장 프로시저를 삭제하거나 수정할 경우 게시자를 삭제하고 다시 구성해야 합니다. 이러한 개체의 일부 목록을 보려면 [Oracle 게시자에 생성되는 개체](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)를 참조하세요.  
  
 게시자를 삭제 및 다시 구성하는 방법은 [Troubleshooting Oracle Publishers](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)항목의 "게시자를 다시 구성해야 하는 변경 내용이 적용되었습니다" 섹션을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [Oracle 게시자 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle 게시자에 대한 디자인 고려 사항 및 제한 사항](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
