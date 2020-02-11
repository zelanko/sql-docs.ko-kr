---
title: SQL Server 기능 및 기능 사용 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 01/21/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 06f89721-8478-4abc-8ada-e9c73b08bf51
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 69f0027041b4acf45a54d8d8d655bc8772417dc6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68811537"
---
# <a name="use-of-sql-server-features-and-capabilities"></a>SQL Server 기능 및 기능 사용

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

OLTP 데이터베이스에서 SQL Server 기능 및 기능을 WideWorldImporters 사용 합니다.

WideWorldImporters는 SQL Server 2016에 도입 된 최신 기능을 비롯 하 여 SQL Server의 많은 주요 기능을 보여 주기 위해 설계 되었습니다. 다음 표에서는 SQL Server의 기능과 기능을 보여 줍니다. 또한 각 행은 WideWorldImporters에서 기능을 사용 하는 방법에 대 한 설명을 제공 합니다.  
&nbsp;

|SQL Server 기능 또는 기능|WideWorldImporters에서 사용|
|:-------------------------------|:------------------------|
|임시 테이블|StockItems, Customers 및 Suppliers와 같은 주요 엔터티 및 모든 조회 스타일 참조 테이블을 포함 하는 많은 temporal 테이블이 있습니다. Temporal 테이블을 사용 하면 이러한 엔터티의 기록을 편리 하 게 추적할 수 있습니다.|
|JSON에 대 한 AJAX 호출|응용 프로그램은 종종 AJAX 호출을 사용 하 여 이러한 테이블을 쿼리 합니다. Persons, Customers, Suppliers 및 StockItems. 호출은 JSON 형식으로 데이터를 반환 합니다. 예를 들어 저장 프로시저 `Website.SearchForCustomers`를 참조 하세요.|
|JSON 속성/값 모음|테이블의 관계형 데이터를 확장 하기 위해 JSON 데이터를 포함 하는 열이 있는 테이블이 여러 개 있습니다. 예를 들어 `Application.SystemParameters` 에는 응용 프로그램 설정에 대 `Application.People` 한 열이 있고 사용자 기본 설정을 기록 하는 열이 있습니다. 이러한 테이블은 열 `nvarchar(max)` 값이 유효한 json 인지 확인 하기 위해 기본 제공 함수 `ISJSON` 를 사용 하 여 CHECK 제약 조건과 함께 json 데이터를 기록 하는 열을 사용 합니다.|
|행 수준 보안(RLS)|RLS (행 수준 보안)는 역할 멤버 자격에 따라 Customers 테이블에 대 한 액세스를 제한 하는 데 사용 됩니다. 각 영업 지역에는 역할과 사용자가 있습니다. 작업에서 RLS 액세스 제한을 보려면 [샘플 릴리스의](https://go.microsoft.com/fwlink/?LinkID=800630)일부인 sample-script의 해당 스크립트를 사용 합니다.|
|실시간 운영 분석|(데이터베이스의 전체 버전) 운영 워크 로드에 `Sales.InvoiceLines` 미치는 `Sales.OrderLines` 영향을 최소화 하 고 트랜잭션 데이터베이스의 분석 쿼리를 효율적으로 실행 하는 것을 지원 하기 위해 핵심 트랜잭션 테이블 및 둘 다에 비클러스터형 columnstore 인덱스가 있습니다. 동일한 데이터베이스에서 트랜잭션 및 분석을 실행 하는 것을 [하이브리드 트랜잭션/분석 처리 (HTAP)](https://wikipedia.org/wiki/Hybrid_Transactional/Analytical_Processing_(HTAP))라고도 합니다. 이 작업을 수행 하는 것을 확인 하려면 [샘플 릴리스의](https://go.microsoft.com/fwlink/?LinkID=800630)일부인 sample-script의 해당 스크립트를 사용 합니다.|
|PolyBase|이 PolyBase가 작동 하는 것을 확인 하려면 Azure 블로그 저장소에서 호스트 되는 공용 데이터 집합이 있는 외부 테이블을 사용 하 여 [샘플 릴리스의](https://go.microsoft.com/fwlink/?LinkID=800630)일부인 sample-script의 해당 스크립트를 사용 합니다.|
|메모리 내 OLTP|(데이터베이스의 전체 버전) 테이블 형식 Tvp (테이블 반환 매개 변수)는 모두 메모리 최적화를 활용 하 여 모든 메모리 최적화 기능을 제공 합니다.<br/><br/>`Warehouse.VehicleTemperatures` 및 `Warehouse.ColdRoomTemperatures`의 두 모니터링 테이블은 메모리 최적화입니다. 메모리 최적화를 사용 하면 기존 디스크 기반 테이블 보다 더 높은 속도로 ColdRoomTemperatures 테이블을 채울 수 있습니다. VehicleTemperatures 테이블은 JSON 페이로드를 보관 하 고 IoT 시나리오에 대 한 확장에 적합 합니다. VehicleTemperatures 테이블은 EventHubs, Stream Analytics 및 Power BI와 관련 된 시나리오에 더 적합 합니다.<br/><br/>저장 프로시저 `Website.RecordColdRoomTemperatures` 는 기본적으로 컴파일되어 콜드 실내 온도를 기록 하는 성능을 향상 시킵니다.<br/><br/>작동 중인 메모리 내 OLTP의 예를 보려면 [샘플 릴리스의](https://go.microsoft.com/fwlink/?LinkID=800630)workload-drivers에서 차량-위치 워크 로드 드라이버를 참조 하세요.|
|클러스터형 columnstore 인덱스|(데이터베이스의 전체 버전) 테이블 `Warehouse.StockItemTransactions` 은 클러스터형 columnstore 인덱스를 사용 합니다. 이 테이블의 행 수는 커질 것으로 예상 되며 클러스터형 columnstore 인덱스는 테이블의 디스크 크기를 상당히 줄이고 쿼리 성능을 향상 시킵니다. 이 테이블에 대 한 수정은 삽입 전용입니다. 온라인 워크 로드에서이 테이블에 대 한 업데이트/삭제가 없으며, 클러스터형 columnstore 인덱스는 삽입 작업에 대해 잘 수행 됩니다.|
|동적 데이터 마스킹|데이터베이스 스키마에서 테이블 `Purchasing.Suppliers`의 공급자에 대해 보유 한 은행 정보에 데이터 마스킹을 적용 했습니다. 비관리자 직원은이 정보에 액세스할 수 없습니다.|
|Always Encrypted|Always Encrypted에 대 한 데모는 [샘플 릴리스의](https://go.microsoft.com/fwlink/?LinkID=800630)일부인 다운로드 가능한 샘플 .zip에 포함 되어 있습니다. 데모에서는 암호화 키, 중요 한 데이터에 대 한 암호화를 사용 하는 테이블 및 테이블에 데이터를 삽입 하는 작은 샘플 응용 프로그램을 만듭니다.|
|스트레치 데이터베이스|`Warehouse.ColdRoomTemperatures` 테이블이 임시 테이블로 구현 되었으며 전체 버전의 예제 데이터베이스에서 메모리 최적화 되어 있습니다. 보관 테이블은 디스크를 기반으로 하며 Azure로 확장 될 수 있습니다.|
|전체 텍스트 인덱스|전체 텍스트 인덱스는 사람, 고객 및 StockItems 대 한 검색을 개선 합니다. 인덱스는 전체 텍스트 인덱싱이 SQL Server 인스턴스에 설치 된 경우에만 쿼리에 적용 됩니다. 비영구 계산 열은 StockItems 테이블에서 전체 텍스트 인덱싱되는 데이터를 만드는 데 사용 됩니다.<br/><br/>`CONCAT`는 전체 텍스트 인덱싱되는 SearchData를 만들기 위해 필드를 연결 하는 데 사용 됩니다.<br/>예제에서 전체 텍스트 인덱스를 사용 하도록 설정 하려면 데이터베이스에서 다음 문을 실행 합니다.<br/><br/>`EXECUTE [Application].[Configuration_ConfigureFullTextIndexing]`<br/><br/>프로시저는 기본 전체 텍스트 카탈로그를 만든 다음 (없는 경우), 검색 뷰를 해당 뷰의 전체 텍스트 버전으로 바꿉니다.<br/><br/>SQL Server에서 전체 텍스트 인덱스를 사용 하려면 설치 하는 동안 전체 텍스트 옵션을 선택 해야 합니다. Azure SQL Database는 전체 텍스트 인덱스를 사용 하기 위해 및 특정 구성이 필요 하지 않습니다.|
|인덱싱된 지속형 계산 열|SupplierTransactions 및 CustomerTransactions 사용 되는 인덱싱된 지속형 계산 열입니다.|
|CHECK 제약 조건|비교적 복잡 한 check 제약 조건은에 `Sales.SpecialDeals`있습니다. 이를 통해 한 Countamount, Discountamount 및 UnitPrice 중 하나만 구성 됩니다.|
|UNIQUE 제약 조건|에 대해 다 대 `Warehouse.StockItemStockGroups`다 생성 (및 unique 제약 조건)을 설정 합니다.|
|테이블 분할|(데이터베이스의 전체 버전) 및 `Sales.CustomerTransactions` `Purchasing.SupplierTransactions` 테이블은 모두 파티션 함수 `PF_TransactionDate` 및 파티션 구성표 `PS_TransactionDate`를 사용 하 여 연도별로 분할 됩니다. 분할은 많은 테이블의 관리 효율성을 향상 시키는 데 사용 됩니다.|
|목록 처리|예제 테이블 형식이 `Website.OrderIDList` 제공 됩니다. 예제 프로시저 `Website.InvoiceCustomerOrders`에서 사용 됩니다. 이 절차에서는 Cte (공통 테이블 식), TRY/CATCH, JSON_MODIFY, XACT_ABORT, NOCOUNT, THROW 및 XACT_STATE를 사용 하 여 응용 프로그램에서 데이터베이스 엔진으로의 왕복을 최소화 하기 위해 단일 순서만이 아닌 주문 목록을 처리 하는 기능을 보여 줍니다.|
|GZip 압축|`Warehouse.VehicleTemperature` 뷰에서 해당 테이블은 전체 센서 데이터를 포함 합니다. 그러나이 데이터가 몇 개월 이상 오래 된 경우 공간을 절약 하기 위해 압축 됩니다. 압축 함수는 GZip 압축을 사용 합니다.<br/><br/>이 뷰에서 `Website.VehicleTemperatures` 는 이전에 압축 된 데이터를 검색할 때 압축 풀기 함수를 사용 합니다.|
|쿼리 저장소|데이터베이스에서 쿼리 저장소를 사용할 수 있습니다. 몇 가지 쿼리를 실행 한 후에는 다음 단계를 수행 합니다.<br/><br/>1. Management Studio에서 데이터베이스를 엽니다.<br/>2. 데이터베이스 아래에 있는 노드 쿼리 저장소를 엽니다.<br/>3. 리소스를 많이 사용 하는 *상위 쿼리*보고서를 엽니다. 쿼리 실행을 참조 하 고 방금 실행 한 쿼리에 대 한 계획을 참조 하세요.|
|STRING_SPLIT|테이블 `Sales.Invoices` 의 `DeliveryInstructions` 열에는 STRING_SPLIT를 설명 하는 데 사용할 수 있는 쉼표로 구분 된 값이 있습니다.|
|감사|데이터베이스에서 다음 문을 실행 하 여이 예제 데이터베이스에 대 한 SQL Server 감사를 사용 하도록 설정할 수 있습니다.<br/><br/>`EXECUTE [Application].[Configuration_ApplyAuditing]`<br/><br/>Azure SQL Database에서 감사는 [Azure Portal](https://portal.azure.com/)를 통해 사용 하도록 설정 됩니다.<br/><br/>로그인, 역할 및 사용 권한과 관련 된 보안 작업은 감사를 사용 하는 모든 시스템 (standard edition 시스템 포함)에 기록 됩니다. 감사는 모든 시스템에서 사용할 수 있으며 추가 권한이 필요 하지 않으므로 응용 프로그램 로그로 전달 됩니다. 더 높은 보안을 위해 보안 로그 나 보안 폴더의 파일로 리디렉션해야 하는 경고가 제공 됩니다. 필요한 추가 구성을 설명 하기 위한 링크가 제공 됩니다.<br/><br/>Evaluation/developer/enterprise edition 시스템의 경우 모든 금융 트랜잭션 데이터에 대 한 액세스가 감사 됩니다.|
| &nbsp; | &nbsp; |
