---
title: Integration Services 패키지의 MERGE | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- MERGE statement [SQL Server]
ms.assetid: 7e44a5c2-e6d6-4fe2-a079-4f95ccdb147b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e4b14fae3600b30c1e4f2d8fe5547533a4673242
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915409"
---
# <a name="merge-in-integration-services-packages"></a>Integration Services 패키지의 MERGE

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 현재 릴리스에서 SQL 실행 태스크의 SQL 문은 MERGE 문을 포함할 수 있습니다. 이 MERGE 문을 사용하면 하나의 문에서 여러 INSERT, UPDATE 및 DELETE 작업을 수행할 수 있습니다.  
  
 패키지에서 MERGE 문을 사용하려면 다음 단계를 따르세요.  
  
-   원본 데이터를 로드하고 변환하여 임시 또는 준비 테이블에 저장하는 데이터 흐름 태스크를 만듭니다.  
  
-   MERGE 문을 포함하는 SQL 실행 태스크를 만듭니다.  
  
-   데이터 흐름 태스크를 SQL 실행 태스크에 연결하고 준비 테이블의 데이터를 MERGE 문의 입력으로 사용합니다.  
  
    > [!NOTE]  
    >  이 시나리오의 MERGE 문에는 일반적으로 준비 테이블이 필요하지만 MERGE 문의 성능은 대개 조회 변환에 의해 수행되는 행 단위 조회보다 뛰어납니다. 또한 MERGE는 대용량 조회 테이블이 조회 변환에서 참조 테이블을 캐시하는 데 사용할 수 있는 메모리를 테스트하는 경우 유용합니다.  
  
 MERGE 문 사용을 지원하는 예제 대상 구성 요소는 CodePlex 커뮤니티 예제 [MERGE 대상(MERGE Destination)](https://go.microsoft.com/fwlink/?LinkId=141215)을 참조하세요.  
  
## <a name="using-merge"></a>MERGE 사용  
 일반적으로 삽입, 업데이트 및 삭제가 포함된 한 테이블의 변경을 다른 테이블에 적용하려는 경우 MERGE 문을 사용합니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]전에는 이 프로세스에 조회 변환과 여러 OLE DB 명령 변환이 모두 필요했습니다. 조회 변환은 행 단위로 조회를 수행하여 각 행이 새로운 행인지 변경된 행인지를 판단했습니다. 그러면 OLE DB 명령 변환이 필요한 INSERT, UPDATE 및 DELETE 작업을 수행했습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]이상에서는 하나의 MERGE 문이 조회 변환과 이에 해당하는 OLE DB 명령 변환을 대체합니다.  
  
### <a name="merge-with-incremental-loads"></a>증분 로드와의 MERGE  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 의 새로운 변경 데이터 캡처 기능을 사용하면 데이터 웨어하우스로 증분 로드를 보다 쉽게, 안정적으로 수행할 수 있습니다. 삽입과 업데이트를 수행하기 위해 매개 변수가 있는 OLE DB 명령 변환을 사용하는 대신 MERGE 문을 사용하여 두 작업을 결합할 수 있습니다.  
  
 자세한 내용은 [대상에 변경 내용 적용](../../integration-services/change-data-capture/apply-the-changes-to-the-destination.md)을 참조하세요.  
  
#### <a name="merge-in-other-scenarios"></a>다른 시나리오에서의 MERGE  
 다음 시나리오에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 외부 또는 내부에서 MERGE 문을 사용할 수 있습니다. 그러나 대부분의 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지는 다른 유형의 여러 원본에서 이 데이터를 로드한 후 결합하고 정리해야 합니다. 따라서 쉽고 간단한 유지 관리를 위해 패키지에서 MERGE 문을 사용하는 방법을 고려할 수 있습니다.  
  
##### <a name="track-buying-habits"></a>구매 습관 추적  
 데이터 웨어하우스의 FactBuyingHabits 테이블은 고객이 특정 제품을 구매한 마지막 날짜를 추적합니다. 테이블은 ProductID, CustomerID 및 PurchaseDate 열로 구성됩니다. 매주 트랜잭션 데이터베이스는 해당 주 동안 이루어진 구매를 포함하는 PurchaseRecords 테이블을 생성합니다. 목표는 하나의 MERGE 문을 사용하여 PurchaseRecords 테이블의 정보를 FactBuyingHabits 테이블로 병합하는 것입니다. MERGE 문은 존재하지 않는 제품-고객 쌍에 대해 새 행을 삽입하고, 존재하는 제품-고객 쌍에 대한 최근 구매 날짜를 업데이트합니다.  
  
###### <a name="track-price-history"></a>가격 기록 추적  
 DimBook 테이블은 서점에 재고가 있는 책 목록을 나타내고 각 책의 가격 기록을 식별합니다. 이 테이블에는 ISBN, ProductID, Price, Shelf 및 IsCurrent 열이 있습니다. 또한 이 테이블에는 책의 각 가격에 대한 행이 하나씩 있습니다. 이러한 여러 행 중 하나에 현재 가격이 포함됩니다. 현재 가격이 포함된 행을 나타내기 위해 해당 행에 대한 IsCurrent 열의 값이 1로 설정됩니다.  
  
 매주 데이터베이스는 해당 주의 가격 변동과 주 동안 추가된 새 책을 포함하는 WeeklyChanges 테이블을 생성합니다. 하나의 MERGE 문을 사용하여 WeeklyChanges 테이블의 변경 사항을 DimBook 테이블에 적용할 수 있습니다. MERGE 문은 새로 추가된 책에 대해 새 행을 삽입하고, 가격이 변경된 기존 책의 행에 대한 IsCurrent 열을 0으로 업데이트합니다. 또한 MERGE 문은 가격이 변경된 책에 대해 새 행을 삽입하고, 삽입된 새 행에 대해 IsCurrent 열의 값을 1로 설정합니다.  
  
### <a name="merge-a-table-with-new-data-against-the-old-table"></a>새 데이터가 있는 테이블을 기존 테이블에 병합  
 데이터베이스는 "개방형 스키마", 즉 각 속성에 대한 이름-값 쌍을 포함하는 테이블을 사용하여 개체의 속성을 모델링합니다. 속성 테이블에는 EntityID, PropertyID 및 Value의 3개 열이 있습니다. 이 테이블의 새로운 버전인 NewProperties 테이블은 Properties 테이블과 동기화되어야 합니다. 이 두 테이블을 동기화하려면 하나의 MERGE 문을 사용하여 다음 작업을 수행하면 됩니다.  
  
-   NewProperties 테이블에 없는 속성을 Properties 테이블에서 삭제합니다.  
  
-   Properties 테이블의 속성 값을 NewProperties 테이블의 새 값으로 업데이트합니다.  
  
-   NewProperties 테이블에는 있지만 Properties 테이블에는 없는 속성에 대한 새 속성을 삽입합니다.  
  
 이 방식은 서버 두 대에 있는 두 테이블의 데이터를 동기화된 상태로 유지하는 것이 목적인 복제 시나리오와 비슷한 시나리오에서 유용합니다.  
  
### <a name="track-inventory"></a>재고 추적  
 Inventory 데이터베이스의 ProductsInventory 테이블에는 ProductID와 StockOnHand 열이 있습니다. ProductID, CustomerID 및 Quantity 열이 있는 Shipments 테이블은 고객에게 보내는 제품 배송을 추적합니다. ProductInventory 테이블은 Shipments 테이블의 정보를 바탕으로 매일 업데이트되어야 합니다. 하나의 MERGE 문은 배송을 기준으로 ProductInventory 테이블의 재고를 줄일 수 있습니다. 또한 제품에 대한 재고가 0이 되면 이 MERGE 문은 ProductInventory 테이블에서 해당 제품 행을 삭제할 수도 있습니다.  
  
  
