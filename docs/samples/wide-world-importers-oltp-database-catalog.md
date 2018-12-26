---
title: WideWorldImporters OLTP 데이터베이스 카탈로그-SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ed73e9e97c34ad1bd1d3aa4e0d37a351cbac0703
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798047"
---
# <a name="wideworldimporters-database-catalog"></a>WideWorldImporters 데이터베이스 카탈로그
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
WideWorldImporters 데이터베이스 모든는 트랜잭션 정보 및 판매 및 구매에 대 한 일일 데이터와 콜드 방 차량에 센서 데이터를 포함합니다.

## <a name="schemas"></a>스키마

WideWorldImporters, 데이터를 저장 하 고, 사용자 데이터에 액세스할 수 있습니다 하는 방법을 정의 하 고, 데이터 웨어하우스 개발 및 통합에 대 한 개체를 제공 하는 등의 다양 한 용도로 스키마를 사용 합니다.

### <a name="data-schemas"></a>데이터 스키마

이러한 스키마는 데이터를 포함 합니다. 테이블 수가 다른 모든 스키마에 필요한 이며 응용 프로그램 스키마에 있습니다.

|스키마|Description|
|-----------------------------|---------------------|
|애플리케이션|응용 프로그램 수준의 사용자, 연락처 및 매개 변수입니다. 여러 스키마에 의해 사용 되는 데이터를 사용 하 여 참조 테이블도 포함|
|Purchasing|주식 항목에 공급 업체 및 공급자에 대 한 세부 정보에서 구입합니다.|  
|Sales|재고 항목 소매 고객 및 고객 및 판매 사람에 대 한 세부 정보를 판매 합니다. |  
|Warehouse|재고 항목 인벤토리 및 트랜잭션입니다.|  

### <a name="secure-access-schemas"></a>보안 액세스 스키마

이러한 스키마는 데이터 테이블에 직접 액세스를 허용 되지 않는 외부 응용 프로그램에 사용 됩니다. 뷰 및 저장된 프로시저 외부 응용 프로그램에서 사용 하는 포함 합니다.

|스키마|Description|
|-----------------------------|---------------------|
|웹 사이트|이 스키마를 통해 회사 웹 사이트에서 데이터베이스에 대 한 모든 액세스가 됩니다.|
|보고서|이 스키마를 통해 Reporting Services 보고서에서 데이터베이스에 대 한 모든 액세스가 됩니다.|
|PowerBI|이 스키마를 통해 엔터프라이즈 게이트웨이 통해 Power BI 대시보드에서 데이터베이스에 대 한 모든 액세스가 됩니다.|

보고서 및 PowerBI 스키마 예제 데이터베이스의 초기 릴리스에서 사용 되지 않습니다. 그러나이 데이터베이스가 기반으로 하는 모든 Reporting Services 및 Power BI 샘플 이러한 스키마를 사용 하는 것이 좋습니다.

### <a name="development-schemas"></a>개발 스키마

특수 한 용도의 스키마

|스키마|Description|
|-----------------------------|---------------------|
|통합|개체 및 데이터 웨어하우스 통합에 필요한 절차 (즉, WideWorldImportersDW database로 데이터 마이그레이션).|
|시퀀스|응용 프로그램의 모든 테이블에 사용 되는 시퀀스를 보유 합니다.|

## <a name="tables"></a>테이블

데이터베이스의 모든 테이블 데이터 스키마의 경우

### <a name="application-schema"></a>응용 프로그램 스키마

매개 변수 및 일반 참조 테이블 (다른 여러 스키마를 일반적인)와 함께 사용자 (사용자 및 연락처)의 세부 정보입니다.

|Table|Description|
|-----------------------------|---------------------|
|SystemParameters|시스템 수준 구성 가능한 매개 변수를 포함합니다.|
|사용자|사용자 이름, 고객의 조직에서 사용 하 여 Wide World Importers를 처리 하는 사용자 및 모든 응용 프로그램을 사용 하 여 사용자에 대 한 연락처 정보를 포함 합니다. 직원, 고객, 공급 업체 및 기타 연락처 포함 됩니다. 정보는 시스템 또는 웹 사이트를 사용할 수 있는 권한이 부여 된 사람들에 게 로그인 세부 정보를 포함 합니다.|
|도시|사용자, 고객 조직 배달 주소, 공급 업체 등에서 픽업 주소에 대 한 시스템에 저장 된 주소의 있습니다. 주소는 저장할 때마다이 테이블의 도시에 대 한 참조가 있습니다. 각 도시에 대 한 공간 위치 이기도합니다.|
|StateProvinces|도시는 국가 또는 시/도의 일부입니다. 이 테이블에는 각 시 /도 경계를 설명 하는 공간 데이터를 비롯 한 이러한 세부 정보입니다.|
|Countries|국가 또는 국가에 속합니다. 이 테이블에는 각 국가의 경계를 설명 하는 공간 데이터를 비롯 한 이러한 세부 정보가 있습니다.|
|DeliveryMethods|재고 항목 (예를 들어, 트럭/van, post, 승차, courier, 등)를 제공 하기 위한 선택 항목|
|PaymentMethods|대금 지불 옵션 (예를 들어 현금, 확인, EFT, 등.)|
|TransactionTypes|고객, 공급 업체 또는 주식 트랜잭션 (예를 들어, 청구서, 크레딧 메모 등) 형식|

### <a name="purchasing-schema"></a>스키마를 구매합니다.

재고 항목 구매 및 공급 업체의 세부 정보입니다.

|Table|Description|
|-----------------------------|---------------------|
|Suppliers|공급 업체 (조직)에 대 한 주요 엔터티 테이블|
|SupplierCategories|공급 업체 (예를 들어 novelties, toys, clothing, 패키징 등)에 대 한 범주|
|SupplierTransactions|공급자 관련 (청구서를 지불)는 모든 금융 거래|
|PurchaseOrders|공급자 구매 주문의 세부 정보|
|PurchaseOrderLines|공급 업체에서 세부 정보 줄 구매 주문서|

 
### <a name="sales-schema"></a>Sales 스키마

재고 항목 판매 및 고객, 영업 사원, 세부 정보입니다.

|Table|Description|
|-----------------------------|---------------------|
|고객|고객 (조직 또는 개인)에 대 한 주요 엔터티 테이블|
|CustomerCategories|고객 (ie 새로 움 저장소, 슈퍼마켓 등)에 대 한 범주|
|BuyingGroups|고객의 조직에는 구매 강화는 그룹의 일부가 될 수 있습니다.|
|CustomerTransactions|고객 관련 (청구서를 지불)는 모든 금융 거래|
|SpecialDeals|특별 합니다. 고정된 가격, 할인 달러 또는 할인율 수이 있습니다.|
|Orders|고객 주문 세부 정보|
|OrderLines|고객 주문에서 세부 정보 행|
|송장|고객 청구서의 세부 정보|
|InvoiceLines|고객 청구서에서 세부 정보 행|

### <a name="warehouse-schema"></a>웨어하우스 스키마

재고 항목, holdings 및 트랜잭션 세부 정보입니다.

|Table|Description|
|-----------------------------|---------------------|
|StockItems|주식 항목에 대 한 주요 엔터티 테이블|
|StockItemHoldings|주식 항목에 대 한 비 temporal 열입니다. 이들은 자주 업데이트 된 열입니다.|
|StockGroups|재고 항목 (예를 들어 novelties, toys, 식용 novelties 등)를 분류 하는 것에 대 한 그룹|
|StockItemStockGroups|재고 항목 재고가 그룹 (다 대 다)?|
|색|재고 항목 색 있습니다 (선택 사항)|
|PackageTypes|항목 스톡 방식으로 패키징할 수 있습니다 (예: 상자, carton, 팔레트, kg, 등입니다.|
|StockItemTransactions|트랜잭션 (수신, 판매, write-off) 모든 재고 항목의 동작은 모두를 포함 합니다.|
|VehicleTemperatures|차량 냉각기의 정기적으로 기록 된 온도|
|ColdRoomTemperatures|콜드 방 냉각기의 온도 정기적으로 기록|


## <a name="design-considerations"></a>디자인 고려 사항

데이터베이스 디자인은 주관적 이며 데이터베이스 디자인에 잘못 되었거나 올바른 방법은 없습니다. 스키마 및이 데이터베이스의 테이블에 사용자 고유의 데이터베이스를 디자인 하는 방법을 하는 것에 대 한 아이디어를 보여 줍니다.

### <a name="schema-design"></a>스키마 디자인

WideWorldImporters 소수의 스키마를 사용 하므로 데이터베이스 시스템을 이해 하 고 데이터베이스 원칙을 설명 하는 것이 쉽습니다.  

가능한 경우 일반적으로 쿼리는 함께 조인 복잡성을 최소화 하기 위해 동일한 스키마로 테이블 데이터베이스에 함께 배치 합니다.

데이터베이스 스키마가 되었습니다 코드 생성 WWI_Preparation 다른 데이터베이스의 메타 데이터 테이블 계열을 기반으로 합니다. 매우 높은 수준의 디자인 일관성, 명명 일관성 및 완결성 WideWorldImporters 제공합니다. 스키마를 생성 하는 방법에 대 한 자세한 내용은 소스 코드를 참조 하십시오.: [wide-전 세계-가져오기/wwi-데이터베이스-스크립트](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

### <a name="table-design"></a>테이블 디자인

- 모든 테이블에는 단일 열 조인 단순성에 대 한 기본 키에 있습니다.
- 모든 스키마, 테이블, 열, 인덱스 및 check 제약 조건에는 Description 확장 속성의 개체 또는 열 용도 파악 하는 경우 메모리 최적화 테이블에는이 확장된 속성을 현재 지원 하지 않으므로 합니다.
- 모든 외래 키 같은 왼쪽 구성 요소에 있는 다른 비클러스터형 인덱스 없는 자동으로 인덱싱됩니다.
- 테이블에서 자동 번호 매기기 시퀀스를 기반으로 합니다. 이러한 시퀀스는 연결 된 서버 및 ID 열 보다 유사한 환경에서 사용 하기 쉽습니다. 메모리 최적화 테이블에서 SQL Server 2016을 지원 하지 않으므로 ID 열을 사용 합니다.
- 이러한 테이블에 대 한 단일 시퀀스 (트랜잭션 Id)는: CustomerTransactions, SupplierTransactions, 및 StockItemTransactions 합니다. 이 테이블의 집합을 단일 시퀀스를 가질 수 있습니다 하는 방법을 보여 줍니다.
- 일부 열에 적절 한 기본값입니다.

### <a name="security-schemas"></a>보안 스키마

보안상의 WideWorldImporters 외부 응용 프로그램 데이터 스키마를 직접 액세스를 허용 하지 않습니다. 액세스를 격리 하려면 WideWorldImporters 데이터에 포함 되지 않은 있지만 뷰 및 저장된 프로시저를 포함 하는 보안 액세스 스키마를 사용 합니다. 보려는 허용 된 데이터를 검색할 보안 스키마를 사용 하는 외부 응용 프로그램입니다.  이 이렇게 하면 사용자가 에서만 실행할 수 있습니다 뷰 및 저장된 프로시저에 보안 액세스 스키마

예를 들어이 샘플에 Power BI 대시보드를 포함 되어 있습니다. 이러한 Power BI 대시보드를 Power BI gateway에서 PowerBI 스키마에 대 한 읽기 전용 권한이 있는 사용자로 액세스 하는 외부 응용 프로그램입니다.  읽기 전용 권한에 대 한 사용자만 PowerBI 스키마에 대 한 SELECT 및 EXECUTE 권한이 필요합니다. WWI에서 데이터베이스 관리자가 필요에 따라 이러한 권한을 할당 합니다.

## <a name="stored-procedures"></a>저장 프로시저

저장된 프로시저는 스키마에서 구성 됩니다. 스키마의 대부분은 구성 또는 샘플 목적으로 사용 됩니다.

`Website` 스키마 웹 프런트 엔드를 사용할 수 있는 저장된 프로시저를 포함 합니다.

합니다 `Reports` 및 `PowerBI` 스키마는 reporting services 및 PowerBI 용도로 적합 합니다. 샘플의 확장 보고용으로 이러한 스키마를 사용 하는 것이 좋습니다.

### <a name="website-schema"></a>웹 사이트 스키마

이들은 웹 프런트 엔드 같은 클라이언트 응용 프로그램에서 사용 하는 절차입니다.

|프로시저|용도|
|-----------------------------|---------------------|
|ActivateWebsiteLogon|수 (에서 `Application.People`) 웹 사이트에 액세스할 수 있도록 합니다.|
|ChangePassword|(외부 인증 메커니즘을 사용 하지 않는 사용자)에 대 한 사용자의 암호를 변경 합니다.|
|InsertCustomerOrders|(주문 줄 포함)에 대 한 하나 이상의 고객 주문을 삽입을 허용 합니다.|
|InvoiceCustomerOrders|송장 처리할 주문 목록을 사용 하 고 청구서를 처리 합니다.|
|RecordColdRoomTemperatures|테이블 반환 매개 변수 (TVP)으로 센서 데이터 목록을 가져오고 데이터를 적용 합니다 `Warehouse.ColdRoomTemperatures` temporal 테이블입니다.|
|RecordVehicleTemperature|JSON 배열을 가져오고 업데이트 하는 데 사용 `Warehouse.VehicleTemperatures`합니다.|
|SearchForCustomers|이름 또는 이름 (회사 이름 또는 사용자 이름) 부분을 기준으로 고객을 검색 합니다.|
|SearchForPeople|사용자 이름 또는 이름의 일부를 검색 합니다.|
|SearchForStockItems|이름 또는 부분 이름 또는 설명을 마케팅 재고 항목을 검색 합니다.|
|SearchForStockItemsByTags|태그로 재고 항목을 검색 합니다.|
|SearchForSuppliers|이름 또는 이름 (회사 이름 또는 사용자 이름)의 일부 공급 업체를 검색 합니다.|

### <a name="integration-schema"></a>통합 스키마

이 스키마의 저장된 프로시저는 ETL 프로세스에서 사용 됩니다. 에 필요한 기간에 대 한 다양 한 테이블에서 필요한 데이터를 가져올 수는 [ETL 패키지](wide-world-importers-perform-etl.md)합니다.

### <a name="dataloadsimulation-schema"></a>DataLoadSimulation 스키마

판매 및 구매를 삽입 하는 작업을 시뮬레이션 합니다. 기본 저장된 프로시저는 `PopulateDataToCurrentDate`는 현재 날짜 까지의 샘플 데이터를 삽입 하는 데 사용 됩니다.

|프로시저|용도|
|-----------------------------|---------------------|
|Configuration_ApplyDataLoadSimulationProcedures|절차를 다시 만드는 데 필요한 데이터에 대 한 부하 시뮬레이션 합니다. 이 현재 날짜 까지의 데이터를 가져오는에 필요 합니다.|
|Configuration_RemoveDataLoadSimulationProcedures|제거 절차 다시 완료 되 면 데이터 시뮬레이션 합니다.|
|DeactiveTemporalTablesBeforeDataLoad|모든 temporal 테이블의 임시 특성을 제거 하 고 해당 하는 경우 sys temporal 테이블을 허용 하는 보다 이전 날짜에 적용 되 고 된 것 처럼 변경할 수 있도록 트리거를 적용 합니다.|
|PopulateDataToCurrentDate|현재 날짜 까지의 데이터를 표시 하는 데 사용 합니다. 초기 백업에서 데이터베이스를 복원한 후 다른 구성 옵션 보다 먼저 실행 되어야 합니다.|
|ReactivateTemporalTablesAfterDataLoad|데이터 일관성 확인을 포함 하 여 temporal 테이블을 다시 설정 합니다. (연결 된 트리거를 제거) 합니다.|


### <a name="application-schema"></a>응용 프로그램 스키마

이러한 절차는 샘플 구성에 사용 됩니다. 스탠더드 버전 샘플의 고도 추가할 감사 및 전체 텍스트 인덱싱에 엔터프라이즈 버전 기능을 적용할 사용 됩니다.

|프로시저|용도|
|-----------------------------|---------------------|
|AddRoleMemberIfNonexistant|역할의 멤버가 아닌 경우 역할에 구성원 추가|
|Configuration_ApplyAuditing|감사를 추가합니다. Standard edition 데이터베이스에 대 한 적용 되는 서버 감사 추가 데이터베이스 감사는 enterprise edition 용 추가 됩니다.|
|Configuration_ApplyColumnstoreIndexing|Columnstore 인덱싱에 적용 됩니다 `Sales.OrderLines` 고 `Sales.InvoiceLines` 및 적절 하 게 되는 다시 인덱싱합니다.|
|Configuration_ApplyFullTextIndexing|전체 텍스트 인덱스에 적용 됩니다 `Application.People`, `Sales.Customers`를 `Purchasing.Suppliers`, 및 `Warehouse.StockItems`합니다. 대체 `Website.SearchForPeople`, `Website.SearchForSuppliers`, `Website.SearchForCustomers`합니다 `Website.SearchForStockItems`, `Website.SearchForStockItemsByTags` 전체 텍스트 인덱싱을 사용 하는 교체 절차를 사용 하 여 합니다.|
|Configuration_ApplyPartitioning|테이블 분할을 적용 `Sales.CustomerTransactions and `에 맞게 Purchasing.SupplierTransactions' 및 인덱스를 다시 정렬 합니다.|
|Configuration_ApplyRowLevelSecurity|매출액으로 고객을 필터링 할 행 수준 보안 적용 territory에 관련 된 역할입니다.|
|Configuration_ConfigureForEnterpriseEdition|Columnstore 인덱싱, 전체 텍스트, 메모리, polybase 및 분할에 적용 됩니다.|
|Configuration_EnableInMemory|(Azure에서 작동 하지 않음) 하는 경우 메모리 최적화 파일 그룹을 추가, 대체 `Warehouse.ColdRoomTemperatures`, `Warehouse.VehicleTemperatures` 에 메모리에 해당 하는 마이그레이션 데이터를 다시 만듭니다 합니다 `Website.OrderIDList`를 `Website.OrderList`를 `Website.OrderLineList`, `Website.SensorDataList` 형식과 테이블 해당 하는 메모리 액세스에 최적화 된, 삭제 및 다시 만드는 절차 `Website.InvoiceCustomerOrders`, `Website.InsertCustomerOrders`, 및 `Website.RecordColdRoomTemperatures` 이러한 테이블 형식을 사용 하 합니다.|
|Configuration_RemoveAuditing|감사 구성을 제거합니다.|
|Configuration_RemoveRowLevelSecurity|(연결된 된 테이블 변경에 대 한 필요는) 행 수준 보안 구성을 제거 합니다.|
|CreateRoleIfNonExistant|이미 존재 하지 않는 경우 데이터베이스 역할을 만듭니다.|


### <a name="sequences-schema"></a>시퀀스 스키마

데이터베이스에서 시퀀스를 구성 하는 절차입니다.

|프로시저|용도|
|-----------------------------|---------------------|
|ReseedAllSequences|모든 시퀀스에 대 한 ReseedSequenceBeyondTableValue 프로시저를 호출합니다.|
|ReseedSequenceBeyondTableValue|동일한 시퀀스를 사용 하는 테이블의 값 보다 큰 다음 시퀀스 값의 위치를 변경 하는 데 사용 합니다. (예:을 DBCC CHECKIDENT identity 열 해당 순서에 대 한 하지만 잠재적으로 여러 테이블에 대해).|
