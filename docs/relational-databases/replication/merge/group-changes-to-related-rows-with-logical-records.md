---
title: 논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication logical records [SQL Server replication]
- articles [SQL Server replication], logical records
- logical records [SQL Server replication]
ms.assetid: ad76799c-4486-4b98-9705-005433041321
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a4bebb60c7d40ab7d1a98bbb6c8b28ff64ea7b09
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62639403"
---
# <a name="group-changes-to-related-rows-with-logical-records"></a>논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 기본적으로 병합 복제는 행 단위로 데이터 변경 내용을 처리합니다. 대부분의 경우 이 방법이 적합하지만 일부 애플리케이션에서는 관련된 행을 하나의 단위로 처리해야 합니다. 병합 복제의 논리적 레코드 기능을 사용하면 서로 다른 테이블에 있는 관련 행 간의 관계를 정의하여 이러한 행을 하나의 단위로 처리할 수 있습니다.  
  
> [!NOTE]  
>  논리적 레코드 기능은 단독으로 사용되거나 조인 필터와 함께 사용될 수 있습니다. 조인 필터에 대한 자세한 내용은 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)를 참조하십시오. 논리적 레코드를 사용하려면 게시의 호환성 수준이 적어도 90RTM 이상이어야 합니다.  
  
 다음과 같은 3개의 관련된 테이블을 살펴보십시오.  
  
 ![열 이름만 포함하는 3개의 테이블 논리적 레코드](../../../relational-databases/replication/merge/media/logical-records-01.gif "Three table logical record, with column names only")  
  
 이 관계의 부모 테이블인 **Customers** 테이블에는 기본 키 열 **CustID**가 있습니다. **Orders** 테이블에는 기본 키 열 **OrderID**가 있으며 **Customers** 테이블의 **CustID** 열을 참조하는 FOREIGN KEY 제약 조건이 이 테이블의 **CustID** 열에 있습니다. 마찬가지로 **OrderItems** 테이블에는 기본 키 열 **OrderItemID**가 있으며 **Orders** 테이블의 **OrderID** 열을 참조하는 FOREIGN KEY 제약 조건이 이 테이블의 **OrderID** 열에 있습니다.  
  
 이 예에서 논리적 레코드는 단일 **CustID** 값에 관련된 **Orders** 테이블의 모든 행 및 **Orders** 테이블의 해당 행과 관련된 **OrderItems** 테이블의 모든 행으로 구성되어 있습니다. 이 다이어그램에서는 Customer2에 대한 논리적 레코드에 있는 3개 테이블의 모든 행을 보여 줍니다.  
  
 ![값을 포함하는 3개의 테이블 논리적 레코드](../../../relational-databases/replication/merge/media/logical-records-02.gif "Three table logical record with values")  
  
 아티클 간 논리적 레코드 관계를 정의하려면 [병합 테이블 기사 간의 논리적 레코드 관계 정의](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)를 참조하십시오.  
  
## <a name="benefits-of-logical-records"></a>논리적 레코드의 장점  
 논리적 레코드 기능에는 다음과 같은 두 가지 주요 장점이 있습니다.  
  
-   데이터 변경 내용을 하나의 단위로 적용  
  
-   여러 테이블의 여러 행에서 동시에 충돌 감지 및 해결  
  
### <a name="the-application-of-changes-as-a-unit"></a>변경 내용을 하나의 단위로 적용  
 연결이 끊기는 경우와 같이 병합 프로세스가 중단되는 경우 논리적 레코드를 사용하면 관련 복제된 변경 내용 중 부분적으로 완료된 변경 내용 집합이 롤백됩니다. 예를 들어 구독자가 **OrderID** = 6인 새 주문과 **OrderID** = 6에 대해 **OrderItemID** = 10 및 **OrderItemID** = 11인 두 개의 새 행을 **OrderItems** 테이블에 추가하는 경우를 살펴봅시다.  
  
 ![값을 포함하는 3개의 테이블 논리적 레코드](../../../relational-databases/replication/merge/media/logical-records-04.gif "Three table logical record with values")  
  
 **OrderID** = 6에 대한 **Orders** 행은 완료되었지만 **OrderItems** 10 및 11이 완료되기 전에 복제 프로세스가 중단되고 논리적 레코드가 사용되지 않는 경우 **OrderID** = 6에 대한 **OrderTotal** 값이 **OrderItems** 행에 대한 **OrderAmount** 값의 합계와 일치하지 않게 됩니다. 논리적 레코드가 사용되는 경우에는 관련 **OrderItems** 변경 내용이 복제될 때까지 **OrderID** = 6에 대한 **Orders** 행이 커밋되지 않습니다.  
  
 다른 시나리오에서 논리적 레코드가 사용되고 병합 프로세스가 변경 내용을 적용하는 동안 다른 사용자가 테이블을 쿼리하는 경우 부분적으로 복제된 변경 내용은 모두 완료될 때까지 사용자에게 표시되지 않습니다. 예를 들어 복제 프로세스가 **OrderID** = 6에 대한 Orders 행을 업로드했지만 복제 프로세스가 **OrderItems** 행을 복제하기 전에 사용자가 해당 테이블을 쿼리하는 경우 **OrderTotal** 값이 **OrderAmount** 값의 합계와 같지 않게 됩니다. 논리적 레코드가 사용되는 경우 **OrderItems** 행이 완료되고 트랜잭션이 하나의 단위로 커밋될 때까지 **Orders** 행이 표시되지 않습니다.  
  
### <a name="the-application-of-conflict-handling-to-more-than-one-table"></a>둘 이상의 테이블에 대한 충돌 처리 적용  
 두 구독자에 위의 데이터 집합이 있는 경우를 살펴봅시다.  
  
-   첫 번째 구독자의 사용자가 **OrderItemID** 5의 **OrderAmount** 를 100에서 150으로 변경하고 **OrderID** 3의 **OrderTotal** 을 200에서 250으로 변경합니다.  
  
-   두 번째 구독자의 사용자가 **OrderItemID** 6의 **OrderAmount** 를 25에서 125로 변경하고 **OrderID** 3의 **OrderTotal** 을 200에서 300으로 변경합니다.  
  
 이러한 변경 내용을 논리적 레코드를 사용하지 않고 복제하면 서로 다른 **OrderTotal** 값으로 인해 충돌이 발생하고 둘 중 하나만 복제됩니다. 그러나 **OrderItems** 테이블의 충돌하지 않는 변경 내용은 충돌 발생 없이 복제되고 **OrderTotal** 의 최종값이 **OrderItems** 행에 대해 일치하지 않게 됩니다. 이 시나리오에서 논리적 레코드를 사용하면 **Orders** 테이블의 무시되는 변경 내용과 연결된 **OrderItems** 의 변경 내용도 롤백되므로 **OrderTotal** 의 최종값이 **OrderItems** 행의 합계와 일치하게 됩니다.  
  
 논리적 레코드를 사용하는 경우의 충돌 감지 및 해결과 관련된 옵션에 대한 자세한 내용은 [논리적 레코드에서 충돌 감지 및 해결](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)을 참조하세요.  
  
## <a name="considerations-for-using-logical-records"></a>논리적 레코드 사용 시 고려 사항  
 논리적 레코드 사용 시 다음 사항을 고려하십시오.  
  
### <a name="general-considerations"></a>일반적인 고려 사항  
  
-   논리적 레코드의 테이블 수는 적을수록 좋으므로 테이블 수를 5개 이하로 유지합니다.  
  
-   논리적 레코드는 다음 데이터 형식의 열은 참조할 수 없습니다.  
  
    -   **varchar(max)** 및 **nvarchar(max)**  
  
    -   **varbinary(max)**  
  
    -   **text** 및 **ntext**  
  
    -   **image**  
  
    -   **XML**  
  
    -   **UDT**  
  
-   게시된 테이블의 외래 키 관계는 CASCADE 옵션으로 정의할 수 없습니다. 자세한 내용은 [CREATE TABLE&#40;Transact-SQL&#41;](../../../t-sql/statements/create-table-transact-sql.md) 및 [ALTER TABLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)을 참조하세요.  
  
-   논리적 관계 절에 사용되는 열은 업데이트할 수 없습니다.  
  
-   논리적 레코드에 포함된 아티클에 대해서는 비즈니스 논리 처리기 또는 사용자 지정 해결 프로그램을 사용하는 사용자 지정 충돌 해결이 지원되지 않습니다.  
  
-   매개 변수가 있는 필터를 포함하는 게시에서 논리적 레코드를 사용하는 경우에는 각 구독자를 해당 파티션에 대한 스냅숏으로 초기화해야 합니다. 다른 방법으로 구독자를 초기화하면 병합 에이전트는 실패합니다. 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을 참조하세요.  
  
-   논리적 레코드와 관련된 충돌은 충돌 뷰어에 표시되지 않습니다. 이러한 충돌에 대한 정보를 보려면 복제 저장 프로시저를 사용합니다. 자세한 내용은 [병합 게시에 대한 충돌 정보 보기&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)을 참조하세요.  
  
### <a name="publication-settings"></a>게시 설정  
  
-   게시의 호환성 수준은 90RTM 이상이어야 합니다. 자세한 내용은 [복제의 이전 버전과의 호환성](../../../relational-databases/replication/replication-backward-compatibility.md)의 "게시 호환성 수준" 섹션을 참조하세요.  
  
-   게시는 기본 스냅숏 모드를 사용해야 합니다. 논리적 레코드를 지원하지 않는 [!INCLUDE[ssEW](../../../includes/ssew-md.md)]에 복제하지 않는 한 기본 스냅숏 모드가 기본값입니다.  
  
-   게시는 웹 동기화를 허용할 수 없습니다. 웹 동기화에 대한 자세한 내용은 [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md)를 참조하십시오.  
  
-   필터링된 게시에 논리적 레코드를 사용하려면 다음을 준수하십시오.  
  
    -   사전 계산 파티션도 사용해야 합니다. 이때 사전 계산 파티션의 요구 사항도 논리적 레코드에 적용됩니다. 자세한 내용은 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)를 참조하세요.  
  
    -   겹치지 않는 매개 변수가 있는 필터는 사용할 수 없습니다. 자세한 내용은 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)의 "'partition options' 설정" 섹션을 참조하십시오.  
  
-   게시에서 조인 필터를 사용하는 경우 논리적 레코드 관계에 관련된 모든 조인 필터에 대해 **join unique key** 속성을 **true** 로 설정해야 합니다. 자세한 내용은 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)를 참조하세요.  
  
### <a name="relationships-between-tables"></a>테이블 간 관계  
  
-   논리적 레코드를 통해 관련된 테이블에는 기본 키-외래 키 관계가 있어야 합니다.  
  
-   FOREIGN KEY 제약 조건에 대해서는 NOT FOR REPLICATION 옵션을 설정할 수 없습니다.  
  
-   자식 테이블에는 부모 테이블이 하나만 있을 수 있습니다.  
  
     예를 들어 수업 및 학생 데이터를 추적하는 데이터베이스는 다음과 같습니다.  
  
     ![둘 이상의 부모 테이블이 있는 자식 테이블](../../../relational-databases/replication/merge/media/logical-records-03.gif "Child table with more than one parent table")  
  
     **ClassMembers** 의 행이 기본 키 행과 연결되어 있지 않았기 때문에 논리적 레코드를 사용하여 이 관계에 있는 3개의 테이블을 나타낼 수 없습니다. **ClassMembers** 테이블과 **Students** 테이블 간에 논리적 레코드를 만들 수 있듯이 **Classes** 테이블과 **ClassMembers**테이블 간에도 논리적 레코드를 만들 수 있지만 이 3개의 테이블 간에는 논리적 레코드를 만들 수 없습니다.  
  
-   게시에는 순환 조인 필터 관계가 포함될 수 없습니다.  
  
     **Customers**, **Orders**및 **OrderItems**테이블의 예를 들면 **Orders** 테이블에도 **OrderItems** 테이블을 참조하는 FOREIGN KEY 제약 조건이 있는 경우에는 논리적 레코드를 사용할 수 없습니다.  
  
## <a name="performance-implications-of-logical-records"></a>논리적 레코드가 성능에 미치는 영향  
 논리적 레코드 기능을 사용하면 성능이 다소 떨어집니다. 논리적 레코드를 사용하지 않는 경우 복제 에이전트는 지정된 아티클에 대한 모든 변경 내용을 동시에 처리할 수 있으며 변경 내용이 행 단위로 적용되므로 변경 내용 적용에 대해 최소의 잠금 및 트랜잭션 로그 요구 사항만 필요합니다.  
  
 논리적 레코드를 사용하는 경우 복제 에이전트는 각각의 전체 논리적 레코드에 대한 변경 내용을 한 번에 처리해야 합니다. 이 방식은 병합 에이전트가 행을 복제하는 데 걸리는 시간에 영향을 미칩니다. 또한 에이전트가 각 논리적 레코드에 대해 별도의 트랜잭션을 열기 때문에 잠금 요구 사항이 증가할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [병합 복제를 위한 아티클 옵션](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)  
  
  
