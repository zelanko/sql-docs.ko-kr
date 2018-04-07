---
title: WideWorldImporters 데이터베이스 카탈로그 | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: samples
ms.technology:
- samples
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e47c0022-ce87-4ba5-a24b-df55efe66431
caps.latest.revision: 3
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 0d458bc15530aa87bfa922787558fff3f07645f7
ms.sourcegitcommit: 094c46e7fa6de44735ed0040c65a40ec3d951b75
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2018
---
# <a name="wideworldimporters-database-catalog"></a>WideWorldImporters 데이터베이스 카탈로그
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 데이터베이스 모든는 트랜잭션 정보 및 판매 및 구매에 대 한 일별 데이터도 차량 및 콜드 방 센서 데이터를 포함합니다.

## <a name="schemas"></a>스키마

스키마를 사용 하 여, 데이터를 저장 하 고, 사용자는 데이터에 액세스할 수 있습니다 어떻게 정의 하 고, 데이터 웨어하우스 개발 및 통합을 위한 개체를 제공 하는 등의 다른 용도로 WideWorldImporters 합니다.

### <a name="data-schemas"></a>데이터 스키마

이러한 스키마는 데이터를 포함합니다. 다른 모든 스키마가 필요 하 고 응용 프로그램 스키마에 있는 하는 테이블의 수입니다.

|스키마|Description|
|-----------------------------|---------------------|
|응용 프로그램|전체 응용 프로그램 사용자, 연락처 및 매개 변수입니다. 참조 테이블에 여러 스키마에서 사용 되는 데이터도 여기에 포함|
|Purchasing|공급 업체 및 공급 업체에 대 한 세부 정보에서 재고 항목을 구입 했습니다.|  
|Sales|재고 항목 소매 고객 및 고객 및 판매 사람에 대 한 세부 정보에 판매 합니다. |  
|Warehouse|재고 항목 인벤토리 및 트랜잭션입니다.|  

### <a name="secure-access-schemas"></a>보안 액세스 스키마

이러한 스키마는 데이터 테이블에 직접 액세스를 허용 하지 않는 외부 응용 프로그램에 사용 됩니다. 뷰 및 저장된 프로시저 외부 응용 프로그램에서 사용 하는 포함 됩니다.

|스키마|Description|
|-----------------------------|---------------------|
|웹 사이트|이 스키마를 통해 회사 웹 사이트에서 데이터베이스에 대 한 모든 액세스가 됩니다.|
|보고서|이 스키마를 통해 Reporting Services 보고서에서 데이터베이스에 대 한 모든 액세스가 됩니다.|
|PowerBI|이 스키마를 통해 엔터프라이즈 게이트웨이 통해 Power BI 대시보드를 데이터베이스에 대 한 모든 액세스가 됩니다.|

보고서 및 PowerBI 스키마 예제 데이터베이스의 초기 릴리스에서 사용 되지 않습니다. 그러나이 데이터베이스를 기반으로 빌드된 모든 Reporting Services 및 Power BI 샘플 이러한 스키마를 사용 하는 것이 좋습니다.

### <a name="development-schemas"></a>개발 스키마

특수 한 용도의 스키마

|스키마|Description|
|-----------------------------|---------------------|
|통합|개체 및 데이터 웨어하우스 통합에 필요한 절차 (예: WideWorldImportersDW 데이터베이스로 데이터 마이그레이션).|
|시퀀스|응용 프로그램의 모든 테이블에서 사용 하는 시퀀스를 보유 합니다.|

## <a name="tables"></a>테이블

데이터베이스의 모든 테이블은 데이터 스키마.

### <a name="application-schema"></a>응용 프로그램 스키마

매개 변수 및 일반 참조 테이블 (다른 여러 스키마를 공통)와 함께 사용자 (사용자 및 연락처)의 세부 정보입니다.

|테이블|Description|
|-----------------------------|---------------------|
|SystemParameters|시스템 수준 구성 가능한 매개 변수를 포함합니다.|
|사람|사용자 이름, 모든 응용 프로그램을 사용 하 고 고객 조직에서 Wide World Importers를 처리 하는 사람들에 대 한 연락처 정보를 포함 합니다. 직원, 고객, 공급 업체 및 다른 연락처를 포함 합니다. 시스템 또는 웹 사이트를 사용할 수 있는 권한이 부여 된 사용자를 위해 정보 로그인 세부 정보를 포함 합니다.|
|도시|사용자에 게 고객 조직 배달 주소, 공급 업체 등에서 픽업 주소는 시스템에 저장 하는 주소 여러 개 있습니다. 주소는 저장할 때마다이 테이블의 city에 대 한 참조가 있습니다. 각 도시에 대 한 공간 위치 이기도합니다.|
|StateProvinces|도시는 국가 또는 주의의 일부입니다. 이 테이블에는 각 시 /도의 경계를 설명 하는 공간 데이터를 비롯 한 이러한 세부 정보입니다.|
|Countries|국가 또는 주의 일부 국가입니다. 이 테이블에 각 국가 경계를 설명 하는 공간 데이터를 비롯 한 이러한 세부 정보입니다.|
|DeliveryMethods|재고 항목 (예: 트럭/van, post, 픽업, courier 등)을 전달 하는 것에 대 한 선택|
|PaymentMethods|대금을 지불 하는 것에 대 한 선택 (예: 현금, 확인, EFT, 등입니다.)|
|TransactionTypes|고객, 공급 업체 또는 주식 트랜잭션 (예: 송장, 신용 메모 등)는 형식|

### <a name="purchasing-schema"></a>스키마를 구입합니다.

재고 항목 구매 및 공급 업체의 세부 정보입니다.

|테이블|Description|
|-----------------------------|---------------------|
|Suppliers|공급 업체 (조직)에 대 한 주 엔터티 테이블|
|SupplierCategories|공급자 (예: novelties, 장난감, clothing, 패키징, 등)에 대 한 범주|
|SupplierTransactions|모든 금융 거래 업체와 관련 된 (송장을 지불) 있는|
|PurchaseOrders|공급 업체 구매 주문 세부 정보|
|PurchaseOrderLines|구매 주문서를 공급자에서 정보 행|

 
### <a name="sales-schema"></a>판매 스키마

재고 항목 판매 및 고객, 영업 사원의 세부 정보입니다.

|테이블|Description|
|-----------------------------|---------------------|
|Customers|고객 (조직이 나 개인)에 대 한 주 엔터티 테이블|
|CustomerCategories|고객 (ie 새로 움 저장소, 슈퍼마켓 등)에 대 한 범주|
|BuyingGroups|고객 조직에는 강력한 구매를 실행 하는 그룹의 일부가 될 수 있습니다.|
|CustomerTransactions|고객 관련 (송장을 지불) 되는 모든 금융 거래|
|SpecialDeals|특별 한 가격입니다. 이러한 고정된 가격을 포함, 달러 또는 할인율 할인 수 있습니다.|
|Orders|고객 주문 세부 정보|
|주문 라인|고객 주문에서 정보 행|
|송장|고객 송장 세부 정보|
|InvoiceLines|고객 송장에서 정보 행|

### <a name="warehouse-schema"></a>웨어하우스 스키마

재고 항목, 주식 및 트랜잭션 세부 정보입니다.

|테이블|Description|
|-----------------------------|---------------------|
|StockItems|재고 항목에 대 한 주 엔터티 테이블|
|StockItemHoldings|재고 항목에 대 한 비 임시 열입니다. 이들은 자주 업데이트 된 열입니다.|
|StockGroups|재고 항목 (예: novelties, 장난감, 식용 novelties 등)을 분류에 대 한 그룹|
|StockItemStockGroups|재고 항목 들 주식 그룹 (다대다)|
|색|재고 항목 수 (선택 사항) 색상을 갖습니다.|
|PackageTypes|항목을 판매 하는 방식으로 패키지로 만들 수도 있습니다 (예: 상자 carton, 팔레트를 표시, k g, 등입니다.|
|StockItemTransactions|모든 재고 항목 (수신, 판매, write-off)의 동작은 모두 포함 하는 트랜잭션|
|VehicleTemperatures|자동차를 움직일 chillers의 온도 정기적으로 기록 된|
|ColdRoomTemperatures|콜드 방 chillers의 온도 정기적으로 기록|


## <a name="design-considerations"></a>디자인 고려 사항

데이터베이스 디자인 주관적인 이며 데이터베이스 디자인에 맞거나 틀릴 방법이 없습니다. 이 데이터베이스의 테이블과 스키마 사용자 데이터베이스를 디자인 하는 방법에 대 한 아이디어를 보여 줍니다.

### <a name="schema-design"></a>스키마 디자인

WideWorldImporters 적은 수의 스키마를 사용 하므로 데이터베이스 시스템을 이해 하 고 데이터베이스 원칙 시연 하기 쉽습니다.  

가능 하면 데이터베이스 collocates 테이블을 조인 복잡성을 최소화 하기 위해 동일한 스키마로 함께 일반적으로 쿼리 됩니다.

데이터베이스 스키마가 되었습니다 코드에서 생성 된 일련의 WWI_Preparation 다른 데이터베이스의 메타 데이터 테이블에 따라. 매우 높은 수준의 일관성 디자인, 명명 일관성 및 완결성 WideWorldImporters 제공합니다. 스키마가 생성 되었습니다 참조 소스 코드: [와이드-실제-가져오기/wwi-데이터베이스-스크립트](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

### <a name="table-design"></a>테이블 디자인

- 모든 테이블에는 조인 단순성에 대 한 단일 열 기본 키가 있습니다.
- 모든 스키마, 테이블, 열, 인덱스 및 check 제약 조건에는 개체 또는 열의 목적을 파악 하는 데 사용할 수 있는 속성을 확장 하는 설명이 필요 합니다. 메모리 액세스에 최적화 된 테이블 예외 되므로 현재 확장된 속성을 지원 하지 않습니다.
- 모든 외래 키를 사용 하지 않으면 다른 비클러스터형 인덱스 같은 왼쪽 구성 요소를 자동으로 인덱싱됩니다.
- 테이블에서 자동 번호 지정 시퀀스를 기반으로 합니다. 이러한 시퀀스는 연결 된 서버 및 ID 열 보다 유사한 환경에서 사용 하기 쉽습니다. 메모리 액세스에 최적화 된 테이블 ID 열을 사용 하 여 SQL Server 2016에서 지원 하지 않습니다.
- 단일 시퀀스 (트랜잭션 Id)는 이러한 테이블에 사용 됩니다: CustomerTransactions, SupplierTransactions, 및 StockItemTransactions 합니다. 이 테이블 집합 단일 시퀀스를 가질 수 있습니다는 방법을 보여 줍니다.
- 일부 열에는 적절 한 기본값이 있습니다.

### <a name="security-schemas"></a>보안 스키마

보안을 위해 WideWorldImporters 데이터 스키마에 직접 액세스 하는 외부 응용 프로그램을 허용 하지 않습니다. 액세스를 격리 하려면 WideWorldImporters 데이터를 포함 하지 않은 있지만 뷰 및 저장된 프로시저를 포함 하는 보안 액세스 스키마를 사용 합니다. 외부 응용 프로그램 보안 스키마를 사용 하 여 볼 수 있는 데이터를 검색 합니다.  이러한 방식으로 사용자가 실행할 수 있습니다 뷰 및 저장된 프로시저는 보안 액세스 스키마

예를 들어이 샘플에 Power BI 대시보드를 포함 됩니다. Power BI 게이트웨이 PowerBI 스키마에 대 한 읽기 전용 권한이 있는 사용자로 이러한 Power BI 대시보드를 액세스 하는 외부 응용 프로그램입니다.  읽기 전용 권한에 대 한 사용자는 PowerBI 스키마에 대 한 SELECT 및 EXECUTE 권한이 필요합니다. WWI에서 데이터베이스 관리자는 필요에 따라 이러한 사용 권한을 할당 합니다.

## <a name="stored-procedures"></a>저장 프로시저

저장된 프로시저는 스키마에서 구성 됩니다. 대부분의 스키마 구성 또는 샘플 목적으로 사용 됩니다.

`Website` 스키마 웹 프런트 엔드에 사용할 수 있는 저장된 프로시저를 포함 합니다.

`Reports` 및 `PowerBI` 스키마 reporting services 및 PowerBI 목적을 위해서 제공 됩니다. 이 샘플의 모든 확장 보고용으로 이러한 스키마를 사용 하는 것이 좋습니다.

### <a name="website-schema"></a>웹 사이트 스키마

이들은 웹 프런트 엔드 같은 클라이언트 응용 프로그램에서 사용 되는 프로시저입니다.

|절차|용도|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|사용자 허용 (에서 `Application.People`) 웹 사이트에 액세스할 수 있어야 합니다.|
|ChangePassword|(사용자에 대 한 외부 인증 메커니즘을 사용 하지 않는) 사용자의 암호를 변경 합니다.|
|InsertCustomerOrders|(주문 라인 포함)에 대 한 하나 이상의 고객 주문을 삽입할 수 있습니다.|
|InvoiceCustomerOrders|목록이 며 송장 발급을 주문 하 고는 청구서를 처리 합니다.|
|RecordColdRoomTemperatures|테이블 반환 매개 변수 (TVP) 센서 데이터 목록 변수로 및 데이터를 적용 하는 `Warehouse.ColdRoomTemperatures` 임시 테이블입니다.|
|RecordVehicleTemperature|JSON 배열을 사용 하 고 사용 하 여 업데이트를 `Warehouse.VehicleTemperatures`합니다.|
|SearchForCustomers|고객 이름이 나 이름 (회사 이름 또는 사용자 이름)의 일부를 검색 합니다.|
|SearchForPeople|사용자 이름 또는 이름의 일부를 검색 합니다.|
|SearchForStockItems|재고 항목을 이름 또는 이름 또는 설명을 마케팅 중 일부를 검색 합니다.|
|SearchForStockItemsByTags|태그별으로 재고 항목을 검색 합니다.|
|SearchForSuppliers|공급 업체 이름 또는 이름 (회사 이름 또는 사용자 이름)의 일부를 검색 합니다.|

### <a name="integration-schema"></a>통합 스키마

이 스키마에 저장된 프로시저는 ETL 프로세스에 의해 사용 됩니다. 에 필요한 기간에 대 한 다양 한 테이블에서 필요한 데이터를 가져올는 [ETL 패키지](etl-workflow.md)합니다.

### <a name="dataloadsimulation-schema"></a>DataLoadSimulation 스키마

판매 및 구매를 삽입 하는 작업을 시뮬레이션 합니다. 기본 저장된 프로시저는 `PopulateDataToCurrentDate`, 현재 날짜 까지의 샘플 데이터를 삽입 하는 데 사용 되는 합니다.

|절차|용도|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|절차를 다시 만드는 데 필요한 데이터에 대 한 부하 시뮬레이션 합니다. 이 현재 날짜 까지의 데이터를 가져오는 필요 합니다.|
|Configuration_RemoveDataLoadSimulationProcedures|그러면 제거 절차 다시 데이터 시뮬레이션 완료 된 후 됩니다.|
|DeactiveTemporalTablesBeforeDataLoad|모든 임시 테이블의 임시 특성을 제거 하 고 해당 되는 경우 트리거 sys 임시 테이블을 사용 하는 보다 이전 날짜에 적용 되 고 한 것 처럼 변경할 수 있도록 적용 합니다.|
|PopulateDataToCurrentDate|현재 날짜 까지의 데이터를 가져오는 데 합니다. 초기 백업에서 데이터베이스를 복원한 후 다른 구성 옵션 보다 먼저 실행 해야 합니다.|
|ReactivateTemporalTablesAfterDataLoad|데이터 일관성 검사를 포함 하 여 임시 테이블을 다시 설정 합니다. (연결 된 트리거를 제거합니다.)|


### <a name="application-schema"></a>응용 프로그램 스키마

이 절차의 샘플을 구성 하는 데 사용 됩니다. Enterprise edition 기능 standard edition 버전 샘플의 및 감사를 추가할 및 전체 텍스트 인덱싱에 적용할 사용 됩니다.

|절차|용도|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|멤버 역할에 있지 않은 경우 역할에 구성원 추가|
|Configuration_ApplyAuditing|감사를 추가합니다. Standard edition 데이터베이스에 대 한 적용 되는 서버 감사 추가 데이터베이스 감사는 enterprise edition 용 추가 됩니다.|
|Configuration_ApplyColumnstoreIndexing|Columnstore 인덱스를 작성 적용 `Sales.OrderLines` 및 `Sales.InvoiceLines` reindexes 적절 하 게 하 고 있습니다.|
|Configuration_ApplyFullTextIndexing|전체 텍스트 인덱스에 적용 됩니다. `Application.People`, `Sales.Customers`, `Purchasing.Suppliers`, 및 `Warehouse.StockItems`합니다. 대체 `Website.SearchForPeople`, `Website.SearchForSuppliers`, `Website.SearchForCustomers`, `Website.SearchForStockItems`, `Website.SearchForStockItemsByTags` 대체 하는 프로시저 전체 텍스트 인덱스를 사용 합니다.|
|Configuration_ApplyPartitioning|테이블 분할에 적용 됩니다. `Sales.CustomerTransactions and `에 맞게 Purchasing.SupplierTransactions' 및 인덱스를 다시 정렬 합니다.|
|Configuration_ApplyRowLevelSecurity|매출액으로 행 수준 보안 필터 고객에 게 적용 territory에 관련 된 역할입니다.|
|Configuration_ConfigureForEnterpriseEdition|Columnstore 인덱스, 전체 텍스트, 메모리, polybase를 및 분할에 적용 됩니다.|
|Configuration_EnableInMemory|(Azure에서 작동 하지 않을) 하는 경우 메모리 액세스에 최적화 된 파일 그룹을 추가, 대체 `Warehouse.ColdRoomTemperatures`, `Warehouse.VehicleTemperatures` 메모리 내의 해당를 하 고 데이터를 마이그레이션하면 다시 만듭니다는 `Website.OrderIDList`, `Website.OrderList`, `Website.OrderLineList`, `Website.SensorDataList` 삭제 하 고 절차를 다시 만듭니다. 해당 메모리 액세스에 최적화 된 테이블 형식을 `Website.InvoiceCustomerOrders`, `Website.InsertCustomerOrders`, 및 `Website.RecordColdRoomTemperatures` 이러한 테이블 형식을 사용 하 합니다.|
|Configuration_RemoveAuditing|감사 구성을 제거합니다.|
|Configuration_RemoveRowLevelSecurity|(이 과정이 필요 관련된 테이블의 변경 내용을) 행 수준 보안 구성을 제거 합니다.|
|CreateRoleIfNonExistant|존재 하지 않는 경우 데이터베이스 역할을 만듭니다.|


### <a name="sequences-schema"></a>시퀀스 스키마

데이터베이스의 시퀀스를 구성 하는 절차입니다.

|절차|용도|
|-----------------------------|---------------------|
|ReseedAllSequences|모든 시퀀스에 대 한 ReseedSequenceBeyondTableValue 프로시저를 호출합니다.|
|ReseedSequenceBeyondTableValue|동일한 시퀀스를 사용 하는 테이블의 값 보다 큰 다음 시퀀스 값의 위치를 변경 하는 데 사용 합니다. (예:을 DBCC CHECKIDENT identity 열 해당 시퀀스에 대 한 하지만 잠재적으로 여러 테이블에 대해).|
