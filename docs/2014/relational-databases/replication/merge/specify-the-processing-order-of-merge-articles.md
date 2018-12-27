---
title: 병합 아티클의 처리 순서 지정 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], processing order
- merge replication [SQL Server replication], article processing order
ms.assetid: d151e2c5-cf50-4cb3-a829-8f32455dbd66
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 569767e74c6666a68b41b5af9914a5a028522bc1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48174053"
---
# <a name="specify-the-processing-order-of-merge-articles"></a>병합 아티클의 처리 순서 지정
   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]부터 병합 게시에 대한 아티클의 기본 처리 순서를 덮어쓸 수 있게 되었습니다. 트리거를 통해 참조 무결성을 정의하고 이러한 트리거가 특정 순서로 발생해야 할 경우 이러한 작업이 유용할 수 있습니다.  
  
 **아티클의 처리 순서를 지정하려면**  
  
-   복제 Transact-SQL 프로그래밍: [병합 테이블 아티클의 처리 순서 지정&#40;복제 Transact-SQL 프로그래밍&#41;](../publish/specify-the-processing-order-of-merge-table-articles.md)  
  
## <a name="how-processing-order-is-determined"></a>처리 순서 결정 방식  
 병합 동기화 중 아티클은 기본적으로 기본 테이블에 정의된 DRI(선언적 참조 무결성) 제약 조건을 포함하여 개체 간 종속 관계에 필요한 순서대로 처리됩니다. 아티클 처리 시 테이블에 변경 내용을 열거한 다음 이들 변경 내용을 적용합니다. DRI가 없지만 조인 필터 또는 논리적 레코드가 테이블 아티클 사이에 존재할 경우 아티클은 필터 및 논리적 레코드에 필요한 순서대로 처리됩니다. DRI, 조인 필터, 논리적 레코드 또는 기타 종속 관계를 통해 다른 아티클과 관련되어 있지 않은 아티클은 [sysmergearticles&#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysmergearticles-transact-sql) 시스템 테이블에서의 아티클 애칭에 따라 처리됩니다.  
  
 **SalesOrderHeader** 테이블에는 기본 키 열 **SalesOrderID** 가 있고 **SalesOrderDetail** 테이블에는 해당 외래 키 열 **SalesOrderID** 가 있는 **SalesOrderHeader** 및 **SalesOrderDetail** 테이블을 포함하는 게시가 있다고 가정합니다. 이 게시를 동기화할 때 병합 복제에서 **SalesOrderHeader** 에 새 행을 삽입한 다음 **SalesOrderDetail**에 연결된 행을 삽입하여 외래 키 위반을 방지합니다. 마찬가지로 **SalesOrderDetail** 에서 행을 삭제한 다음 **SalesOrderHeader**에서 연결된 행을 삭제합니다.  
  
 그러나 일부 애플리케이션에서는 DRI가 아닌 애플리케이션 수준에서나 데이터베이스 트리거를 통해 참조 무결성이 적용됩니다. DRI 대신 위에서 설명한 게시를 제공한 경우 **SalesOrderDetail** 테이블에는 삽입을 허용하기 전에 **SalesOrderHeader** 테이블에 연결된 행이 존재하도록 하는 삽입 트리거가 있을 수 있습니다. **SalesOrderHeader** 에는 삭제를 허용하기 전에 **SalesOrderDetail** 에 연결된 행이 없도록 하는 삭제 트리거가 있을 수 있습니다. 병합 복제는 트리거가 발생될 때까지 트리거의 결과를 확인할 수 없으므로 아티클의 처리 순서를 결정할 때 트리거를 고려하지 않습니다. 마찬가지로 복제는 애플리케이션 수준에서 정의된 제약 조건을 고려할 수 없습니다.  
  
 참조 무결성이 트리거를 통해서 또는 애플리케이션 수준에서 유지 관리되는 경우 아티클이 처리되는 순서를 지정해야 합니다. 트리거가 있는 예제에서 아티클 순서는 삽입 순서에 따라 지정되므로 **SalesOrderDetail** 전에 **SalesOrderHeader**테이블이 처리되도록 지정합니다. 병합 복제는 삭제 순서를 자동으로 반대로 바꿉니다. 병합 에이전트는 제약 조건 위반이 발생해도 아티클을 계속 처리하고 다른 아티클이 처리된 후 실패한 작업을 모두 다시 시도하므로 병합 복제는 아티클 순서를 지정하지 않아도 실패하지 않습니다. 아티클 순서를 지정하면 다시 시도 및 다시 시도와 연결된 추가 처리 작업이 실행되지 않도록 할 수 있습니다. 헤더 레코드 전에 정보 레코드가 처리되도록 하는 등 순서를 잘못 지정하면 병합 복제는 성공할 때까지 처리를 다시 시도합니다.  
  
## <a name="see-also"></a>관련 항목  
 [병합 복제를 위한 아티클 옵션](article-options-for-merge-replication.md)   
 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](group-changes-to-related-rows-with-logical-records.md)   
 [Join Filters](join-filters.md)  
  
  
