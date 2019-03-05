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
manager: craigg
ms.openlocfilehash: 914ec6be6d73bf6411a700ab6fc9586743c40527
ms.sourcegitcommit: 2663063e29f2868ee6b6d596df4b2af2d22ade6f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/04/2019
ms.locfileid: "57305351"
---
# <a name="use-of-sql-server-features-and-capabilities"></a>SQL Server 기능 및 기능 사용

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

WideWorldImporters 가지 OLTP 데이터베이스에서 SQL Server 기능을 사용합니다.

WideWorldImporters는 다양 한 SQL Server 2016에 도입 된 최신 기능을 포함 하 여 SQL Server의 주요 기능을 보여 주도록 설계 되었습니다. 다음 표에서 SQL Server의 특징과 기능을 나열합니다. 각 행에는 또한 기능 WideWorldImporters에서 사용 하는 방법에 대 한 설명을 제공 합니다.  
&nbsp;

|SQL Server 기능 또는 특징|WideWorldImporters에서 사용 하 여|
|:-------------------------------|:------------------------|
|임시 테이블|모든 조회 스타일 참조 테이블 및 StockItems, 고객 및 공급 업체와 같은 주요 엔터티를 포함 하 여 temporal 테이블을 있습니다. Temporal 테이블을 사용 하 여 편리 하 게 추적 하기 위해 이러한 엔터티의 기록을 수 있습니다.|
|JSON에 대 한 AJAX 호출|자주 응용 프로그램 AJAX 호출을 사용 하 여 이러한 테이블을 쿼리하려면: 사용자, 고객, 공급 업체 및 StockItems 합니다. 호출 하 여 JSON 형식으로 데이터를 반환합니다. 예를 들어 저장된 프로시저를 참조 `Website.SearchForCustomers`합니다.|
|JSON 속성/값 모음|여러 테이블 열 테이블의 관계형 데이터를 확장 하는 JSON 데이터를 보유 하는 경우 예를 들어 `Application.SystemParameters` 에 응용 프로그램 설정에 대 한 열 및 `Application.People` 에 열이 레코드 사용자 기본 설정 합니다. 이러한 테이블 사용을 `nvarchar(max)` 기본 제공 함수를 사용 하 여 CHECK 제약 조건 함께 JSON 데이터를 기록 하는 열 `ISJSON` 열을 확인 하는 값은 유효한 JSON입니다.|
|행 수준 보안 (RLS)|행 수준 보안 (RLS)은 역할 멤버 자격에 따라 고객에 게 테이블에 대 한 액세스를 제한 하는 데 사용 됩니다. 각 영업 지역에 역할 및 사용자 있습니다. RLS 액세스 중인 제한, 해당 스크립트를 사용 하 여 샘플-script.zip에서 보려는 일부인 합니다 [샘플의 릴리스](https://go.microsoft.com/fwlink/?LinkID=800630)합니다.|
|실시간 운영 분석|(데이터베이스의 전체 버전) 핵심 트랜잭션 테이블 `Sales.InvoiceLines` 고 `Sales.OrderLines` 운영 워크 로드에 영향을 최소화 하면서 트랜잭션 데이터베이스에서 분석 쿼리의 효율적인 실행을 지원 하도록 비클러스터형 columnstore 인덱스를 둘 다. 동일한 데이터베이스에서 트랜잭션 및 분석을 실행는 라고도 [하이브리드 트랜잭션/분석 처리 (HTAP)](https://wikipedia.org/wiki/Hybrid_Transactional/Analytical_Processing_(HTAP))합니다. 이 실행 중인 확인 하려면 샘플 script.zip 일부인에서 해당 스크립트를 사용의 합니다 [샘플의 릴리스](https://go.microsoft.com/fwlink/?LinkID=800630)합니다.|
|PolyBase|작업에서이 PolyBase 외부 테이블을 사용 하 여 Azure 블로그 저장소에서 호스트 되는 공용 데이터 집합을 사용 하 여 보려는 샘플 script.zip 일부인에서 해당 스크립트를 사용의 합니다 [샘플의 릴리스](https://go.microsoft.com/fwlink/?LinkID=800630)합니다.|
|메모리 내 OLTP|(데이터베이스의 전체 버전) 테이블 형식은 테이블 반환 매개 변수 (Tvp) 모든 메모리 액세스에 최적화에서 이점을 얻을 수 있도록 모든 메모리 최적화 됩니다.<br/><br/>두 모니터링 테이블 `Warehouse.VehicleTemperatures` 및 `Warehouse.ColdRoomTemperatures`, 메모리 액세스에 최적화 됩니다. 메모리 최적화 ColdRoomTemperatures은 기존의 디스크 기반 테이블 보다 더 빠른 속도로 채워질 수 있습니다. VehicleTemperatures 테이블 JSON 페이로드 포함 및 IoT 시나리오를 위한 확장 프로그램에 적합 합니다. VehicleTemperatures 테이블 추가 event Hubs, Stream Analytics 및 Power BI를 포함 하는 시나리오에 적합 합니다.<br/><br/>저장된 프로시저 `Website.RecordColdRoomTemperatures` 콜드 방 온도 기록의 성능을 높이기 위해 고유 하 게 컴파일됩니다.<br/><br/>작업의 메모리 내 OLTP의 예제를 보려면 drivers.zip 워크 로드에 참가 하는 지정 된 차량 위치 작업 드라이버의 합니다 [샘플의 릴리스](https://go.microsoft.com/fwlink/?LinkID=800630)합니다.|
|클러스터형 columnstore 인덱스|(데이터베이스의 전체 버전) 테이블 `Warehouse.StockItemTransactions` 클러스터형된 columnstore 인덱스를 사용 합니다. 이 테이블의 행 수가 큰 경우 성장할 것으로 예상 되 고 클러스터형된 columnstore 인덱스를 크게 테이블의 디스크 크기를 줄입니다. 쿼리 성능이 향상 됩니다. 삽입만 수정이이 테이블에는-온라인 워크 로드-이 테이블에 없는 업데이트/삭제 되며 클러스터형된 columnstore 인덱스 삽입 작업에 대 한 잘 수행 합니다.|
|동적 데이터 마스킹|데이터베이스 스키마의 데이터 마스킹에 적용 된 테이블에 공급 업체에 대 한 저장 된 은행 정보 `Purchasing.Suppliers`합니다. 비관리자 직원이이 정보에 액세스할을 수 없습니다.|
|항상 암호화|Always Encrypted에 대 한 데모 참가 하는 다운로드 가능한 samples.zip에 포함 된의 합니다 [샘플의 릴리스](https://go.microsoft.com/fwlink/?LinkID=800630)합니다. 데모는 암호화 키를 암호화를 사용 하 여 중요 한 데이터 및 테이블에 데이터를 삽입 하는 작은 샘플 응용 프로그램에 대 한 테이블을 만듭니다.|
|스트레치 데이터베이스|`Warehouse.ColdRoomTemperatures` 테이블을 temporal 테이블로 구현 되었습니다 및 예제 데이터베이스의 전체 버전에서 메모리 최적화 합니다. 보관은 디스크 기반 테이블과 Azure에 스트레치할 수 있습니다.|
|전체 텍스트 인덱스|전체 텍스트 인덱스에는 사용자, 고객 및 StockItems 검색 향상 시킵니다. 전체 텍스트 인덱싱에 SQL Server 인스턴스에 설치 되어 있는 경우에 인덱스를 쿼리에 적용 됩니다. 비영구적 계산된 열이 전체 텍스트 인덱싱 StockItems 테이블에 데이터를 만들기 위해 사용 됩니다.<br/><br/>`CONCAT` 전체 텍스트 인덱스는 SearchData 만들려면 필드를 연결 하는 데 사용 됩니다.<br/>샘플의 전체 텍스트 인덱스의 사용을 사용 하려면 데이터베이스에 다음 문을 실행 합니다.<br/><br/>`EXECUTE [Application].[Configuration_ConfigureFullTextIndexing]`<br/><br/>프로시저는 만듭니다 기본 전체 텍스트 카탈로그 하나 존재 하지 않는 한 다음 그 뷰의 전체 텍스트 버전을 사용 하 여 검색 뷰를 대체 하는 경우).<br/><br/>참고를 설치 하는 동안 전체 텍스트 옵션을 선택 하는 SQL Server에서 전체 텍스트 인덱스를 사용 해야 합니다. Azure SQL Database는 필요 하지 않습니다 및 전체 텍스트 인덱스를 사용 하도록 설정 하기 위한 특정 구성이 있습니다.|
|지속형된 계산된 열 인덱싱|SupplierTransactions CustomerTransactions에 사용 되는 지속형된 계산된 열을 인덱스.|
|CHECK 제약 조건|상대적으로 복잡 한 check 제약 조건에 `Sales.SpecialDeals`입니다. 이렇게 하면 하나 및 하나만 DiscountAmount, DiscountPercentage 하 고 UnitPrice 구성 됩니다.|
|Unique 제약 조건|많은 생성 (및 unique 제약 조건)에 다는 설정 `Warehouse.StockItemStockGroups`합니다.|
|테이블 분|(데이터베이스의 전체 버전) 테이블 `Sales.CustomerTransactions` 하 고 `Purchasing.SupplierTransactions` 파티션 함수를 사용 하 여 연도별로 분할 되 `PF_TransactionDate` 및 파티션 구성표 `PS_TransactionDate`합니다. 분할은 큰 테이블의 관리 효율성을 개선 하기 위해 사용 됩니다.|
|목록 처리|예제 테이블 형식 `Website.OrderIDList` 제공 됩니다. 예제 프로시저를 사용 하 고 `Website.InvoiceCustomerOrders`입니다. 에 응용 프로그램에서 왕복을 최소화 하기 위해 단일 주문 것 보다는 주문 목록을 처리 기능을 보여 줍니다 공통 테이블 식 (Cte), TRY/CATCH, JSON_MODIFY, XACT_ABORT, NOCOUNT, THROW 및 XACT_STATE를 사용 하는 절차는 데이터베이스 엔진입니다.|
|GZip 압축|에 `Warehouse.VehicleTemperature` 뷰에서 해당 테이블 전체 센서 데이터를 보유 합니다. 하지만이 데이터가 이전 몇 개월 경우 공간을 절약 하기 위해 압축 됩니다. COMPRESS 함수는 GZip 압축을 사용합니다.<br/><br/>뷰 `Website.VehicleTemperatures` 이전에 압축 된 데이터를 검색할 때 DECOMPRESS 함수를 사용 합니다.|
|쿼리 저장소|쿼리 저장소는 데이터베이스에 사용 됩니다. 몇 가지 쿼리를 실행 한 후 다음 단계를 수행 합니다.<br/><br/>1. Management Studio에서 데이터베이스를 엽니다.<br/>2. 쿼리 저장소 데이터베이스 아래에 있는 노드를 엽니다.<br/>3. 보고서를 엽니다 *상위 리소스 소비 쿼리*합니다. 쿼리 실행을 참조 하 고 방금 실행 한 쿼리에 대 한 계획을 확인 하세요.|
|STRING_SPLIT|열 `DeliveryInstructions` 표에 `Sales.Invoices` STRING_SPLIT를 보여 주기 위해 사용할 수 있는 쉼표로 구분 된 값입니다.|
|감사|SQL Server Audit는 데이터베이스에서 다음 문을 실행 하 여이 샘플 데이터베이스에 대해 활성화할 수 있습니다.<br/><br/>`EXECUTE [Application].[Configuration_ApplyAuditing]`<br/><br/>Azure SQL Database에서 감사를 사용할 수를 통해 합니다 [Azure portal](https://portal.azure.com/)합니다.<br/><br/>로그인 관련 된 보안 작업, 역할 및 사용 권한 (standard edition 시스템) 포함 하 여 감사를 사용할 수 있는 모든 시스템에 기록 됩니다. 감사 모든 시스템에서 사용할 수 있으며 추가 권한이 필요 하지 않습니다 때문에 응용 프로그램 로그로 전달 됩니다. 경고 하는 보안을 강화 하기를 리디렉션해야 할 보안 로그 또는 파일을 보안 폴더에 있습니다. 필요한 추가 구성을 설명 하는 링크가 제공 됩니다.<br/><br/>평가/개발자/enterprise edition 시스템에 대 한 모든 재무 트랜잭션 데이터에 대 한 액세스 감사 됩니다.|
| &nbsp; | &nbsp; |
