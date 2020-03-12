---
title: WideWorldImporters OLAP 데이터베이스 카탈로그-SQL | Microsoft Docs
description: WideWorldImportersDW 데이터베이스에서 데이터 웨어하우징 및 분석 처리에 사용 되는 스키마, 테이블 및 저장 프로시저를 이해 합니다.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 167b9d1d9990c20be8c01a3407a5423644e524f8
ms.sourcegitcommit: 59c09dbe29882cbed539229a9bc1de381a5a4471
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/11/2020
ms.locfileid: "79112437"
---
# <a name="wideworldimportersdw-database-catalog"></a>WideWorldImportersDW 데이터베이스 카탈로그
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW 데이터베이스의 스키마, 테이블 및 저장 프로시저에 대 한 설명입니다. 

WideWorldImportersDW 데이터베이스는 데이터 웨어하우징 및 분석 처리에 사용 됩니다. 판매 및 구매에 대 한 트랜잭션 데이터는 WideWorldImporters 데이터베이스에 생성 되며 **매일 ETL 프로세스**를 사용 하 여 WideWorldImportersDW 데이터베이스에 로드 됩니다.

따라서 WideWorldImportersDW의 데이터는 WideWorldImporters의 데이터를 미러링 하지만 테이블은 다르게 구성 됩니다. WideWorldImporters에는 기존의 정규화 된 스키마가 있지만 WideWorldImportersDW는 테이블 디자인에 [별모양 스키마](https://wikipedia.org/wiki/Star_schema) 방법을 사용 합니다. 팩트 및 차원 테이블 외에도 데이터베이스에는 ETL 프로세스에 사용 되는 여러 준비 테이블이 포함 되어 있습니다.

## <a name="schemas"></a>스키마

여러 유형의 테이블은 세 가지 스키마로 구성 됩니다.

|스키마|Description|
|-----------------------------|---------------------|
|차원|차원 테이블|
|팩트|팩트 테이블.|  
|통합|ETL에 필요한 준비 테이블 및 기타 개체입니다.|  

## <a name="tables"></a>테이블

차원 및 팩트 테이블은 아래에 나열 되어 있습니다. 통합 스키마의 테이블은 ETL 프로세스에만 사용 되며 나열 되지 않습니다.

### <a name="dimension-tables"></a>차원 테이블

WideWorldImportersDW에는 다음과 같은 차원 테이블이 있습니다. 설명에는 WideWorldImporters 데이터베이스의 원본 테이블과의 관계가 포함 됩니다.

|테이블|원본 테이블|
|-----------------------------|---------------------|
|City|`Application.Cities`, `Application.StateProvinces`, `Application.Countries`.|
|Customer|`Sales.Customers`, `Sales.BuyingGroups`, `Sales.CustomerCategories`.|
|Date|재무 연도를 포함 하 여 날짜에 대 한 정보를 포함 하는 새 테이블 (재무 년 11 월 1 일 기준)|
|Employee|`Application.People`.|
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors`, `Warehouse.PackageType`.|
|공급자|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`.|
|PaymentMethod|`Application.PaymentMethods`.|
|TransactionType|`Application.TransactionTypes`.|

### <a name="fact-tables"></a>팩트 테이블

WideWorldImportersDW에는 다음과 같은 팩트 테이블이 있습니다. 설명에는 WideWorldImporters 데이터베이스의 원본 테이블과의 관계 및 각 팩트 테이블이에서 일반적으로 사용 되는 분석/보고 쿼리 클래스가 포함 됩니다.

|테이블|원본 테이블|샘플 분석|
|-----------------------------|---------------------|---------------------|
|주문|`Sales.Orders` 및 `Sales.OrderLines`|판매 직원, 선택/팩 광고 생산성 및 주문 선택 시간을 선택 합니다. 또한 낮은 재고 상황은 주문에 선행 됩니다.|
|Sale|`Sales.Invoices` 및 `Sales.InvoiceLines`|판매 날짜, 배달 날짜, 시간별 수익성, 영업 사원 수익성|
|Purchase|`Purchasing.PurchaseOrderLines`|예상 및 실제 리드 시간|
|트랜잭션|`Sales.CustomerTransactions` 및 `Purchasing.SupplierTransactions`|문제 날짜와 종료 날짜 및 금액을 측정 합니다.|
|방식|`Warehouse.StockTransactions`|시간이 지남에 따라 이동 합니다.|
|재고 보유|`Warehouse.StockItemHoldings`|직접 재고 수준 및 가치.|

## <a name="stored-procedures"></a>저장 프로시저

저장 프로시저는 주로 ETL 프로세스 및 구성 용도로 사용 됩니다.

샘플의 모든 확장은 Reporting Services 보고서에 `Reports` 스키마를 사용 하 고 power BI 액세스를 `PowerBI` 위한 스키마를 사용 하는 것이 좋습니다.

### <a name="application-schema"></a>응용 프로그램 스키마

이러한 절차는 샘플을 구성 하는 데 사용 됩니다. 이 버전은 샘플의 standard edition 버전에 enterprise edition 기능을 적용 하 고, PolyBase를 추가 하 고, ETL을 시드 하는 데 사용 됩니다.

|절차|목적|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|팩트 테이블에 대 한 분할 및 columnstore 인덱스를 모두 적용 합니다.|
|Configuration_ConfigureForEnterpriseEdition|분할, columnstore 인덱싱 및 메모리 내를 적용 합니다.|
|Configuration_EnableInMemory|SCHEMA_ONLY 메모리 최적화 테이블로 통합 준비 테이블을 대체 하 여 ETL 성능을 향상 시킵니다.|
|Configuration_ApplyPolyBase|외부 데이터 원본, 파일 형식 및 테이블을 구성 합니다.|
|Configuration_PopulateLargeSaleTable|Enterprise edition 변경 내용을 적용 한 다음, 2012 년에 대 한 더 많은 양의 데이터를 추가 기록으로 채웁니다.|
|Configuration_ReseedETL|기존 데이터를 제거 하 고 ETL 시드를 다시 시작 합니다. 이렇게 하면 OLAP 데이터베이스를 OLTP 데이터베이스의 업데이트 된 행과 일치 늘이기 수 있습니다.|

### <a name="integration-schema"></a>통합 스키마

ETL 프로세스에 사용 되는 프로시저는 다음과 같은 범주로 분류 됩니다.
- ETL 패키지에 대 한 도우미 프로시저-모든 Get * 프로시저
- ETL 패키지에서 준비 된 데이터를 DW 테이블 (모든 마이그레이션 * 절차)로 마이그레이션하기 위해 사용 하는 프로시저입니다.
- `PopulateDateDimensionForYear`-연도를 사용 하 고 해당 연도에 대 한 모든 날짜가 `Dimension.Date` 테이블에 채워지는지 확인 합니다.

### <a name="sequences-schema"></a>시퀀스 스키마

데이터베이스에서 시퀀스를 구성 하는 절차

|절차|목적|
|-----------------------------|---------------------|
|ReseedAllSequences|모든 시퀀스에 `ReseedSequenceBeyondTableValue` 대해 프로시저를 호출 합니다.|
|ReseedSequenceBeyondTableValue|동일한 시퀀스를 사용 하는 테이블의 값을 벗어나 다음 시퀀스 값의 위치를 변경 하는 데 사용 됩니다. 시퀀스에 해당 `DBCC CHECKIDENT` 하는 id 열의 경우와 같지만 잠재적으로 여러 테이블에 대 한입니다.|
