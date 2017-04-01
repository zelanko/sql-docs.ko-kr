---
title: "논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "병합 복제 논리적 레코드 [SQL Server 복제]"
  - "아티클, [SQL Server 복제], 논리적 레코드"
  - "논리적 레코드 [SQL Server 복제]"
ms.assetid: ad76799c-4486-4b98-9705-005433041321
caps.latest.revision: 55
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 55
---
# 논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 기본적으로 병합 복제는 행 단위로 데이터 변경 내용을 처리합니다. 대부분의 경우 이 방법이 적합하지만 일부 응용 프로그램에서는 관련된 행을 하나의 단위로 처리해야 합니다. 병합 복제의 논리적 레코드 기능을 사용하면 서로 다른 테이블에 있는 관련 행 간의 관계를 정의하여 이러한 행을 하나의 단위로 처리할 수 있습니다.  
  
> [!NOTE]  
>  논리적 레코드 기능은 단독으로 사용되거나 조인 필터와 함께 사용될 수 있습니다. 조인 필터에 대 한 자세한 내용은 참조 [조인 필터](../../../relational-databases/replication/merge/join-filters.md)합니다. 논리적 레코드를 사용하려면 게시의 호환성 수준이 적어도 90RTM 이상이어야 합니다.  
  
 다음과 같은 3개의 관련된 테이블을 살펴보십시오.  
  
 ![열 이름만 포함하는 3개의 테이블 논리 레코드](../../../relational-databases/replication/merge/media/logical-records-01.gif "열 이름만 포함하는 3개의 테이블 논리 레코드")  
  
 이 관계의 부모 테이블인 **Customers** 테이블에는 기본 키 열 **CustID**가 있습니다. **Orders** 테이블에는 기본 키 열 **OrderID**가 있으며 **Customers** 테이블의 **CustID** 열을 참조하는 FOREIGN KEY 제약 조건이 이 테이블의 **CustID** 열에 있습니다. 마찬가지로 **OrderItems** 테이블에는 기본 키 열 **OrderItemID**가 있으며 **Orders** 테이블의 **OrderID** 열을 참조하는 FOREIGN KEY 제약 조건이 이 테이블의 **OrderID** 열에 있습니다.  
  
 이 예에서 논리적 레코드는 단일 **CustID** 값에 관련된 **Orders** 테이블의 모든 행 및 **Orders** 테이블의 해당 행과 관련된 **OrderItems** 테이블의 모든 행으로 구성되어 있습니다. 이 다이어그램에서는 Customer2에 대한 논리적 레코드에 있는 3개 테이블의 모든 행을 보여 줍니다.  
  
 ![값을 포함하는 3개의 테이블 논리 레코드](../../../relational-databases/replication/merge/media/logical-records-02.gif "값을 포함하는 3개의 테이블 논리 레코드")  
  
 아티클 간 논리적 레코드 관계를 정의하려면 [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)를 참조하십시오.  
  
## 논리적 레코드의 장점  
 논리적 레코드 기능에는 다음과 같은 두 가지 주요 장점이 있습니다.  
  
-   데이터 변경 내용을 하나의 단위로 적용  
  
-   여러 테이블의 여러 행에서 동시에 충돌 감지 및 해결  
  
### 변경 내용을 하나의 단위로 적용  
 연결이 끊기는 경우와 같이 병합 프로세스가 중단되는 경우 논리적 레코드를 사용하면 관련 복제된 변경 내용 중 부분적으로 완료된 변경 내용 집합이 롤백됩니다. 예를 들어 구독자 인 새 주문과 추가 하는 경우 **OrderID** = 6 및 두 개의 새 행에는 **OrderItems** 테이블에 **OrderItemID** = 10 및 **OrderItemID** = 11 **OrderID** = 6입니다.  
  
 ![값을 포함하는 3개의 테이블 논리 레코드](../../../relational-databases/replication/merge/media/logical-records-04.gif "값을 포함하는 3개의 테이블 논리 레코드")  
  
 다음 복제 프로세스가 중단 되는 경우는 **주문** 에 대 한 행 **OrderID** = 6 하기 전에 완료 되는 **OrderItems** 10 및 11이 완료 되 면 및 논리적 레코드 사용 되지 않는 **OrderTotal** 에 대 한 값 **OrderID** = 6의 합계와 일치 되지 것입니다는 **OrderAmount** 에 대 한 값는 **OrderItems** 행. 논리적 레코드를 사용 하는 경우는 **주문** 행 **OrderID** = 6 관련 될 때까지 커밋되지 않습니다 **OrderItems** 변경 내용이 복제 됩니다.  
  
 다른 시나리오에서 논리적 레코드가 사용되고 병합 프로세스가 변경 내용을 적용하는 동안 다른 사용자가 테이블을 쿼리하는 경우 부분적으로 복제된 변경 내용은 모두 완료될 때까지 사용자에게 표시되지 않습니다. 복제 프로세스에 대 한 Orders 행을 업로드 하는 예를 들어 **OrderID** = 6에는 사용자 쿼리의 테이블 복제 프로세스에 복제 되기 전에 **OrderItems** 행의 **OrderTotal** 값 됩니다의 합계와 동일한는 **OrderAmount** 값입니다. 논리적 레코드가 사용되는 경우 **OrderItems** 행이 완료되고 트랜잭션이 하나의 단위로 커밋될 때까지 **Orders** 행이 표시되지 않습니다.  
  
### 둘 이상의 테이블에 대한 충돌 처리 적용  
 두 구독자에 위의 데이터 집합이 있는 경우를 살펴봅시다.  
  
-   첫 번째 구독자의 사용자가 **OrderItemID** 5의 **OrderAmount** 를 100에서 150으로 변경하고 **OrderID** 3의 **OrderTotal** 을 200에서 250으로 변경합니다.  
  
-   두 번째 구독자의 사용자가 **OrderItemID** 6의 **OrderAmount** 를 25에서 125로 변경하고 **OrderID** 3의 **OrderTotal** 을 200에서 300으로 변경합니다.  
  
 이러한 변경 내용을 논리적 레코드를 사용하지 않고 복제하면 서로 다른 **OrderTotal** 값으로 인해 충돌이 발생하고 둘 중 하나만 복제됩니다. 하지만 충돌 하지 않는 변경은 **OrderItems** 테이블의 최종 충돌 없이 복제 되 **OrderTotal** 기준으로 일관 되지 않은 상태의 값은 **OrderItems** 행 합니다. 이 시나리오에서 논리적 레코드를 사용하면 **Orders** 테이블의 무시되는 변경 내용과 연결된 **OrderItems** 의 변경 내용도 롤백되므로 **OrderTotal** 의 최종값이 **OrderItems** 행의 합계와 일치하게 됩니다.  
  
 충돌 감지 및 해결 논리 레코드와 관련 된 옵션에 대 한 자세한 내용은 참조 [검색 및 논리적 레코드에서 충돌 해결](../../../relational-databases/replication/merge/detecting-and-resolving-conflicts-in-logical-records.md)합니다.  
  
## 논리적 레코드 사용 시 고려 사항  
 논리적 레코드 사용 시 다음 사항을 고려하십시오.  
  
### 일반적인 고려 사항  
  
-   논리적 레코드의 테이블 수는 적을수록 좋으므로 테이블 수를 5개 이하로 유지합니다.  
  
-   논리적 레코드는 다음 데이터 형식의 열은 참조할 수 없습니다.  
  
    -   **varchar (max)** 및 **nvarchar (max)**  
  
    -   **varbinary(max)**  
  
    -   **text** 및 **ntext**  
  
    -   **image**  
  
    -   **XML**  
  
    -   **UDT**  
  
-   게시된 테이블의 외래 키 관계는 CASCADE 옵션으로 정의할 수 없습니다. 자세한 내용은 참조 [CREATE TABLE & #40; TRANSACT-SQL & #41;](../../../t-sql/statements/create-table-transact-sql.md) 및 [테이블 & #40; ALTER TRANSACT-SQL & #41;](../../../t-sql/statements/alter-table-transact-sql.md)합니다.  
  
-   논리적 관계 절에 사용되는 열은 업데이트할 수 없습니다.  
  
-   논리적 레코드에 포함된 아티클에 대해서는 비즈니스 논리 처리기 또는 사용자 지정 해결 프로그램을 사용하는 사용자 지정 충돌 해결이 지원되지 않습니다.  
  
-   매개 변수가 있는 필터를 포함하는 게시에서 논리적 레코드를 사용하는 경우에는 각 구독자를 해당 파티션에 대한 스냅숏으로 초기화해야 합니다. 다른 방법으로 구독자를 초기화하면 병합 에이전트는 실패합니다. 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)을 참조하세요.  
  
-   논리적 레코드와 관련된 충돌은 충돌 뷰어에 표시되지 않습니다. 이러한 충돌에 대한 정보를 보려면 복제 저장 프로시저를 사용합니다. 자세한 내용은 참조 [병합 게시 및 #40;에 대 한 충돌 정보 보기 복제 TRANSACT-SQL 프로그래밍 & #41;](../../../relational-databases/replication/view conflict information for merge publications.md)합니다.  
  
### 게시 설정  
  
-   게시의 호환성 수준은 90RTM 이상이어야 합니다. 자세한 내용은의 "게시 호환성 수준" 섹션을 참조 하십시오. [복제 이전 버전과 호환성](../../../relational-databases/replication/replication-backward-compatibility.md)합니다.  
  
-   게시는 기본 스냅숏 모드를 사용해야 합니다. 논리적 레코드를 지원하지 않는 [!INCLUDE[ssEW](../../../includes/ssew-md.md)]에 복제하지 않는 한 기본 스냅숏 모드가 기본값입니다.  
  
-   게시는 웹 동기화를 허용할 수 없습니다. 웹 동기화에 대한 자세한 내용은 [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md)를 참조하십시오.  
  
-   필터링된 게시에 논리적 레코드를 사용하려면 다음을 준수하십시오.  
  
    -   사전 계산 파티션도 사용해야 합니다. 이때 사전 계산 파티션의 요구 사항도 논리적 레코드에 적용됩니다. 자세한 내용은 참조 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md)합니다.  
  
    -   겹치지 않는 매개 변수가 있는 필터는 사용할 수 없습니다. 자세한 내용은 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)의 "'partition options' 설정" 섹션을 참조하십시오.  
  
-   게시에서 조인 필터를 사용하는 경우 논리적 레코드 관계에 관련된 모든 조인 필터에 대해 **join unique key** 속성을 **true** 로 설정해야 합니다. 자세한 내용은 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)을 참조하세요.  
  
### 테이블 간 관계  
  
-   논리적 레코드를 통해 관련된 테이블에는 기본 키-외래 키 관계가 있어야 합니다.  
  
-   FOREIGN KEY 제약 조건에 대해서는 NOT FOR REPLICATION 옵션을 설정할 수 없습니다.  
  
-   자식 테이블에는 부모 테이블이 하나만 있을 수 있습니다.  
  
     예를 들어 수업 및 학생 데이터를 추적하는 데이터베이스는 다음과 같습니다.  
  
     ![둘 이상의 부모 테이블이 있는 자식 테이블](../../../relational-databases/replication/merge/media/logical-records-03.gif "둘 이상의 부모 테이블이 있는 자식 테이블")  
  
     **ClassMembers** 의 행이 기본 키 행과 연결되어 있지 않았기 때문에 논리적 레코드를 사용하여 이 관계에 있는 3개의 테이블을 나타낼 수 없습니다. **ClassMembers** 테이블과 **Students** 테이블 간에 논리적 레코드를 만들 수 있듯이 **Classes** 테이블과 **ClassMembers**테이블 간에도 논리적 레코드를 만들 수 있지만 이 3개의 테이블 간에는 논리적 레코드를 만들 수 없습니다.  
  
-   게시에는 순환 조인 필터 관계가 포함될 수 없습니다.  
  
     **Customers**, **Orders**및 **OrderItems**테이블의 예를 들면 **Orders** 테이블에도 **OrderItems** 테이블을 참조하는 FOREIGN KEY 제약 조건이 있는 경우에는 논리적 레코드를 사용할 수 없습니다.  
  
## 논리적 레코드가 성능에 미치는 영향  
 논리적 레코드 기능을 사용하면 성능이 다소 떨어집니다. 논리적 레코드를 사용하지 않는 경우 복제 에이전트는 지정된 아티클에 대한 모든 변경 내용을 동시에 처리할 수 있으며 변경 내용이 행 단위로 적용되므로 변경 내용 적용에 대해 최소의 잠금 및 트랜잭션 로그 요구 사항만 필요합니다.  
  
 논리적 레코드를 사용하는 경우 복제 에이전트는 각각의 전체 논리적 레코드에 대한 변경 내용을 한 번에 처리해야 합니다. 이 방식은 병합 에이전트가 행을 복제하는 데 걸리는 시간에 영향을 미칩니다. 또한 에이전트가 각 논리적 레코드에 대해 별도의 트랜잭션을 열기 때문에 잠금 요구 사항이 증가할 수 있습니다.  
  
## 참고 항목  
 [병합 복제를 위한 아티클 옵션](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)  
  
  