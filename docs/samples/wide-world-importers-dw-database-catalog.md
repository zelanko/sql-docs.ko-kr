---
title: WideWorldImporters OLAP 데이터베이스 카탈로그 SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7b4533ec0667bc59317ba213578db7301c15b241
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="wideworldimportersdw-database-catalog"></a>WideWorldImportersDW 데이터베이스 카탈로그
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
스키마, 테이블 및 WideWorldImportersDW 데이터베이스의 저장된 프로시저에 대 한 설명입니다. 

WideWorldImportersDW 데이터베이스는 데이터 웨어하우징 및 분석 처리에 사용 됩니다. 판매 및 구매에 대 한 트랜잭션 데이터 WideWorldImporters 데이터베이스에 생성 되 고 사용 하 여 WideWorldImportersDW 데이터베이스에 로드 한 **일별 ETL 프로세스**합니다.

WideWorldImportersDW의 데이터를 따라서 WideWorldImporters에 데이터를 미러링 하지만 테이블은 서로 다르게 구성 됩니다. WideWorldImporters에는 기존의 정규화 된 스키마가 반면 WideWorldImportersDW 사용은 [별모양 스키마](https://wikipedia.org/wiki/Star_schema) 테이블 디자인에 대 한 접근 방식입니다. 팩트 및 차원 테이블 외에도 데이터베이스는 ETL 프로세스에 사용 되는 준비 테이블의 번호를 포함 합니다.

## <a name="schemas"></a>스키마

´ Ù à 세 개의 스키마에서 구성 됩니다.

|스키마|Description|
|-----------------------------|---------------------|
|차원|차원 테이블입니다.|
|팩트|팩트 테이블입니다.|  
|통합|테이블 및 ETL에 필요한 기타 개체를 준비 합니다.|  

## <a name="tables"></a>테이블

차원 및 팩트 테이블은 다음과 같습니다. 통합 스키마의 테이블 ETL 프로세스에 대해서만 사용 되 고 나열 되지 않습니다.

### <a name="dimension-tables"></a>차원 테이블

WideWorldImportersDW 다음 차원 테이블에 있습니다. 설명은 WideWorldImporters 데이터베이스에서는 원본 테이블과 관계를 포함합니다.

|테이블|원본 테이블|
|-----------------------------|---------------------|
|City|`Application.Cities`, `Application.StateProvinces` 및 `Application.Countries` 데이터 형식에 사용할 수 있습니다.|
|Customer|`Sales.Customers`, `Sales.BuyingGroups` 및 `Sales.CustomerCategories` 데이터 형식에 사용할 수 있습니다.|
|날짜|회계 연도 포함 하 여 날짜에 대 한 정보가 포함 된 새 테이블 (11 월 1 일에 따라 회계 연도 대 한 시작)입니다.|
|Employee|`Application.People`을 참조하세요.|
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors` 및 `Warehouse.PackageType` 데이터 형식에 사용할 수 있습니다.|
|공급자|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`에 적용되지 않습니다.|
|PaymentMethod|`Application.PaymentMethods`을 참조하세요.|
|TransactionType|`Application.TransactionTypes`을 참조하세요.|

### <a name="fact-tables"></a>팩트 테이블

WideWorldImportersDW 다음 팩트 테이블에 있습니다. 설명은 WideWorldImporters 데이터베이스 뿐만 아니라 각 팩트 테이블 일반적으로 사용 되는 분석/보고 된 쿼리의 클래스 원본 테이블과 관계를 포함 합니다.

|테이블|원본 테이블|샘플 분석|
|-----------------------------|---------------------|---------------------|
|주문|`Sales.Orders`및`Sales.OrderLines`|판매 사람, 선택/packer 생산성, 및에서 orders를 선택 하도록 시간. 또한 주문을 백업 하는 주식 상황 부족 합니다.|
|판매|`Sales.Invoices`및`Sales.InvoiceLines`|판매 날짜, 배달 날짜, 시간에 따라 수익성, 영업 사원의 수익성 합니다.|
|구매|`Purchasing.PurchaseOrderLines`|예상된 및 실제 시간|
|트랜잭션|`Sales.CustomerTransactions`및`Purchasing.SupplierTransactions`|문제 날짜와 종료 날짜 및 시간을 측정 합니다.|
|이동|`Warehouse.StockTransactions`|시간이 지남에 따라 이동 합니다.|
|스톡 보유|`Warehouse.StockItemHoldings`|보유 재고 수준 및 값입니다.|

## <a name="stored-procedures"></a>저장 프로시저

저장된 프로시저는 기본적으로 ETL 프로세스에 대 한 구성 작업에 사용할 사용 됩니다.

사용 하도록이 샘플의 모든 확장의 `Reports` Reporting Services 보고서에 대 한 스키마 및 `PowerBI` Power BI 액세스에 대 한 스키마입니다.

### <a name="application-schema"></a>응용 프로그램 스키마

이 절차의 샘플을 구성 하는 데 사용 됩니다. PolyBase를를 추가 하는 샘플의 standard edition 버전에 적용 되는 enterprise edition 기능 ETL 초기값을 다시 설정 하는 데 사용 됩니다.

|절차|용도|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|팩트 테이블에 대 한 분할 및 columnstore 인덱스에 적용 됩니다.|
|Configuration_ConfigureForEnterpriseEdition|분할 columnstore 인덱싱 및 메모리에 적용 됩니다.|
|Configuration_EnableInMemory|통합 준비 테이블을 ETL 성능을 향상 하기 위해 SCHEMA_ONLY 메모리 액세스에 최적화 된 테이블을 바꿉니다.|
|Configuration_ApplyPolybase|외부 데이터 원본, 파일 형식 및 테이블을 구성합니다.|
|Configuration_PopulateLargeSaleTable|Enterprise edition 변경 내용을 적용 한 후 추가 기록으로 2012 달력 연도 대 한 더 많은 양의 데이터를 채웁니다.|
|Configuration_ReseedETL|기존 데이터를 제거 하 고 ETL 초기값을 다시 시작 합니다. 이렇게 하면 OLAP 데이터베이스를 다시 채워야 하는 OLTP 데이터베이스의 업데이트 된 행과 일치 합니다.|

### <a name="integration-schema"></a>통합 스키마

ETL 프로세스에 사용 되는 프로시저는 이러한 범주에 속합니다.
- ETL 패키지-모든 Get * 프로시저에 대 한 도우미 프로시저입니다.
- 모든 마이그레이션 * 프로시저-DW 테이블로 데이터를 준비 하는 ETL 패키지에서 마이그레이션하는 데 사용 되는 프로시저입니다.
- `PopulateDateDimensionForYear` -1 년을 사용 하 고 해당 연도의 모든 날짜에 채워지도록 보장는 `Dimension.Date` 테이블입니다.

### <a name="sequences-schema"></a>시퀀스 스키마

데이터베이스의 시퀀스를 구성 하는 절차입니다.

|절차|용도|
|-----------------------------|---------------------|
|ReseedAllSequences|프로시저 호출 `ReseedSequenceBeyondTableValue` 모든 시퀀스에 대 한 합니다.|
|ReseedSequenceBeyondTableValue|동일한 시퀀스를 사용 하는 테이블의 값 보다 큰 다음 시퀀스 값의 위치를 변경 하는 데 사용 합니다. (같은 `DBCC CHECKIDENT` identity 열 동일 시퀀스에 대 한 하지만 잠재적으로 여러 테이블에 대 한 합니다.)|
