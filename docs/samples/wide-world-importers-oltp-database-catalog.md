---
title: WideWorldImporters OLTP 데이터베이스 카탈로그-SQL | Microsoft Docs
description: WideWorldImporters 예제 데이터베이스 카탈로그의 스키마, 테이블, 저장 프로시저 및 디자인 고려 사항을 이해 합니다.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d4502a64a3822741c1928fcf6faee69d80d893d5
ms.sourcegitcommit: 59c09dbe29882cbed539229a9bc1de381a5a4471
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/11/2020
ms.locfileid: "79112407"
---
# <a name="wideworldimporters-database-catalog"></a>WideWorldImporters 데이터베이스 카탈로그
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 데이터베이스에는 차량 및 냉 기에 대 한 센서 데이터 뿐만 아니라 판매 및 구매에 대 한 모든 트랜잭션 정보 및 일일 데이터가 포함 되어 있습니다.

## <a name="schemas"></a>스키마

WideWorldImporters는 데이터를 저장 하 고, 사용자가 데이터에 액세스 하는 방법을 정의 하 고, 데이터 웨어하우스 개발 및 통합에 대 한 개체를 제공 하는 등의 목적으로 스키마를 사용 합니다

### <a name="data-schemas"></a>데이터 스키마

이러한 스키마는 데이터를 포함 합니다. 다른 모든 스키마에는 많은 테이블이 필요 하며 응용 프로그램 스키마에 있습니다.

|스키마|Description|
|-----------------------------|---------------------|
|애플리케이션|응용 프로그램 전체 사용자, 연락처 및 매개 변수 여기에는 여러 스키마에서 사용 하는 데이터를 포함 하는 참조 테이블도 포함 됩니다.|
|구매|공급 업체의 재고 항목 구매 및 공급 업체에 대 한 세부 정보입니다.|  
|Sales|소매 고객에 대 한 재고 항목 판매 및 고객과 판매 직원에 대 한 세부 정보입니다. |  
|Warehouse|재고 항목 인벤토리 및 트랜잭션입니다.|  

### <a name="secure-access-schemas"></a>보안 액세스 스키마

이러한 스키마는 데이터 테이블에 직접 액세스할 수 없는 외부 응용 프로그램에 사용 됩니다. 여기에는 외부 응용 프로그램에서 사용 하는 뷰 및 저장 프로시저가 포함 됩니다.

|스키마|Description|
|-----------------------------|---------------------|
|Website|회사 웹 사이트의 데이터베이스에 대 한 모든 액세스는이 스키마를 통해 실행 됩니다.|
|보고서|Reporting Services 보고서에서 데이터베이스에 대 한 모든 액세스는이 스키마를 통해 실행 됩니다.|
|PowerBI|엔터프라이즈 게이트웨이를 통해 Power BI 대시보드에서 데이터베이스에 대 한 모든 액세스는이 스키마를 통해 실행 됩니다.|

예제 데이터베이스의 초기 릴리스에서는 보고서 및 PowerBI 스키마가 사용 되지 않습니다. 그러나이 데이터베이스를 기반으로 하는 모든 Reporting Services 및 Power BI 샘플은 이러한 스키마를 사용 하는 것이 좋습니다.

### <a name="development-schemas"></a>개발 스키마

특수 용도의 스키마

|스키마|Description|
|-----------------------------|---------------------|
|통합|데이터 웨어하우스 통합에 필요한 개체 및 프로시저 (즉, 데이터를 WideWorldImportersDW 데이터베이스로 마이그레이션하는 경우)|
|시퀀스|응용 프로그램의 모든 테이블에서 사용 하는 시퀀스를 저장 합니다.|

## <a name="tables"></a>테이블

데이터베이스의 모든 테이블은 데이터 스키마에 있습니다.

### <a name="application-schema"></a>응용 프로그램 스키마

공통 참조 테이블과 함께 매개 변수 및 사용자 (사용자 및 연락처)의 세부 정보입니다 (여러 다른 스키마에 공통).

|테이블|Description|
|-----------------------------|---------------------|
|SystemParameters|시스템 차원의 구성 가능한 매개 변수를 포함 합니다.|
|피플|에는 응용 프로그램을 사용 하는 모든 사용자에 대 한 사용자 이름, 연락처 정보, 그리고 Wide Wide가 고객 조직에서 처리 하는 사람이 포함 됩니다. 여기에는 직원, 고객, 공급 업체 및 기타 연락처가 포함 됩니다. 시스템이 나 웹 사이트를 사용할 수 있는 권한이 부여 된 사용자의 경우이 정보에는 로그인 정보가 포함 됩니다.|
|건설|시스템에 저장 된 많은 주소, 고객 조직 배달 주소, 공급 업체의 픽업 주소 등이 있습니다. 주소가 저장 될 때마다이 테이블에 도시에 대 한 참조가 있습니다. 또한 각 도시의 공간 위치도 있습니다.|
|StateProvinces|도시는 시/도의 일부입니다. 이 표에는 각 시/도의 경계를 설명 하는 공간 데이터를 비롯 한 세부 정보가 있습니다.|
|국가|주 또는도는 국가의 일부입니다. 이 표에는 각 국가의 경계를 설명 하는 공간 데이터를 비롯 하 여이에 대 한 세부 정보가 있습니다.|
|DeliveryMethods|재고 항목 (예: 트럭/van, post, 픽업, courier 등)을 제공 하기 위한 선택 항목|
|PaymentMethods|지불 하기 위한 선택 사항 (예: 현금, 확인, EFT 등)|
|TransactionTypes|고객, 공급자 또는 재고 거래 유형 (예: 청구서, 크레딧 메모 등)|

### <a name="purchasing-schema"></a>구매 스키마

공급 업체 및 재고 항목 구매의 세부 정보입니다.

|테이블|Description|
|-----------------------------|---------------------|
|Suppliers|Suppliers (조직)에 대 한 주 엔터티 테이블|
|SupplierCategories|공급 업체에 대 한 범주 (예: novelties, 장난감, 옷, 패키징 등)|
|SupplierTransactions|공급 업체와 관련 된 모든 금융 트랜잭션 (송장, 지불)|
|PurchaseOrders|공급자 구매 주문의 세부 정보|
|PurchaseOrderLines|공급 업체 구매 주문의 세부 정보 줄|

 
### <a name="sales-schema"></a>판매 스키마

고객, 영업 사원 및 재고 항목 판매에 대 한 세부 정보입니다.

|테이블|Description|
|-----------------------------|---------------------|
|고객|고객에 대 한 기본 엔터티 테이블 (조직 또는 개인)|
|CustomerCategories|고객에 대 한 범주 (ie 새로 움 stores, supermarkets 등)|
|BuyingGroups|고객 조직은 구매 능력을 강화 하는 그룹의 일부일 수 있습니다.|
|CustomerTransactions|고객이 관련 된 모든 금융 거래 (송장, 지불)|
|SpecialDeals|특별 가격 책정. 여기에는 고정 가격, 달러 또는 할인율 (할인율)이 포함 될 수 있습니다.|
|주문|고객 주문 세부 정보|
|OrderLines|고객 주문의 세부 정보 줄|
|송장|고객 청구서의 세부 정보|
|InvoiceLines|고객 청구서의 세부 정보 줄|

### <a name="warehouse-schema"></a>웨어하우스 스키마

재고 항목, 해당의 및 트랜잭션에 대 한 세부 정보입니다.

|테이블|Description|
|-----------------------------|---------------------|
|StockItems|재고 항목에 대 한 주 엔터티 테이블|
|StockItemHoldings|재고 항목에 대 한 비 temporal 열 이러한 열은 자주 업데이트 됩니다.|
|StockGroups|재고 항목 분류를 위한 그룹 (예: novelties, 장난감, novelties 등)|
|StockItemStockGroups|재고 그룹이 있는 재고 항목 (다 대 다)|
|색|재고 항목 (선택 사항)에 색이 있습니다.|
|Packagetypes>|재고 항목을 패키지할 수 있는 방법 (예: box, carton, 팔레트, kg 등)|
|StockItemTransactions|모든 재고 항목 (수신, 판매, 쓰기 해제)의 모든 움직임을 다루는 트랜잭션|
|VehicleTemperatures|차량 냉각기의 정기적으로 기록 된 온도|
|ColdRoomTemperatures|정기적으로 기록 되는 냉 냉각기의 온도|


## <a name="design-considerations"></a>디자인 고려 사항

데이터베이스 디자인은 주관적 이며 데이터베이스를 디자인 하는 데 적합 한 방법이 나 잘못 된 방법이 있습니다. 이 데이터베이스의 스키마와 테이블은 고유한 데이터베이스를 디자인 하는 방법에 대 한 아이디어를 보여 줍니다.

### <a name="schema-design"></a>스키마 디자인

WideWorldImporters는 적은 수의 스키마를 사용 하 여 데이터베이스 시스템을 이해 하 고 데이터베이스 원칙을 보여 줍니다.  

가능 하면 데이터베이스는 일반적으로 동일한 스키마로 함께 쿼리 되는 테이블을 찾아 조인 복잡성을 최소화 합니다.

데이터베이스 스키마는 다른 데이터베이스 WWI_Preparation의 일련의 메타 데이터 테이블을 기반으로 코드를 생성 했습니다. 이를 통해 매우 높은 수준의 디자인 일관성, 이름 일관성 및 완전성을 WideWorldImporters 수 있습니다. 스키마를 생성 하는 방법에 대 한 자세한 내용은 소스 코드: [wide-가져오기/wwi-데이터베이스-스크립트](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts) 를 참조 하세요.

### <a name="table-design"></a>테이블 디자인

- 모든 테이블에는 조인 단순성을 위한 단일 열 기본 키가 있습니다.
- 모든 스키마, 테이블, 열, 인덱스 및 check 제약 조건에는 개체 또는 열의 용도를 식별 하는 데 사용할 수 있는 설명 확장 속성이 있습니다. 메모리 액세스에 최적화 된 테이블은 현재 확장 속성을 지원 하지 않으므로이에 대 한 예외입니다.
- 동일한 왼쪽 구성 요소가 있는 다른 비클러스터형 인덱스가 있는 경우를 제외 하 고 모든 외래 키가 자동으로 인덱싱됩니다.
- 테이블의 자동 번호 매기기는 시퀀스를 기반으로 합니다. 이러한 시퀀스는 ID 열과 연결 된 서버 및 유사한 환경에서 보다 쉽게 작업할 수 있습니다. 메모리 액세스에 최적화 된 테이블은 SQL Server 2016에서를 지원 하지 않기 때문에 ID 열을 사용 합니다.
- CustomerTransactions, SupplierTransactions 및 StockItemTransactions 테이블에는 단일 시퀀스 (TransactionID)가 사용 됩니다. 테이블 집합에서 단일 시퀀스를 사용할 수 있는 방법을 보여 줍니다.
- 일부 열에는 적절 한 기본값이 있습니다.

### <a name="security-schemas"></a>보안 스키마

보안을 위해 WideWorldImporters는 외부 응용 프로그램이 데이터 스키마에 직접 액세스할 수 있도록 허용 하지 않습니다. 액세스를 격리 하기 위해 WideWorldImporters는 데이터를 저장 하지 않고 뷰 및 저장 프로시저를 포함 하는 보안 액세스 스키마를 사용 합니다. 외부 응용 프로그램은 보안 스키마를 사용 하 여 볼 수 있는 데이터를 검색 합니다.  이러한 방식으로 사용자는 보안 액세스 스키마의 뷰 및 저장 프로시저만 실행할 수 있습니다.

예를 들어이 샘플에 Power BI 대시보드가 포함 되어 있습니다. 외부 응용 프로그램은 PowerBI 스키마에 대 한 읽기 전용 권한이 있는 사용자로 Power BI 게이트웨이에서 이러한 Power BI 대시보드에 액세스 합니다.  읽기 전용 권한의 경우 사용자에 게 PowerBI 스키마에 대 한 SELECT 및 EXECUTE 권한만 필요 합니다. WWI의 데이터베이스 관리자는 필요에 따라 이러한 권한을 할당 합니다.

## <a name="stored-procedures"></a>저장 프로시저

저장 프로시저는 스키마로 구성 됩니다. 대부분의 스키마는 구성 또는 샘플 목적으로 사용 됩니다.

이 `Website` 스키마에는 웹 프런트 엔드에서 사용할 수 있는 저장 프로시저가 포함 되어 있습니다.

`Reports` 및 `PowerBI` 스키마는 reporting services 및 PowerBI 용도로 사용 됩니다. 이 샘플의 모든 확장은 보고 용도로 이러한 스키마를 사용 하는 것이 좋습니다.

### <a name="website-schema"></a>웹 사이트 스키마

클라이언트 응용 프로그램에서 사용 하는 프로시저 (예: 웹 프런트 엔드)입니다.

|절차|목적|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|사용자 `Application.People`가 웹 사이트에 액세스할 수 있도록 허용 합니다.|
|ChangePassword|외부 인증 메커니즘을 사용 하지 않는 사용자의 경우 사용자의 암호를 변경 합니다.|
|InsertCustomerOrders|주문 줄을 포함 하 여 하나 이상의 고객 주문 삽입을 허용 합니다.|
|InvoiceCustomerOrders|송장을 발부 하 고 송장을 처리할 주문 목록을 가져옵니다.|
|RecordColdRoomTemperatures|는 센서 데이터 목록을 테이블 반환 매개 변수 (TVP)로 사용 하 고 데이터를 `Warehouse.ColdRoomTemperatures` temporal 테이블에 적용 합니다.|
|RecordVehicleTemperature|는 JSON 배열을 사용 하 고 업데이트 `Warehouse.VehicleTemperatures`하는 데 사용 합니다.|
|SearchForCustomers|이름 또는 이름의 일부 (회사 이름 또는 사람 이름)로 고객을 검색 합니다.|
|SearchForPeople|이름 또는 이름의 일부로 사용자를 검색 합니다.|
|SearchForStockItems|이름 또는 이름 또는 마케팅 주석의 일부로 재고 항목을 검색 합니다.|
|SearchForStockItemsByTags|태그를 기준으로 재고 항목을 검색 합니다.|
|SearchForSuppliers|이름 또는 이름 (회사 이름 또는 사람 이름)의 일부로 공급 업체를 검색 합니다.|

### <a name="integration-schema"></a>통합 스키마

이 스키마의 저장 프로시저는 ETL 프로세스에서 사용 됩니다. [ETL 패키지](wide-world-importers-perform-etl.md)에 필요한 시간대에 대해 다양 한 테이블에서 필요한 데이터를 가져옵니다.

### <a name="dataloadsimulation-schema"></a>DataLoadSimulation 스키마

판매 및 구매를 삽입 하는 작업을 시뮬레이션 합니다. 주 저장 프로시저는 현재 `PopulateDataToCurrentDate`날짜까지 샘플 데이터를 삽입 하는 데 사용 되는입니다.

|절차|목적|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|데이터 로드 시뮬레이션에 필요한 프로시저를 다시 만듭니다. 현재 날짜까지 데이터를 가져오는 데 필요 합니다.|
|Configuration_RemoveDataLoadSimulationProcedures|이렇게 하면 데이터 시뮬레이션이 완료 된 후 프로시저를 다시 제거 합니다.|
|DeactivateTemporalTablesBeforeDataLoad|모든 temporal 테이블의 임시 특성을 제거 하 고 해당 하는 경우, 변경 내용이 sys 임시 테이블이 허용 하는 것 보다 이전 날짜에 적용 되는 것 처럼 변경 될 수 있도록 트리거를 적용 합니다.|
|PopulateDataToCurrentDate|현재 날짜까지 데이터를 가져오는 데 사용 됩니다. 초기 백업에서 데이터베이스를 복원한 후 다른 구성 옵션 보다 먼저 실행 해야 합니다.|
|ReactivateTemporalTablesAfterDataLoad|데이터 일관성 확인을 포함 하 여 임시 테이블을 다시 설정 합니다. 연결 된 트리거를 제거 합니다.|


### <a name="application-schema"></a>응용 프로그램 스키마

이러한 절차는 샘플을 구성 하는 데 사용 됩니다. 이 버전은 샘플의 standard edition 버전에 enterprise edition 기능을 적용 하는 데 사용 되며, 감사 및 전체 텍스트 인덱싱을 추가 하는 데에도 사용 됩니다.

|절차|목적|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|멤버가 역할에 아직 없는 경우 역할에 멤버를 추가 합니다.|
|Configuration_ApplyAuditing|감사를 추가 합니다. 서버 감사는 standard edition 데이터베이스에 적용 됩니다. enterprise edition에 대 한 추가 데이터베이스 감사가 추가 됩니다.|
|Configuration_ApplyColumnstoreIndexing|Columnstore 인덱싱을 및에 `Sales.OrderLines` 적절 `Sales.InvoiceLines` 하 게 다시 인덱스에 적용 합니다.|
|Configuration_ApplyFullTextIndexing|, `Application.People` `Sales.Customers`, 및 `Warehouse.StockItems`에 전체 텍스트 인덱스를 적용 합니다. `Purchasing.Suppliers` , `Website.SearchForPeople` `Website.SearchForSuppliers` `Website.SearchForStockItems`,,를 `Website.SearchForStockItemsByTags` 전체 텍스트 인덱싱을 사용 하는 대체 프로시저로 바꿉니다. `Website.SearchForCustomers`|
|Configuration_ApplyPartitioning|및에 `Sales.CustomerTransactions` 테이블 분할을 `Purchasing.SupplierTransactions`적용 하 고 인덱스를 다시 정렬 합니다.|
|Configuration_ApplyRowLevelSecurity|행 수준 보안을 적용 하 여 영업 지역 관련 역할별로 고객을 필터링 합니다.|
|Configuration_ConfigureForEnterpriseEdition|Columnstore 인덱싱, 전체 텍스트, 메모리 내 polybase 및 분할을 적용 합니다.|
|Configuration_EnableInMemory|메모리 최적화 파일 그룹 (Azure에서 작업 하지 않는 경우)을 추가 하 `Warehouse.ColdRoomTemperatures`고 `Warehouse.VehicleTemperatures` ,를 메모리 내 항목으로 대체 하 `Website.OrderIDList`고, 데이터 `Website.OrderList` `Website.OrderLineList`를 마이그레이션하고,,, `Website.SensorDataList` , 메모리 최적화 된 해당 항목을 포함 하는 테이블 형식을 다시 `Website.InvoiceCustomerOrders`만들고 `Website.InsertCustomerOrders`, 프로시저 `Website.RecordColdRoomTemperatures` 를 삭제 하 고 다시 만든 다음 이러한 테이블 형식을 사용 합니다.|
|Configuration_RemoveAuditing|감사 구성을 제거 합니다.|
|Configuration_RemoveRowLevelSecurity|행 수준 보안 구성 (연결 된 테이블을 변경 하는 데 필요 함)을 제거 합니다.|
|CreateRoleIfNonExistant|아직 존재 하지 않는 경우 데이터베이스 역할을 만듭니다.|


### <a name="sequences-schema"></a>시퀀스 스키마

데이터베이스에서 시퀀스를 구성 하는 절차

|절차|목적|
|-----------------------------|---------------------|
|ReseedAllSequences|모든 시퀀스에 대해 ReseedSequenceBeyondTableValue 프로시저를 호출 합니다.|
|ReseedSequenceBeyondTableValue|동일한 시퀀스를 사용 하는 테이블의 값을 벗어나 다음 시퀀스 값의 위치를 변경 하는 데 사용 됩니다. (시퀀스에 해당 하는 id 열에 대 한 DBCC CHECKIDENT와 같이 여러 테이블에서)|
