---
title: "메모리 내 OLTP에 대한 예제 데이터베이스 | Microsoft 문서"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: df347f9b-b950-4e3a-85f4-b9f21735eae3
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9f9957d4c83ce351e49224fcd2bc499a5aa777dd
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="sample-database-for-in-memory-oltp"></a>메모리 내 OLTP에 대한 예제 데이터베이스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
    
## <a name="overview"></a>개요  
 이 샘플에서는 메모리 내 OLTP 기능을 소개합니다. 이 예제는 메모리 액세스에 최적화된 테이블과 고유하게 컴파일된 저장 프로시저를 보여 주며, 메모리 내 OLTP의 성능 이점을 설명하는 데 사용할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에 대한 이 항목을 보려면 [메모리 내 OLTP를 보여주기 위한 AdventureWorks 확장](https://msdn.microsoft.com/library/dn511655\(v=sql.120\).aspx)을 참조하세요.  
  
 또한 AdventureWorks 데이터베이스의 5개 테이블을 메모리 액세스에 최적화된 테이블로 마이그레이션하며, 판매 주문 처리용 데모 작업을 포함하고 있습니다. 이 데모 작업을 사용하여 서버에서 메모리 내 OLTP를 사용하는 경우의 성능 이점을 확인할 수 있습니다.  
  
 샘플에 대한 설명에서는 테이블을 메모리 내 OLTP로 마이그레이션할 때 메모리 액세스에 최적화된 테이블에 아직 지원되지 않는 기능을 보완하기 위해 수행한 절충 작업에 대해 설명합니다.  
  
 이 샘플에 대한 설명서는 다음과 같이 구성되어 있습니다.  
  
-   샘플을 설치하고 데모 워크로드를 실행하기 위한[필수 조건](#Prerequisites)  
  
-   [Installing the In-Memory OLTP sample based on AdventureWorks](#InstallingtheIn-MemoryOLTPsamplebasedonAdventureWorks)지침  
  
-   [예제 테이블 및 프로시저에 대한 설명](#Descriptionofthesampletablesandprocedures) – 메모리 내 OLTP 샘플에서 AdventureWorks에 추가한 테이블 및 프로시저에 대한 설명과 원래 AdventureWorks 테이블을 메모리 액세스에 최적화된 테이블로 마이그레이션하기 위한 고려 사항이 포함되어 있습니다.  
  
-   [데모 작업을 사용한 성능 측정](#PerformanceMeasurementsusingtheDemoWorkload) 을 수행하기 위한 지침 – 데모 작업 자체를 실행하기 위한 지침뿐만 아니라 작업을 추진하는 데 사용되는 도구인 ostress를 설치하고 실행하기 위한 지침이 포함되어 있습니다.  
  
-   [샘플의 메모리 및 디스크 공간 사용률](#MemoryandDiskSpaceUtilizationintheSample)  
  
##  <a name="Prerequisites"></a> Prerequisites  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
-   성능 테스트에 사용할, 프로덕션 환경과 유사한 사양을 가진 서버 이 특정 샘플의 경우 SQL Server에 사용할 수 있는 메모리가 16GB 이상 있어야 합니다. 메모리 내 OLTP의 하드웨어에 대한 일반 지침은 다음 블로그 게시물을 참조하세요.[http://blogs.technet.com/b/dataplatforminsider/archive/2013/08/01/hardware-considerations-for-in-memory-oltp-in-sql-server-2014.aspx](http://blogs.technet.com/b/dataplatforminsider/archive/2013/08/01/hardware-considerations-for-in-memory-oltp-in-sql-server-2014.aspx)  
  
##  <a name="InstallingtheIn-MemoryOLTPsamplebasedonAdventureWorks"></a> Installing the In-Memory OLTP sample based on AdventureWorks  
 다음 단계를 수행하여 예제를 설치합니다.  
  
1.  [https://www.microsoft.com/download/details.aspx?id=49502](https://www.microsoft.com/download/details.aspx?id=49502) 에서 로컬 폴더(예: 'c:\temp')에 AdventureWorks2016CTP3.bak 및 SQLServer2016CTP3Samples.zip을 다운로드합니다.  
  
2.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 데이터베이스 백업을 복원합니다.  
  
    1.  다음 예와 같은 데이터 파일의 대상 폴더와 파일 이름을 식별합니다.  
  
         'h:\DATA\AdventureWorks2016CTP3_Data.mdf'  
  
    2.  다음 예와 같은 로그 파일의 대상 폴더와 파일 이름을 식별합니다.  
  
         'i:\DATA\AdventureWorks2016CTP3_log.ldf'  
  
        1.  로그 파일은 데이터 파일과 다른 드라이브에 배치되어야 합니다. 최상의 성능을 위해 SSD 또는 PCIe 저장소와 같이 대기 시간이 적은 드라이브가 이상적입니다.  
  
     T-SQL 스크립트 예:  
  
    ```  
    RESTORE DATABASE [AdventureWorks2016CTP3]   
      FROM DISK = N'C:\temp\AdventureWorks2016CTP3.bak'   
        WITH FILE = 1,    
      MOVE N'AdventureWorks2016_Data' TO N'h:\DATA\AdventureWorks2016CTP3_Data.mdf',    
      MOVE N'AdventureWorks2016_Log' TO N'i:\DATA\AdventureWorks2016CTP3_log.ldf',  
      MOVE N'AdventureWorks2016CTP3_mod' TO N'h:\data\AdventureWorks2016CTP3_mod'  
     GO  
    ```  
  
3.  샘플 스크립트와 워크로드를 보려면 로컬 폴더에 SQLServer2016CTP3Samples.zip 파일의 압축을 풉니다. 워크로드 실행에 대한 지침은 In-Memory OLTP\readme.txt 파일을 참조하세요.  
  
##  <a name="Descriptionofthesampletablesandprocedures"></a> Description of the sample tables and procedures  
 예제에서는 AdventureWorks의 기존 테이블을 기반으로 제품과 판매 주문에 대한 새 테이블을 만듭니다. 새 테이블의 스키마는 아래에 설명된 대로 몇 가지 차이점이 있지만 기존 테이블과 유사합니다.  
  
 새로운 메모리 액세스에 최적화된 테이블에는 ‘_inmem’ 접미사가 붙습니다. 예제에는 '_ondisk' 접미사가 붙는 해당 테이블도 포함되어 있습니다. 이러한 테이블을 사용하여 시스템에서 메모리 액세스에 최적화된 테이블과 디스크 기반 테이블의 성능을 일 대 일로 비교할 수 있습니다.  
  
 성능 비교를 위한 작업에서 사용되는 메모리 액세스에 최적화된 테이블은 완전한 내구성을 가지며 모두 기록됩니다. 이러한 테이블은 성능 이점을 얻기 위해 내구성이나 안정성을 희생하지 않습니다.  
  
 이 예제의 대상 작업은 판매 주문 처리이므로 제품 및 할인에 대한 정보도 고려하며, 이를 위해 SalesOrderHeader, SalesOrderDetail, Product, SpecialOffer 및 SpecialOfferProduct 테이블이 사용됩니다.  
  
 두 가지 새로운 저장 프로시저 Sales.usp_InsertSalesOrder_inmem 및 Sales.usp_UpdateSalesOrderShipInfo_inmem은 판매 주문을 삽입하고 지정된 판매 주문의 배송 정보를 업데이트하는 데 사용됩니다.  
  
 새로운 스키마 'Demo'에는 데모 작업을 실행하기 위한 도우미 테이블과 저장 프로시저가 포함되어 있습니다.  
  
 구체적으로 설명하자면 메모리 내 OLTP 샘플에서는 다음 개체를 AdventureWorks에 추가합니다.  
  
### <a name="tables-added-by-the-sample"></a>예제에서 추가된 테이블  
  
#### <a name="the-new-tables"></a>새로운 테이블  
 Sales.SalesOrderHeader_inmem  
  
-   판매 주문에 대한 머리글 정보. 각 판매 주문에 해당하는 행이 이 테이블에 하나씩 있습니다.  
  
 Sales.SalesOrderDetail_inmem  
  
-   판매 주문에 대한 세부 정보. 판매 주문의 각 품목에 해당하는 행이 이 테이블에 하나씩 있습니다.  
  
 Sales.SpecialOffer_inmem  
  
-   각 특별 행사와 관련된 할인율을 비롯한 특별 행사에 대한 정보.  
  
 Sales.SpecialOfferProduct_inmem  
  
-   특별 행상 및 제품 간의 참조 테이블. 각 특별 행사에는 제품이 0개 이상 있을 수 있으며 각 제품은 0개 이상의 특별 행사에 포함될 수 있습니다.  
  
 Production.Product_inmem  
  
-   가격을 비롯한 제품에 대한 정보  
  
 Demo.DemoSalesOrderDetailSeed  
  
-   예제 판매 주문을 생성하기 위해 데모 작업에서 사용됩니다.  
  
 테이블의 디스크 기반 변형:  
  
-   Sales.SalesOrderHeader_ondisk  
  
-   Sales.SalesOrderDetail_ondisk  
  
-   Sales.SpecialOffer_ondisk  
  
-   Sales.SpecialOfferProduct_ondisk  
  
-   Production.Product_ondisk  
  
#### <a name="differences-between-original-disk-based-and-the-and-new-memory-optimized-tables"></a>원래 디스크 기반 테이블과 새로운 메모리 액세스에 최적화된 테이블 간의 차이점  
 대부분의 경우 이 예제에서 도입한 새로운 테이블은 원래 테이블과 동일한 열 및 동일한 데이터 형식을 사용하지만 몇 가지 차이점이 있습니다. 이러한 차이점과 변경에 대한 이유는 다음과 같습니다.  
  
 Sales.SalesOrderHeader_inmem  
  
-   *기본 제약 조건* 은 메모리 액세스에 최적화된 테이블에 지원되며 대부분의 기본 제약 조건은 있는 그대로 마이그레이션되었습니다. 그러나 원래 테이블 Sales.SalesOrderHeader에는 OrderDate 및 ModifiedDate 열에 대한 현재 날짜를 검색하는 두 가지 기본 제약 조건이 포함되어 있습니다. 동시 작업과 처리량이 많은 주문 처리 작업에서 전역 리소스는 경합 지점이 될 수 있습니다. 시스템 시간은 이러한 전역 리소스이며 판매 주문을 삽입하는 메모리 내 OLTP 작업을 실행할 때 병목 현상을 발생시킬 수 있다는 사실이 관찰되었습니다. 이는 판매 주문 정보뿐만 아니라 판매 주문 머리글의 여러 열에 대해 시스템 시간을 검색해야 하는 경우 특히 해당하는 사실입니다. 이러한 문제는 이 예제에서 삽입되는 각 판매 주문에 대해 시스템 시간을 한 번만 검색하고 Sales.usp_InsertSalesOrder_inmem 저장 프로시저에서 SalesOrderHeader_inmem 및 SalesOrderDetail_inmem의 datetime 열에 이 값을 사용하여 해결되었습니다.  
  
-   *별칭 UDT* - 원래 테이블은 PurchaseOrderNumber 및 AccountNumber 열에 대해 두 가지 별칭 UDT(사용자 정의 데이터 형식)인 dbo.OrderNumber 및 dbo.AccountNumber를 각각 사용합니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 에서는 메모리 액세스에 최적화된 테이블에 대한 별칭 UDT를 지원하지 않으므로 새 테이블은 시스템 데이터 형식 nvarchar(25) 및 nvarchar(15)을 각각 사용합니다.  
  
-   *인덱스 키의 Null 허용 열* - 원래 테이블에서 SalesPersonID 열은 Null을 허용하지만 새 테이블에서 이 열은 Null을 허용하지 않으며 값(-1)을 사용하는 기본 제약 조건을 갖습니다. 이는 메모리 액세스에 최적화된 테이블에 대한 인덱스의 경우 인덱스 키에 Null 허용 열이 있을 수 없기 때문이며, 이 경우 -1은 NULL의 대리 값입니다.  
  
-   *계산 열* - [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 에서는 메모리 액세스에 최적화된 테이블에서 계산 열을 지원하지 않기 때문에 계산 열 SalesOrderNumber 및 TotalDue가 생략되었습니다. 새로운 뷰 Sales.vSalesOrderHeader_extended_inmem이 SalesOrderNumber 및 TotalDue 열을 반영하므로 이러한 열이 필요한 경우 이 뷰를 사용할 수 있습니다.  

    - **Applies to:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.  
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1부터 계산 열이 메모리 액세스에 최적화된 테이블 및 인덱스에서 지원됩니다.

  
-   *외래 키 제약 조건* 은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 메모리 액세스에 최적화된 테이블에 지원되지만 참조된 테이블도 메모리 액세스에 최적화된 경우에만 지원됩니다. 메모리 액세스에 최적화된 테이블로 마이그레이션된 테이블을 참조하는 외래 키는 마이그레이션된 테이블에 유지되지만 다른 외래 키는 생략됩니다.  또한 SalesOrderHeader_inmem은 예제 작업에서 핫 테이블이며, FOREIGN KEY 제약 조건을 지정하려면 모든 DML 작업에 대한 추가 처리가 필요합니다. 이는 이러한 제약 조건에서 참조된 다른 모든 테이블에서 조회가 필요하기 때문입니다. 따라서 응용 프로그램에서 Sales.SalesOrderHeader_inmem 테이블에 대한 참조 무결성을 보장하며 참조 무결성은 행이 삽입될 때 확인되지 않는다고 가정합니다.  
  
-   *Rowguid* - rowguid 열이 생략되었습니다. uniqueidentifier가 메모리 액세스에 최적화된 테이블에 지원되지만 ROWGUIDCOL 옵션은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 지원되지 않습니다. 이러한 종류의 열은 일반적으로 병합 복제나 filestream 열이 있는 테이블에 사용됩니다. 이 예제에는 둘 다 포함되어 있지 않습니다.  
  
 Sales.SalesOrderDetail  
  
-   *기본 제약 조건* - SalesOrderHeader와 유사하게 시스템 날짜/시간을 필요로 하는 기본 제약 조건은 마이그레이션되지 않으며, 대신 판매 주문을 삽입하는 저장 프로시저가 첫 번째 삽입 시 현재 시스템 날짜/시간을 삽입하는 작업을 처리합니다.  
  
-   *계산 열* - 계산 열이 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 메모리 액세스에 최적화된 테이블에 지원되지 않기 때문에 계산 열 LineTotal이 마이그레이션되지 않았습니다. 이 열에 액세스하려면 Sales.vSalesOrderDetail_extended_inmem 뷰를 사용합니다.  
  
-   *Rowguid* - rowguid 열이 생략되었습니다. 자세한 내용은 SalesOrderHeader 테이블에 대한 설명을 참조하세요.  
  
 Production.Product  
  
-   *별칭 UDT* - 원래 테이블은 시스템 데이터 형식 bit와 동일한 사용자 정의 데이터 형식 dbo.Flag를 사용합니다. 마이그레이션된 테이블은 bit 데이터 형식을 대신 사용합니다.  
  
-   *Rowguid* - rowguid 열이 생략되었습니다. 자세한 내용은 SalesOrderHeader 테이블에 대한 설명을 참조하세요.  
  
 Sales.SpecialOffer  
  
-   *Rowguid* - rowguid 열이 생략되었습니다. 자세한 내용은 SalesOrderHeader 테이블에 대한 설명을 참조하세요.  
  
 Sales.SpecialOfferProduct  
  
-   *Rowguid* - rowguid 열이 생략되었습니다. 자세한 내용은 SalesOrderHeader 테이블에 대한 설명을 참조하세요.  
  
#### <a name="considerations-for-indexes-on-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블의 인덱스에 대한 고려 사항  
 메모리 액세스에 최적화된 테이블의 기준 인덱스는 포인트 조회(같음 조건자의 인덱스 검색), 범위 검색(같지 않음 조건자의 인덱스 검색), 전체 인덱스 검색 및 정렬된 검색을 지원하는 비클러스터형 인덱스입니다. 또한 비클러스터형 인덱스는 인덱스 키의 선행 열에 대한 검색을 지원합니다. 메모리 액세스에 최적화된 비클러스터형 인덱스는 역방향 검색만 제외하고 디스크 기반 비클러스터형 인덱스가 지원하는 모든 작업을 지원합니다. 따라서 비클러스터형 인덱스의 사용은 인덱스에 선택할 수 있는 안전한 방법입니다.  
  
 해시 인덱스를 사용하여 작업을 추가로 최적화할 수 있습니다. 해시 인덱스는 포인트 조회와 행 삽입에 대해 특히 최적화됩니다. 그러나 해시 인덱스가 범위 검색, 정렬된 검색 또는 선행 인덱스 키 열에 대한 검색을 지원하지 않는다는 점을 고려해야 합니다. 따라서 이러한 인덱스를 사용할 때는 주의를 기울여야 합니다. 또한 만들 때 bucket_count를 지정해야 합니다. bucket_count는 일반적으로 인덱스 키 값의 수와 그 두 배 사이에서 설정되어야 하지만 더 많이 추정해도 대개 문제가 되지 않습니다.  
  
 [인덱스 지침](http://technet.microsoft.com/library/dn133166\(v=sql.120\).aspx) 과 [올바른 bucket_count 선택](http://technet.microsoft.com/library/dn494956\(v=sql.120\).aspx)지침에 대한 자세한 내용은 온라인 설명서를 참조하세요.  
  
 마이그레이션된 테이블의 인덱스는 데모 판매 주문 처리 작업에 맞게 조정되었습니다. 작업은 Sales.SalesOrderHeader_inmem 및 Sales.SalesOrderDetail_inmem 테이블의 삽입 및 포인트 조회에 의존하며 Production.Product_inmem 및 Sales.SpecialOffer_inmem 테이블에서 기본 키 열에 대한 포인트 조회에도 의존합니다.  
  
 Sales.SalesOrderHeader_inmem에는 세 가지 인덱스가 있는데 정렬된 검색이나 범위 검색이 작업에 필요하지 않기 때문에 모두 성능상의 이유로 해시 인덱스입니다.  
  
-   (SalesOrderID)의 해시 인덱스: 예상된 판매 주문 수가 1,000만 개이기 때문에 bucket_count의 크기는 1,000만(1,600만으로 반올림됨)으로 설정됩니다.  
  
-   (SalesPersonID)의 해시 인덱스: bucket_count가 100만입니다. 제공된 데이터 집합에는 많은 영업 사원이 없지만, 이후 성장을 허용할 수 있으며 bucket_count의 크기가 과도하게 설정된 경우 포인트 조회에 대한 성능 저하가 발생하지 않습니다.  
  
-   (CustomerID)의 해시 인덱스: bucket_count가 100만입니다. 제공된 데이터 집합에는 많은 고객이 없지만 이후 성장을 허용할 수 있습니다.  
  
 Sales.SalesOrderDetail_inmem에는 세 가지 인덱스가 있는데 정렬된 검색이나 범위 검색이 작업에 필요하지 않기 때문에 모두 성능상의 이유로 해시 인덱스입니다.  
  
-   (SalesOrderID, SalesOrderDetailID)의 해시 인덱스: 기본 키 인덱스이며 (SalesOrderID, SalesOrderDetailID)의 조회가 빈번하지는 않지만 키에 해시 인덱스를 사용하면 행 삽입이 빨라집니다. bucket_count 크기 5,000만(6,700만으로 반올림됨): 예상 판매 주문 수가 1,000만 개이므로 이 크기에는 주문당 평균 5개 품목이 있을 수 있습니다.  
  
-   (SalesOrderID)의 해시 인덱스: 단일 주문에 해당하는 모든 품목을 찾으려고 합니다.  예상된 판매 주문 수가 1,000만 개이기 때문에 bucket_count의 크기는 1,000만(1,600만으로 반올림됨)으로 설정됩니다.  
  
-   (ProductID)의 해시 인덱스: bucket_count가 100만입니다. 제공된 데이터 집합에는 많은 제품이 없지만 이후 성장을 허용할 수 있습니다.  
  
 Production.Product_inmem에는 세 가지 인덱스가 있습니다.  
  
-   (ProductID)의 해시 인덱스: ProductID의 조회가 데모 작업의 중요 경로에 있으므로 해시 인덱스가 사용됩니다.  
  
-   (Name)의 비클러스터형 인덱스: 제품 이름의 정렬된 검색을 허용합니다.  
  
-   (ProductNumber)의 비클러스터형 인덱스: 제품 번호의 정렬된 검색을 허용합니다.  
  
 Sales.SpecialOffer_inmem에는 (SpecialOfferID)의 해시 인덱스가 하나 있습니다. 특별 행사의 포인트 조회는 데모 작업의 중요한 부분에 있습니다. bucket_count의 크기는 이후 성장을 허용하기 위해 100만으로 설정됩니다.  
  
 Sales.SpecialOfferProduct_inmem은 데모 작업에서 참조되지 않으므로 작업을 최적화하기 위해 이 테이블에 해시 인덱스를 사용할 명확한 이유가 없습니다. (SpecialOfferID, ProductID) 및 (ProductID)의 인덱스는 비클러스터형 인덱스입니다.  
  
 위에서 일부 bucket_counts의 크기는 과도하게 설정되었지만 SalesOrderHeader_inmem 및 SalesOrderDetail_inmem의 인덱스에 대한 bucket_counts의 크기는 1,000만 개의 판매 주문에 대해서만 설정되었습니다. 이는 사용할 수 있는 메모리가 적은 시스템에 예제를 설치할 수 있도록 하기 위해서입니다. 하지만 이러한 경우에 데모 작업은 메모리 부족으로 실패합니다. 1,000만 개가 훨씬 넘는 판매 주문으로 확장하려는 경우 bucket_counts를 그에 맞게 늘리면 됩니다.  
  
#### <a name="considerations-for-memory-utilization"></a>메모리 사용률에 대한 고려 사항  
 데모 작업을 실행하기 전후에 샘플 데이터베이스의 메모리 사용률은 [메모리 액세스에 최적화된 테이블의 메모리 사용률](#Memoryutilizationforthememory-optimizedtables)섹션에 설명되어 있습니다.  
  
### <a name="stored-procedures-added-by-the-sample"></a>예제에서 추가된 저장 프로시저  
 판매 주문을 삽입하고 배송 정보를 업데이트하기 위한 두 가지 주요 저장 프로시저는 다음과 같습니다.  
  
-   Sales.usp_InsertSalesOrder_inmem  
  
    -   데이터베이스에 새로운 판매 주문을 삽입하고 해당 판매 주문의 SalesOrderID를 출력합니다. 입력 매개 변수로 판매 주문 머리글의 정보뿐만 아니라 주문의 품목을 사용합니다.  
  
    -   출력 매개 변수:  
  
        -   @SalesOrderID int – 방금 삽입된 판매 주문의 SalesOrderID  
  
    -   입력 매개 변수(필수):  
  
        -   @DueDate datetime2  
  
        -   @CustomerID int  
  
        -   @BillToAddressID [int]  
  
        -   @ShipToAddressID [int]  
  
        -   @ShipMethodID [int]  
  
        -   @SalesOrderDetails Sales.SalesOrderDetailType_inmem – 주문의 품목이 포함된 TVP  
  
    -   입력 매개 변수(선택적):  
  
        -   @Status [tinyint]  
  
        -   @OnlineOrderFlag [bit]  
  
        -   @PurchaseOrderNumber [nvarchar](25\)  
  
        -   @AccountNumber [nvarchar](15\)  
  
        -   @SalesPersonID [int]  
  
        -   @TerritoryID [int]  
  
        -   @CreditCardID [int]  
  
        -   @CreditCardApprovalCode [varchar](15\)  
  
        -   @CurrencyRateID [int]  
  
        -   @Comment nvarchar(128)  
  
-   Sales.usp_UpdateSalesOrderShipInfo_inmem  
  
    -   지정된 판매 주문에 대한 배송 정보를 업데이트합니다. 또한 판매 주문의 모든 품목에 대한 배송 정보도 업데이트합니다.  
  
    -   이 저장 프로시저는 동일한 주문을 업데이트하는 동시 트랜잭션과의 예기치 않은 잠재적 충돌을 처리하는 재시도 논리가 포함된 고유하게 컴파일된 저장 프로시저 Sales.usp_UpdateSalesOrderShipInfo_native의 래퍼 프로시저입니다. 재시도 논리에 대한 자세한 내용은 [여기](http://technet.microsoft.com/library/dn169141\(v=sql.120\).aspx)에서 온라인 설명서 항목을 참조하세요.  
  
-   Sales.usp_UpdateSalesOrderShipInfo_native  
  
    -   배송 정보 업데이트를 실제로 처리하는 고유하게 컴파일된 저장 프로시저입니다. 래퍼 저장 프로시저 Sales.usp_UpdateSalesOrderShipInfo_inmem에서 호출되기 위한 수단입니다. 클라이언트가 오류를 처리하고 재시도 논리를 구현할 수 있는 경우 래퍼 저장 프로시저를 사용하지 않고 이 프로시저를 직접 호출할 수 있습니다.  
  
 다음 저장 프로시저는 데모 작업에 사용됩니다.  
  
-   Demo.usp_DemoReset  
  
    -   SalesOrderHeader 및 SalesOrderDetail 테이블을 비우고 초기값을 다시 설정하여 데모를 다시 설정합니다.  
  
 다음 저장 프로시저는 도메인 및 참조 무결성을 보장하면서 메모리 액세스에 최적화된 테이블에서 삽입하고 삭제하는 데 사용됩니다.  
  
-   Production.usp_InsertProduct_inmem  
  
-   Production.usp_DeleteProduct_inmem  
  
-   Sales.usp_InsertSpecialOffer_inmem  
  
-   Sales.usp_DeleteSpecialOffer_inmem  
  
-   Sales.usp_InsertSpecialOfferProduct_inmem  
  
 마지막으로 다음 저장 프로시저는 도메인 및 참조 무결성을 확인하는 데 사용됩니다.  
  
1.  dbo.usp_ValidateIntegrity  
  
    -   선택적 매개 변수: @object_id – 무결성을 확인할 개체의 ID.  
  
    -   이 프로시저는 확인되어야 하는 무결성 규칙에 대해 dbo.DomainIntegrity, dbo.ReferentialIntegrity 및 dbo.UniqueIntegrity 테이블에 의존합니다. 예제에서는 이러한 테이블을 AdventureWorks 데이터베이스의 원래 테이블에 존재하는 CHECK, FOREIGN KEY 및 UNIQUE 제약 조건을 기반으로 채웁니다.  
  
    -   이 프로시저는 도우미 프로시저 dbo.usp_GenerateCKCheck, dbo.usp_GenerateFKCheck 및 dbo.GenerateUQCheck에 의존하여 무결성 검사를 수행하는 데 필요한 T-SQL을 생성합니다.  
  
##  <a name="PerformanceMeasurementsusingtheDemoWorkload"></a> Performance Measurements using the Demo Workload  
 Ostress는 Microsoft CSS SQL Server 지원 팀에서 개발한 명령줄 도구입니다. 이 도구는 쿼리를 실행하거나 저장 프로시저를 병렬로 실행하는 데 사용할 수 있습니다. 지정된 T-SQL 문을 병렬로 실행할 스레드 수를 구성할 수 있으며 해당 스레드에서 문이 실행될 횟수를 지정할 수 있습니다. ostress는 스레드를 시작하고 모든 스레드에서 문을 병렬로 실행합니다. 모든 스레드의 실행이 완료된 후 ostress는 모든 스레드의 실행이 완료되는 데 걸린 시간을 보고합니다.  
  
### <a name="installing-ostress"></a>ostress 설치  
 ostress는 RML 유틸리티의 일부로 설치되며 ostress의 독립 실행형 설치는 없습니다.  
  
 설치 단계:  
  
1.  다음 페이지에서 RML 유틸리티의 x64 설치 패키지를 다운로드하고 실행합니다. [http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx)  
  
2.  특정 파일이 사용 중이라는 대화 상자가 나타나면 'Continue'를 클릭합니다.  
  
### <a name="running-ostress"></a>ostress 실행  
 ostress는 명령줄 프롬프트에서 실행됩니다. RML 유틸리티의 일부로 설치되는 "RML Cmd Prompt"에서 도구를 실행하는 것이 가장 간편합니다.  
  
 RML Cmd Prompt를 열려면 다음 지침을 따르세요.  
  
 Windows Server 2012 [R2]와 Windows 8 및 8.1에서 Windows 키를 클릭하여 시작 메뉴를 열고 'rml'을 입력합니다. 검색 결과의 목록에 있는 “RML Cmd Prompt”를 클릭합니다.  
  
 명령 프롬프트가 RML 유틸리티 설치 폴더에 있는지 확인합니다.  
  
 ostress의 명령줄 옵션은 명령줄 옵션 없이 ostress.exe를 실행하기만 하면 볼 수 있습니다. 이 예제와 함께 ostress를 실행하기 위해 고려할 기본 옵션은 다음과 같습니다.  
  
-   -S 연결할 Microsoft SQL Server 인스턴스 이름  
  
-   -E Windows 인증을 사용하여 연결(기본값). SQL Server 인증을 사용하는 경우 –U 및 –P 옵션을 사용하여 사용자 이름과 암호를 각각 지정합니다.  
  
-   -d 데이터베이스의 이름. 이 예의 경우 AdventureWorks2014입니다.  
  
-   -Q 실행될 T-SQL 문  
  
-   -n 각 입력 파일/쿼리를 처리하는 연결의 수  
  
-   -r 각 연결에서 각 입력 파일/쿼리를 실행할 반복 횟수  
  
### <a name="demo-workload"></a>데모 작업  
 데모 작업에서 사용되는 기본 저장 프로시저는 Sales.usp_InsertSalesOrder_inmem/ondisk입니다. 아래의 스크립트는 예제 데이터로 TVP(테이블 반환 매개 변수)를 생성하고 프로시저를 호출하여 품목이 5개인 판매 주문을 삽입합니다.  
  
 ostress 도구는 저장 프로시저 호출을 병렬로 실행하여 판매 주문을 동시에 삽입하는 클라이언트를 시뮬레이트하는 데 사용됩니다.  
  
 ostress 실행이 끝날 때마다 Demo.usp_DemoReset을 실행하여 데모를 다시 설정합니다. 이 프로시저는 메모리 액세스에 최적화된 테이블의 행을 삭제하고, 디스크 기반 테이블을 자르며, 데이터베이스 검사점을 실행합니다.  
  
 다음 스크립트는 판매 주문 처리 작업을 시뮬레이트하기 위해 동시에 실행됩니다.  
  
```  
DECLARE   
      @i int = 0,   
      @od Sales.SalesOrderDetailType_inmem,   
      @SalesOrderID int,   
      @DueDate datetime2 = sysdatetime(),   
      @CustomerID int = rand() * 8000,   
      @BillToAddressID int = rand() * 10000,   
      @ShipToAddressID int = rand() * 10000,   
      @ShipMethodID int = (rand() * 5) + 1;   
  
INSERT INTO @od   
SELECT OrderQty, ProductID, SpecialOfferID   
FROM Demo.DemoSalesOrderDetailSeed   
WHERE OrderID= cast((rand()*106) + 1 as int);   
  
WHILE (@i < 20)   
BEGIN;   
      EXEC Sales.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od;   
      SET @i += 1   
END  
  
```  
  
 이 스크립트를 사용하면 생성된 각 예제 주문이 WHILE 루프에서 실행되는 20개의 저장 프로시저를 통해 20회 삽입됩니다. 루프는 데이터베이스가 예제 주문을 생성하는 데 사용된다는 사실을 보완하는 데 사용됩니다. 일반적인 프로덕션 환경에서는 중간 계층 응용 프로그램이 삽입될 판매 주문을 생성합니다.  
  
 위의 스크립트는 판매 주문을 메모리 액세스에 최적화된 테이블에 삽입합니다. 판매 주문을 디스크 기반 테이블에 삽입하는 스크립트는 두 ‘_inmem’을 ‘_ondisk’로 바꿔서 파생됩니다.  
  
 ostress 도구를 사용하여 여러 동시 연결을 통해 스크립트를 실행할 것입니다. ‘-n’ 매개 변수를 사용하여 연결 수를 제어하고 ‘r’ 매개 변수를 사용하여 스크립트가 각 연결에서 실행되는 횟수를 제어하려고 합니다.  
  
#### <a name="running-the-workload"></a>작업 실행  
 최대 규모로 테스트하기 위해 100개의 연결을 사용하여 1,000만 개의 판매 주문을 삽입합니다. 이 테스트는 일반 서버(예: 물리적 코어 8개, 논리적 코어 16개)와 로그용 기본 SSD 저장소에서 문제 없이 실행됩니다. 테스트가 사용자의 하드웨어에서 제대로 실행되지 않는 경우 [느리게 실행되는 테스트 문제 해결](#Troubleshootingslow-runningtests)섹션을 참조하세요. 이 테스트에 대한 스트레스 수준을 줄이려면 '-n' 매개 변수를 변경하여 연결 수를 줄입니다. 예를 들어 연결 수를 40으로 줄이려면 ‘-n100’ 매개 변수를 ‘-n40’으로 변경합니다.  
  
 작업에 대한 성능 측정으로 작업을 실행한 후 ostress.exe에서 보고하는 경과 시간을 사용합니다.  
  
 아래 지침과 측정값에서는 1000만 개의 판매 주문을 삽입하는 작업을 사용합니다. 100만 개의 판매 주문을 삽입하는 축소된 워크로드를 실행하는 지침은 SQLServer2016CTP3Samples.zip 보관 파일의 일부인 'In-Memory OLTP\readme.txt'에 있는 지침을 참조하세요.  
  
##### <a name="memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블  
 메모리 액세스에 최적화된 테이블에서 작업을 실행하는 것부터 시작합니다. 다음 명령은 각각 5,000회의 반복을 위해 실행되는 100개의 스레드를 엽니다.  각 반복에서는 별도의 트랜잭션에서 20개의 판매 주문을 삽입합니다. 데이터베이스가 삽입될 데이터를 생성하는 데 사용된다는 사실을 보완하기 위해 반복당 20개의 삽입이 있습니다. 이에 따라 총 20 * 5,000 \* 100 = 10,000,000개의 판매 주문 삽입이 생성됩니다.  
  
 RML Cmd Prompt를 열고 다음 명령을 실행합니다.  
  
 복사 단추를 클릭하여 명령을 복사하고 RML 유틸리티 명령 프롬프트에 붙여 넣습니다.  
  
```  
ostress.exe –n100 –r5000 -S. -E -dAdventureWorks2016CTP3 -q -Q"DECLARE @i int = 0, @od Sales.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand() * 10000, @ShipMethodID int = (rand() * 5) + 1; INSERT INTO @od SELECT OrderQty, ProductID, SpecialOfferID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*106) + 1 as int); while (@i < 20) begin; EXEC Sales.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od; set @i += 1 end"  
```  
  
 물리적 코어가 총 8개(논리적 코어 총 16개)인 테스트 서버에서 이 작업은 2분 5초가 소요되었고, 물리적 코어가 24개(논리적 코어 48개)인 두 번째 테스트 서버에서는 1분 0초가 소요되었습니다.  
  
 작업 관리자 등을 사용하여 작업이 실행되는 동안 CPU 사용률을 관찰합니다. CPU 사용률이 100%에 가깝게 나타나는 것을 확인할 수 있습니다. 그렇지 않은 경우에는 로그 IO 병목 상태가 발생한 것입니다. [느리게 실행되는 테스트 문제 해결](#Troubleshootingslow-runningtests)을 참조하세요.  
  
##### <a name="disk-based-tables"></a>디스크 기반 테이블  
 다음 명령은 디스크 기반 테이블에서 작업을 실행합니다. 이 작업은 실행되는 데 시간이 걸릴 수 있는데 그 이유는 대부분 시스템의 래치 경합 때문입니다. 메모리 액세스에 최적화된 테이블은 래치를 사용하지 않으므로 이 문제의 영향을 받지 않습니다.  
  
 RML Cmd Prompt를 열고 다음 명령을 실행합니다.  
  
 복사 단추를 클릭하여 명령을 복사하고 RML 유틸리티 명령 프롬프트에 붙여 넣습니다.  
  
```  
ostress.exe –n100 –r5000 -S. -E -dAdventureWorks2016CTP3 -q -Q"DECLARE @i int = 0, @od Sales.SalesOrderDetailType_ondisk, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand() * 10000, @ShipMethodID int = (rand() * 5) + 1; INSERT INTO @od SELECT OrderQty, ProductID, SpecialOfferID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*106) + 1 as int); while (@i < 20) begin; EXEC Sales.usp_InsertSalesOrder_ondisk @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od; set @i += 1 end"  
```  
  
 물리적 코어가 총 8개(논리적 코어 총 16개)인 테스트 서버에서 이 작업은 41분 25초가 소요되었고, 물리적 코어가 24개(논리적 코어 48개)인 두 번째 테스트 서버에서는 52분 16초가 소요되었습니다.  
  
 이 테스트에서 메모리 액세스에 최적화된 테이블과 디스크 기반 테이블 간 성능 차이의 주요 요인은 디스크 기반 테이블을 사용하는 경우 SQL Server에서 CPU를 완전히 활용할 수 없다는 사실입니다. 그 이유는 래치 경합 때문입니다. 즉, 동시 트랜잭션이 동일한 데이터 페이지에 쓰려고 합니다. 래치는 한 번에 한 트랜잭션만 페이지에 쓸 수 있도록 하는 데 사용됩니다. 메모리 내 OLTP 엔진은 래치를 사용하지 않으며 데이터 행이 페이지에 구성되지 않습니다. 따라서 동시 트랜잭션이 서로의 삽입을 차단하지 않기 때문에 SQL Server에서 CPU를 완전히 활용할 수 있습니다.  
  
 작업 관리자 등을 사용하여 작업이 실행되는 동안 CPU 사용률을 관찰할 수 있습니다. 디스크 기반 테이블을 사용하는 경우 CPU 사용률이 100%에 크게 못 미치는 것을 확인할 수 있습니다. 논리적 프로세서가 16개인 테스트 구성에서 사용률은 24% 정도입니다.  
  
 필요에 따라 성능 모니터를 사용하여 성능 카운터 ‘\SQL Server:Latches\Latch Waits/sec’를 통해 초당 래치 대기 수를 볼 수 있습니다.  
  
#### <a name="resetting-the-demo"></a>데모 다시 설정  
 데모를 다시 설정하려면 RML Cmd Prompt를 열고 다음 명령을 실행합니다.  
  
```  
ostress.exe -S. -E -dAdventureWorks2016CTP3 -Q"EXEC Demo.usp_DemoReset"  
```  
  
 하드웨어에 따라 이 명령이 실행되는 데 몇 분 정도 걸릴 수 있습니다.  
  
 데모 실행이 끝날 때마다 다시 설정하는 것이 좋습니다. 이 작업이 삽입만 수행하기 때문에 각 실행에서 더 많은 메모리가 사용되므로 메모리 부족을 방지하려면 다시 설정해야 합니다. 실행 후 사용되는 메모리 양은 [작업 실행 후 메모리 사용률](#Memoryutilizationafterrunningtheworkload)섹션에 설명되어 있습니다.  
  
###  <a name="Troubleshootingslow-runningtests"></a> Troubleshooting slow-running tests  
 테스트 결과는 일반적으로 하드웨어와 테스트 실행에서 사용되는 동시성 수준에 따라 달라집니다. 결과가 예상과 다른 경우 확인할 몇 가지 사항은 다음과 같습니다.  
  
-   동시 트랜잭션 수: 단일 스레드에서 작업을 실행할 때 메모리 내 OLTP를 사용한 성능 이점은 두 배보다 적을 수 있습니다. 래치 경합은 동시성 수준이 높은 경우에만 큰 문제가 됩니다.  
  
-   SQL Server에서 사용할 수 있는 적은 코어 수: 즉, 동시에 실행되는 트랜잭션이 SQL에서 사용할 수 있는 코어 수만큼만 있을 수 있으므로 시스템에서 동시성 수준이 낮습니다.  
  
    -   증상: 디스크 기반 테이블에서 작업을 실행할 때 CPU 사용률이 높은 경우 경합이 많다는 의미이며 동시성 부족을 나타냅니다.  
  
-   로그 드라이브의 속도: 로그 드라이브가 시스템의 트랜잭션 처리량 수준을 유지할 수 없는 경우 작업이 로그 IO에서 병목 상태가 됩니다. 메모리 내 OLTP를 사용하는 경우 로깅이 보다 효율적이지만 로그 IO가 병목 상태인 경우 잠재적인 성능 이점이 제한됩니다.  
  
    -   증상: 메모리 액세스에 최적화된 테이블에서 작업을 실행할 때 CPU 사용률이 100%에 가깝지 않거나 변동이 심한 경우 로그 IO 병목 상태가 있을 수 있습니다. 이는 리소스 모니터를 열고 로그 드라이브의 큐 길이를 살펴보고 확인할 수 있습니다.  
  
##  <a name="MemoryandDiskSpaceUtilizationintheSample"></a> 샘플의 메모리 및 디스크 공간 사용률  
 아래에서는 예제 데이터베이스의 메모리 및 디스크 공간 사용률 측면에서 기대하는 것에 대해 설명합니다. 또한 논리적 코어가 16개인 테스트 서버에서 관찰한 결과도 보여 줍니다.  
  
###  <a name="Memoryutilizationforthememory-optimizedtables"></a> Memory utilization for the memory-optimized tables  
  
#### <a name="overall-utilization-of-the-database"></a>데이터베이스의 전체 사용률  
 다음 쿼리를 사용하여 시스템에서 메모리 내 OLTP의 총 메모리 사용률을 얻을 수 있습니다.  
  
```  
SELECT type  
   , name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
 데이터베이스를 만든 후의 스냅숏:  
  
||||  
|-|-|-|  
|**type**|**name**|**pages_MB**|  
|MEMORYCLERK_XTP|기본값|94|  
|MEMORYCLERK_XTP|DB_ID_5|877|  
|MEMORYCLERK_XTP|기본값|0|  
|MEMORYCLERK_XTP|기본값|0|  
  
 기본 메모리 클럭은 시스템 차원의 메모리 구조를 포함하고 있으며 비교적 작습니다. 사용자 데이터베이스(이 경우 ID 5인 데이터베이스)의 메모리 클럭은 약 900MB입니다.  
  
#### <a name="memory-utilization-per-table"></a>테이블당 메모리 사용률  
 다음 쿼리를 사용하여 개별 테이블과 인덱스의 메모리 사용률을 세부적으로 확인할 수 있습니다.  
  
```  
SELECT object_name(t.object_id) AS [Table Name]  
     , memory_allocated_for_table_kb  
 , memory_allocated_for_indexes_kb  
FROM sys.dm_db_xtp_table_memory_stats dms JOIN sys.tables t   
ON dms.object_id=t.object_id  
WHERE t.type='U'  
```  
  
 예제를 처음 설치한 경우 이 쿼리의 결과는 다음과 같습니다.  
  
||||  
|-|-|-|  
|**테이블 이름**|**memory_allocated_for_table_kb**|**memory_allocated_for_indexes_kb**|  
|SpecialOfferProduct_inmem|64|3840|  
|DemoSalesOrderHeaderSeed|1984|5504|  
|SalesOrderDetail_inmem|15316|663552|  
|DemoSalesOrderDetailSeed|64|10432|  
|SpecialOffer_inmem|3|8192|  
|SalesOrderHeader_inmem|7168|147456|  
|Product_inmem|124|12352|  
  
 보시다시피 테이블은 상당히 작습니다. SalesOrderHeader_inmem은 약 7MB이고, SalesOrderDetail_inmem은 약 15MB입니다.  
  
 여기에서 눈에 띄는 것은 테이블 데이터의 크기와 비교할 때 인덱스에 할당된 메모리의 크기입니다. 이는 예제에서 해시 인덱스의 크기가 더 큰 데이터 크기에 대해 설정되었기 때문입니다. 해시 인덱스의 크기는 고정되어 있으므로 테이블의 데이터 크기에 따라 커지지 않습니다.  
  
####  <a name="Memoryutilizationafterrunningtheworkload"></a> Memory utilization after running the workload  
 1,000만 개의 판매 주문을 삽입한 후 총 메모리 사용률은 다음과 유사합니다.  
  
```  
SELECT type  
, name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
||||  
|-|-|-|  
|**type**|**name**|**pages_MB**|  
|MEMORYCLERK_XTP|기본값|146|  
|MEMORYCLERK_XTP|DB_ID_5|7374|  
|MEMORYCLERK_XTP|기본값|0|  
|MEMORYCLERK_XTP|기본값|0|  
  
 보시다시피 SQL Server는 샘플 데이터베이스에서 메모리 액세스에 최적화된 테이블과 인덱스에 8GB보다 조금 작은 크기를 사용하고 있습니다.  
  
 예제를 한 번 실행한 후 테이블당 자세한 메모리 사용률을 살펴보면 다음과 같습니다.  
  
```  
SELECT object_name(t.object_id) AS [Table Name]  
     , memory_allocated_for_table_kb  
 , memory_allocated_for_indexes_kb  
FROM sys.dm_db_xtp_table_memory_stats dms JOIN sys.tables t   
ON dms.object_id=t.object_id  
WHERE t.type='U'  
```  
  
||||  
|-|-|-|  
|**테이블 이름**|**memory_allocated_for_table_kb**|**memory_allocated_for_indexes_kb**|  
|SalesOrderDetail_inmem|5113761|663552|  
|DemoSalesOrderDetailSeed|64|10368|  
|SpecialOffer_inmem|2|8192|  
|SalesOrderHeader_inmem|1575679|147456|  
|Product_inmem|111|12032|  
|SpecialOfferProduct_inmem|64|3712|  
|DemoSalesOrderHeaderSeed|1984|5504|  
  
 총 6.5GB 정도의 데이터를 확인할 수 있습니다. SalesOrderHeader_inmem 및 SalesOrderDetail_inmem 테이블의 인덱스 크기는 판매 주문을 삽입하기 전의 인덱스 크기와 동일합니다. 인덱스 크기는 두 테이블 모두 해시 인덱스를 사용하고 해시 인덱스가 고정되어 있기 때문에 변경되지 않았습니다.  
  
#### <a name="after-demo-reset"></a>데모를 다시 설정한 후  
 저장 프로시저 Demo.usp_DemoReset을 사용하여 데모를 다시 설정할 수 있습니다. 이 프로시저는 SalesOrderHeader_inmem 및 SalesOrderDetail_inmem 테이블의 데이터를 삭제하고 원래 테이블 SalesOrderHeader 및 SalesOrderDetail의 데이터로 초기값을 다시 설정합니다.  
  
 테이블의 행이 삭제되었더라도 메모리가 즉시 회수되지는 않습니다. SQL Server는 필요에 따라 백그라운드에서 메모리 액세스에 최적화된 테이블의 삭제된 행에서 메모리를 회수합니다. 데모가 다시 설정된 직후에는 시스템에 트랜잭션 작업이 없으므로 삭제된 행의 메모리가 아직 회수되지 않은 것을 확인할 수 있습니다.  
  
```  
SELECT type  
, name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
||||  
|-|-|-|  
|**type**|**name**|**pages_MB**|  
|MEMORYCLERK_XTP|기본값|2261|  
|MEMORYCLERK_XTP|DB_ID_5|7396|  
|MEMORYCLERK_XTP|기본값|0|  
|MEMORYCLERK_XTP|기본값|0|  
  
 이는 예상된 결과입니다. 트랜잭션 작업이 실행 중일 때 메모리가 회수됩니다.  
  
 데모 작업의 두 번째 실행을 시작하는 경우 이전에 삭제된 행이 정리됨에 따라 메모리 사용률이 처음에는 줄어드는 것을 확인할 수 있습니다. 특정 시점에서 메모리 크기가 다시 증가하고 작업이 완료될 때까지 증가합니다. 데모를 다시 설정하고 1,000만 개의 행을 삽입한 후 메모리 사용률은 처음 실행한 후의 사용률과 매우 유사합니다. 예를 들어  
  
```  
SELECT type  
, name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
||||  
|-|-|-|  
|**type**|**name**|**pages_MB**|  
|MEMORYCLERK_XTP|기본값|1863|  
|MEMORYCLERK_XTP|DB_ID_5|7390|  
|MEMORYCLERK_XTP|기본값|0|  
|MEMORYCLERK_XTP|기본값|0|  
  
### <a name="disk-utilization-for-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블의 디스크 사용률  
 지정된 시점에서 데이터베이스의 검사점 파일에 대한 전체 디스크 크기는 다음 쿼리를 사용하여 확인할 수 있습니다.  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
  
```  
  
#### <a name="initial-state"></a>초기 상태  
 예제 파일 그룹과 예제 메모리 액세스에 최적화된 테이블이 처음에 만들어질 때 많은 검사점 파일이 미리 만들어지고 시스템이 이러한 파일을 채우기 시작합니다. 미리 만들어지는 검사점 파일의 수는 시스템의 논리적 프로세서 수에 따라 달라집니다. 예제는 처음에는 매우 작으므로 미리 만들어진 파일은 처음 만들어진 후 거의 비어 있습니다.  
  
 논리적 프로세서가 16개인 컴퓨터에서 예제의 초기 디스크 크기는 다음과 같습니다.  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
```  
  
||  
|-|  
|**On-disk size in MB**|  
|2312|  
  
 보시다시피 검사점 파일의 디스크 크기(2.3GB)와 실제 데이터 크기(30MB에 가까움)에는 큰 차이가 있습니다.  
  
 디스크 공간 사용의 출처를 자세히 살펴보려면 다음 쿼리를 사용할 수 있습니다. 이 쿼리에서 반환되는 디스크 크기는 상태가 5(REQUIRED FOR BACKUP/HA), 6(IN TRANSITION TO TOMBSTONE) 또는 7(TOMBSTONE)인 파일에 대해 대략적인 값입니다.  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
 예제의 초기 상태에 대한 결과는 논리적 프로세서가 16개인 서버의 경우와 유사합니다.  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**count**|**on-disk size MB**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|UNDER CONSTRUCTION|DATA|1|128|  
|UNDER CONSTRUCTION|DELTA|1|8|  
  
 보시다시피 대부분의 공간이 미리 만들어진 데이터 및 델타 파일에서 사용됩니다. SQL Server는 논리적 프로세서당 하나의 (데이터, 델타) 파일 쌍을 미리 만들었습니다. 또한 데이터 파일의 크기는 128MB로, 델타 파일의 크기는 8MB로 미리 지정되므로 이러한 파일에 더욱 효율적으로 데이터를 삽입할 수 있습니다.  
  
 메모리 액세스에 최적화된 테이블의 실제 데이터는 단일 데이터 파일에 있습니다.  
  
#### <a name="after-running-the-workload"></a>작업을 실행한 후  
 1,000만 개의 판매 주문을 삽입하는 단일 테스트 실행 후 전체 디스크 크기는 다음과 같습니다(16코어 테스트 서버의 경우).  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
```  
  
||  
|-|  
|**On-disk size in MB**|  
|8828|  
  
 디스크 크기는 데이터의 메모리 내 크기와 유사하게 9GB에 가깝습니다.  
  
 다양한 상태에 있는 검사점 파일의 크기를 좀더 자세히 살펴보면 다음과 같습니다.  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**count**|**on-disk size MB**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|UNDER CONSTRUCTION|DATA|1|128|  
|UNDER CONSTRUCTION|DELTA|1|8|  
  
 검사점이 닫힐 때 사용할 준비가 된 미리 만들어진 파일 쌍이 16개 있습니다.  
  
 현재 검사점이 닫힐 때까지 사용되는, 작성 중인 쌍이 하나 있습니다. 활성 검사점 파일과 함께 메모리의 6.5GB 데이터에 대한 약 6.5GB의 디스크를 사용합니다. 인덱스가 디스크에 유지되지 않으므로 이 경우 디스크의 전체 크기는 메모리의 크기보다 작습니다.  
  
#### <a name="after-demo-reset"></a>데모를 다시 설정한 후  
 데모를 다시 설정한 후에는 데이터베이스 검사점이 없고 시스템에 트랜잭션 작업이 없는 경우 디스크 공간이 즉시 회수되지 않습니다. 검사점 파일이 다양한 상태를 이동하여 결국 삭제되려면 검사점 파일의 병합을 시작하고 가비지 수집을 시작하기 위해 많은 검사점 및 로그 잘림 이벤트가 발생해야 합니다. 이러한 이벤트는 시스템에 트랜잭션 작업이 있으면(전체 복구 모델을 사용하는 경우에는 정기 로그 백업을 수행하면) 자동으로 발생하지만, 데모 시나리오와 같이 시스템이 유휴 상태일 때는 발생하지 않습니다.  
  
 예제에서는 데모를 다시 설정한 후 다음과 유사하게 나타날 수 있습니다.  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
```  
  
||  
|-|  
|**On-disk size in MB**|  
|11839|  
  
 거의 12GB로, 데모를 다시 설정하기 전의 9GB보다 훨씬 큽니다. 이는 다음에서 확인할 수 있듯이 일부 검사점 파일 병합이 시작되었지만 일부 병합 대상이 아직 설치되지 않았으며 일부 병합 원본 파일이 아직 정리되지 않았기 때문입니다.  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**count**|**on-disk size MB**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|ACTIVE|DATA|38|5152|  
|ACTIVE|DELTA|38|1331|  
|MERGE TARGET|DATA|7|896|  
|MERGE TARGET|DELTA|7|56|  
|MERGED SOURCE|DATA|13|1772|  
|MERGED SOURCE|DELTA|13|455|  
  
 트랜잭션 작업이 시스템에서 발생하면 병합 대상이 설치되고 병합된 원본이 정리됩니다.  
  
 데모를 다시 설정한 후 1,000만 개의 판매 주문을 삽입하는 데모 작업을 두 번째로 실행하면 작업을 처음 실행하는 동안 생성된 파일이 정리된 것을 확인할 수 있습니다. 작업이 실행되는 동안 위의 쿼리를 몇 차례 실행하는 경우 검사점 파일이 다양한 상태를 거치는 것을 확인할 수 있습니다.  
  
 1,000만 개의 판매 주문을 삽입하는 작업을 두 번째로 실행한 후 디스크 사용률이 처음 실행한 후와 매우 유사한 것을 확인할 수 있습니다. 하지만 시스템이 특성상 동적이므로 반드시 같지는 않습니다. 예를 들어  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**count**|**on-disk size MB**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|UNDER CONSTRUCTION|DATA|2|268|  
|UNDER CONSTRUCTION|DELTA|2|16|  
|ACTIVE|DATA|41|5608|  
|ACTIVE|DELTA|41|328|  
  
 이 경우에는 'under construction' 상태의 검사점 파일 쌍이 두 개 있습니다. 즉, 작업의 높은 동시성 수준 때문에 여러 파일 쌍이 ‘under construction’ 상태로 이동했습니다. 여러 동시 스레드에서 같은 시간에 새로운 파일 쌍을 필요로 했으므로 파일 쌍이 'precreated'에서 ‘under construction’으로 이동했습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  


