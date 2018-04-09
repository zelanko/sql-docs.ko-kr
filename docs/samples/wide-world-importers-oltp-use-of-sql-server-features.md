---
title: SQL Server 기능 및 특성의 사용 | Microsoft Docs
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
ms.assetid: 06f89721-8478-4abc-8ada-e9c73b08bf51
caps.latest.revision: 2
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: d7d50fda2571b90205fbb18aadfb858615ad4f0b
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2018
---
# <a name="use-of-sql-server-features-and-capabilities"></a>SQL Server 기능 및 기능 사용
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
OLTP 데이터베이스의 기능 및 SQL Server 기능의 WideWorldImporters 사용합니다.

WideWorldImporters는 다양 한 SQL Server 2016에 도입 된 최신 기능을 포함 하 여 SQL Server의 주요 기능을 보여 주기 위해 설계 되었습니다. 다음 목록은 SQL Server 기능 및 기능과 WideWorldImporters에서 사용 되는 방법을 설명 합니다.

|SQL Server 기능 또는 기능|WideWorldImporters에서 사용 하 여|
|-----------------------------|---------------------|
|임시 테이블|모든 찾기 스타일 참조 테이블 및 StockItems, 고객 및 공급자와 같은 주요 엔터티를 포함 하 여 많은 임시 테이블이 있습니다. 임시 테이블을 사용 하 여 편리 하 게 추적 하기 위해 이러한 엔터티의 기록을 수 있습니다.|
|JSON에 대 한 AJAX 호출|이러한 테이블을 쿼리 하는 응용 프로그램 자주 사용 하 여 AJAX 호출: 사용자, 고객, 공급 업체와 StockItems 합니다. 호출 하 여 (즉, 반환 되는 데이터의 형식이 JSON 데이터로) JSON 페이로드를 반환 합니다. 저장된 프로시저 예를 들어 참조 `Website.SearchForCustomers`합니다.|
|JSON 속성/값 모음|테이블 수 있는 JSON 데이터를 관계형 데이터 테이블에 확장을 있는 열입니다. 예를 들어 `Application.SystemParameters` 에 응용 프로그램 설정에 대 한 열 및 `Application.People` 에 열이 레코드 사용자 기본 설정 합니다. 이러한 테이블을 사용 하는 `nvarchar(max)` 기본 제공 함수를 사용 하 여 CHECK 제약 조건 함께 JSON 데이터를 기록 하는 열 `ISJSON` 열을 확인 하는 값은 유효한 JSON입니다.|
|행 수준 보안 (RLS)|행 수준 보안 (RLS)은 역할 멤버 자격에 따라 Customers 테이블에 대 한 액세스를 제한 하는 데 사용 됩니다. 각 영업 지역에 역할 및 사용자 있습니다. 이 작업에서 확인 하려면 샘플 script.zip 일부인에서 해당 스크립트를 사용의 [샘플의 릴리스](http://go.microsoft.com/fwlink/?LinkID=800630)합니다.|
|실시간 운영 분석|(데이터베이스의 전체 버전) 코어 트랜잭션 테이블 `Sales.InvoiceLines` 및 `Sales.OrderLines` 운영 워크 로드에 끼치는 영향이 최소화 트랜잭션 데이터베이스에서 효율적인 분석 쿼리 실행을 지원 하기 위해 비클러스터형 columnstore 인덱스 둘 다 합니다. 동일한 데이터베이스에서 트랜잭션 및 분석 실행도 라고 [하이브리드 트랜잭션/Analytical 처리 (HTAP)](https://wikipedia.org/wiki/Hybrid_Transactional/Analytical_Processing_(HTAP))합니다. 이 작업에서 확인 하려면 샘플 script.zip 일부인에서 해당 스크립트를 사용의 [샘플의 릴리스](http://go.microsoft.com/fwlink/?LinkID=800630)합니다.|
|PolyBase|외부 테이블을 사용 하 여 Azure 블로그 저장소에서 호스팅되는 공용 데이터 집합으로 작업에서이 PolyBase를 보려면 샘플 script.zip 일부인에서 해당 스크립트를 사용의 [샘플의 릴리스](http://go.microsoft.com/fwlink/?LinkID=800630)합니다.|
|메모리 내 OLTP|(데이터베이스의 전체 버전) 테이블 형식 되는 모든 메모리 액세스에 최적화 된 테이블 반환 매개 변수 (Tvp) 모든 메모리 최적화를 활용 합니다.<br/><br/>두 개의 모니터링 테이블 `Warehouse.VehicleTemperatures` 및 `Warehouse.ColdRoomTemperatures`, 메모리 액세스에 최적화 됩니다. 이렇게 하면 기존의 디스크 기반 테이블 보다 더 빠른 속도로 채워질 ColdRoomTemperatures 테이블입니다. VehicleTemperatures 테이블 JSON 페이로드를 보유 하 고 IoT 시나리오에 대 한 확장에 있습니다. VehicleTemperatures 테이블 추가 인계 EventHubs, Stream Analytics 및 Power BI를 포함 하는 시나리오입니다.<br/><br/>저장된 프로시저 `Website.RecordColdRoomTemperatures` 콜드 방 온도 기록의 성능을 더욱 향상 시킬 고유 하 게 컴파일됩니다.<br/><br/>메모리 내 OLTP 작업에서 예를 보려면 작업 drivers.zip 일부인에서 차량 위치 작업 부하 드라이버의는 [샘플의 릴리스](http://go.microsoft.com/fwlink/?LinkID=800630)합니다.|
|클러스터형 columnstore 인덱스|(데이터베이스의 전체 버전) 테이블 `Warehouse.StockItemTransactions` 클러스터형된 columnstore 인덱스를 사용 합니다. 이 테이블의 행 수는 커질 하며 크게 클러스터형된 columnstore 인덱스는 테이블의 디스크 크기를 줄일 수 및 쿼리 성능이 향상 됩니다. 삽입만 수정이이 테이블에는--온라인 작업에서이 테이블에 없는 업데이트/삭제 않으며 클러스터형된 columnstore 인덱스 수행 삽입 작업에 효과적입니다.|
|동적 데이터 마스킹|데이터베이스 스키마의 데이터 마스킹에 적용 된 은행 세부 정보에는 테이블에서에서 공급 업체에 대 한 유지 `Purchasing.Suppliers`합니다. Non-admin 인 직원에 체계가이 정보에 액세스할 수 없습니다.|
|항상 암호화|상시 암호화에 대 한 데모 ´ â 포함 되어 있는 다운로드 가능한 samples.zip의는 [샘플의 릴리스](http://go.microsoft.com/fwlink/?LinkID=800630)... 이 데모는 암호화 키를 암호화를 사용 하 여 중요 한 데이터 및 데이터 테이블에 삽입 하는 작은 샘플 응용 프로그램에 대 한 테이블을 만듭니다.|
|스트레치 데이터베이스|`Warehouse.ColdRoomTemperatures` 테이블을 임시 테이블로 구현 및 예제 데이터베이스의 전체 버전에서 메모리 최적화 합니다. 보관 테이블은 디스크 기반 및 Azure로 확장할 수 있습니다.|
|전체 텍스트 인덱스|전체 텍스트 인덱스에는 사용자, 고객 및 StockItems 검색 향상 시킵니다. 전체 텍스트 인덱싱에 SQL Server 인스턴스에 설치 되어 있는 경우에 인덱스 쿼리에 적용 됩니다. 비 영구적인 계산된 열이 전체 텍스트 인덱싱된 StockItems 테이블에 있는 데이터를 만들기 위해 사용 됩니다.<br/><br/>`CONCAT` 전체 텍스트 인덱스는 SearchData 만들려는 필드를 연결 하는 데 사용 됩니다.<br/>샘플에 전체 텍스트 인덱스의 사용을 사용 하도록 설정 하려면 데이터베이스에 다음 문을 실행 합니다.<br/><br/>    `EXECUTE [Application].[Configuration_ConfigureFullTextIndexing]`<br/><br/>프로시저는 만듭니다 기본 전체 텍스트 카탈로그 하나 존재 하지 않는 한 다음 그 뷰의 전체 텍스트 버전 검색 뷰를 대체 하는 경우).<br/><br/>참고 SQL Server에서 전체 텍스트 인덱스를 사용 해야 한다는 설치 하는 동안 전체 텍스트 옵션을 선택 합니다. Azure SQL 데이터베이스 필요 하지 않습니다 및 전체 텍스트 인덱스를 활성화 하려면 특정 구성입니다.|
|인덱싱된 지속형된 계산된 열|SupplierTransactions 및 CustomerTransactions에 사용 되는 지속형된 계산된 열 인덱스입니다.|
|CHECK 제약 조건|상대적으로 복잡 한 check 제약 조건을 중인 `Sales.SpecialDeals`합니다. 이렇게 하면 둘 중 하나만 DiscountAmount, DiscountPercentage, 및 UnitPrice 구성 됩니다.|
|Unique 제약 조건|많은 생성 (및 unique 제약 조건)에 게 다 Warehouse.StockItemStockGroups'에 대 한 설정 되어 있습니다.|
|테이블 분|(데이터베이스의 전체 버전) 테이블 `Sales.CustomerTransactions` 및 `Purchasing.SupplierTransactions` 파티션 함수를 사용 하 여 연도별로 분할 된 `PF_TransactionDate` 및 파티션 구성표 `PS_TransactionDate`합니다. 분할 큰 테이블의 관리 효율성을 개선 하기 위해 사용 됩니다.|
|목록 처리|예제에서는 테이블 형식 `Website.OrderIDList` 제공 됩니다. 예제 프로시저에 의해 사용 되는 `Website.InvoiceCustomerOrders`합니다. 프로시저를 사용 하 여 공통 테이블 식 (Cte), TRY/CATCH, JSON_MODIFY, XACT_ABORT, NOCOUNT, THROW 및 XACT_STATE 주문을 응용 프로그램을 데이터베이스 엔진에서 왕복을 최소화 하기 위해 단일 주문만 하지 않고 목록 처리 하는 기능을 보여 줍니다.|
|GZip 압축|`Warehouse.VehicleTemperature`의테이블 전체 센서 데이터를 보유 하지만이 데이터는 여러 개월을 하는 경우 GZip 압축을 사용 하는 압축 함수를 사용 하 여 공간을 절약 하기 위해 압축 됩니다.<br/><br/>보기 `Website.VehicleTemperatures` 이전에 압축 된 데이터를 검색할 때 DECOMPRESS 함수를 사용 하 여 합니다.|
|쿼리 저장소|쿼리 저장소 데이터베이스에서 사용 됩니다. 몇 가지 쿼리를 실행 한 후 노드를 데이터베이스에서 사용 중인 쿼리 저장소, Management Studio에서 데이터베이스를 열고, 열고 보고서 쿼리 실행 및 실행 하는 쿼리에 대 한 계획을 보려면 상위 리소스 소비 쿼리를 엽니다.|
|STRING_SPLIT|열 `DeliveryInstructions` 표에 `Sales.Invoices`STRING_SPLIT 보여 주기 위해 사용할 수 있는 쉼표로 구분 된 값이 있습니다.|
|감사|데이터베이스에 다음 문을 실행 하 여이 예제 데이터베이스에 대 한 SQL Server Audit은 활성화할 수 있습니다.<br/><br/>    `EXECUTE [Application].[Configuration_ApplyAuditing]`<br/><br/>Azure SQL 데이터베이스에서 감사가 설정 되어 있지만 통해는 [Azure 포털](https://portal.azure.com/)합니다.<br/><br/>보안 연산의 로그인, 역할 및 사용 권한 위치 설정 (standard edition 시스템)는 포함 하는 모든 시스템에 기록 됩니다. 감사는 모든 시스템에서 사용할 수 있으며 추가 권한이 필요 하지 않습니다 때문에 응용 프로그램 로그에 전송 됩니다. 경고 보안을 강화 하기 리디렉션되어야 보안 로그 또는 파일은 안전한 폴더에 있다고 가정 됩니다. 필요한 추가 구성을 설명 하는 링크가 제공 됩니다.<br/><br/>엔터프라이즈 개발자/평가/버전 시스템에 대 한 모든 금융 트랜잭션 데이터에 대 한 액세스 감사 됩니다.|
