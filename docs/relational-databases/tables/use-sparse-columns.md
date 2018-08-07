---
title: 스파스 열 사용 | Microsoft 문서
ms.custom: ''
ms.date: 03/22/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- sparse columns, described
- null columns
- sparse columns
ms.assetid: ea7ddb87-f50b-46b6-9f5a-acab222a2ede
caps.latest.revision: 47
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 6efb69c0043bc5ffb57caa09253d93724c51e146
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39540873"
---
# <a name="use-sparse-columns"></a>스파스 열 사용
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  스파스 열은 Null 값에 대해 최적화된 저장소가 있는 일반 열입니다. 스파스 열을 사용하면 Null 값에 대한 공간 요구 사항이 줄어드는 반면 Null이 아닌 값을 검색하는 데 더 많은 오버헤드가 발생합니다. 최소 20%에서 40% 사이의 공간이 절약되는 경우에는 스파스 열을 사용하십시오. 스파스 열 및 열 집합은 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) 또는 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 문을 사용하여 정의합니다.  
  
 스파스 열은 열 집합 및 필터링된 인덱스와 함께 사용할 수 있습니다.  
  
-   열 집합  
  
     INSERT, UPDATE 및 DELETE 문은 이름별로 스파스 열을 참조할 수 있습니다. 그러나 단일 XML 열에 결합된 테이블의 모든 스파스 열을 보고 사용할 수도 있습니다. 이러한 열을 열 집합이라고 합니다. 열 집합에 대한 자세한 내용은 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)을 참조하세요.  
  
-   필터링된 인덱스  
  
     스파스 열은 Null 값 행을 많이 포함하므로 필터링된 인덱스에 특히 적합합니다. 스파스 열에 대한 필터링된 인덱스는 채워진 값을 포함하는 행만 인덱싱할 수 있습니다. 따라서 보다 작고 효율적인 인덱스가 만들어집니다. 자세한 내용은 [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)을(를) 참조하세요.  
  
 스파스 열 및 필터링된 인덱스를 통해 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]와 같은 응용 프로그램에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]을 사용하여 많은 수의 사용자 정의 속성을 효율적으로 저장하고 액세스할 수 있습니다.  
  
## <a name="properties-of-sparse-columns"></a>스파스 열 속성  
 스파스 열에는 다음과 같은 특징이 있습니다.  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 은 열 정의에 SPARSE 키워드를 사용하여 해당 열의 값 저장을 최적화할 수 있습니다. 따라서 테이블에 있는 행에 대해 열 값이 NULL인 경우 값을 저장할 필요가 없습니다.  
  
-   스파스 열을 포함하는 테이블에 대한 카탈로그 뷰는 일반적인 테이블에 대한 카탈로그 뷰와 동일합니다. sys.columns 카탈로그 뷰는 테이블의 각 열에 대한 행을 포함하고 열 집합(정의된 경우)을 포함합니다.  
  
-   스파스 열은 논리적 테이블이 아닌 저장소 계층의 속성입니다. 따라서 SELECT…INTO 문은 스파스 열 속성을 새 테이블에 복사하지 않습니다.  
  
-   COLUMNS_UPDATED 함수는 **varbinary** 값을 반환하여 DML 동작을 수행하는 동안 업데이트된 모든 열을 나타냅니다. COLUMNS_UPDATED 함수에 의해 반환된 비트는 다음과 같습니다.  
  
    -   스파스 열이 명시적으로 업데이트되면 해당 스파스 열에 대한 비트가 1로 설정되고 열 집합에 대한 비트가 1로 설정됩니다.  
  
    -   열 집합이 명시적으로 업데이트되면 열 집합에 대한 비트가 1로 설정되고 해당 테이블의 모든 스파스 열에 대한 비트가 1로 설정됩니다.  
  
    -   삽입 작업의 경우 모든 비트가 1로 설정됩니다.  
  
     열 집합에 대한 자세한 내용은 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)을 참조하세요.  
  
 다음 데이터 형식은 SPARSE로 지정할 수 없습니다.  
  
|||  
|-|-|  
|**geography**|**text**|  
|**geometry**|**timestamp**|  
|**image**|**사용자 정의 데이터 형식**|  
|**ntext**||  
  
## <a name="estimated-space-savings-by-data-type"></a>데이터 형식별 예상 공간 절약  
 스파스 열을 사용하면 SPARSE로 표시되지 않은 동일한 데이터에 대해 필요한 공간보다 Null이 아닌 값에 더 많은 저장 공간이 필요합니다. 다음 표에서는 각 데이터 형식에 대한 공간 사용률을 보여 줍니다. **NULL 백분율** 열은 40%의 순 공간 절약을 위해 NULL이어야 하는 데이터 비율을 나타냅니다.  
  
 **고정 길이 데이터 형식**  
  
|데이터 형식|비-스파스 바이트|스파스 바이트|NULL 백분율|  
|---------------|---------------------|------------------|---------------------|  
|**bit**|0.125|5|98%|  
|**tinyint**|@shouldalert|5|86%|  
|**smallint**|2|6|76%|  
|**int**|4|8|64%|  
|**bigint**|8|12|52%|  
|**real**|4|8|64%|  
|**float**|8|12|52%|  
|**smallmoney**|4|8|64%|  
|**money**|8|12|52%|  
|**smalldatetime**|4|8|64%|  
|**datetime**|8|12|52%|  
|**uniqueidentifier**|16|20|43%|  
|**date**|3|7|69%|  
  
 **전체 자릿수 종속 길이 데이터 형식**  
  
|데이터 형식|비-스파스 바이트|스파스 바이트|NULL 백분율|  
|---------------|---------------------|------------------|---------------------|  
|**datetime2(0)**|6|10|57%|  
|**datetime2(7)**|8|12|52%|  
|**time(0)**|3|7|69%|  
|**time(7)**|5|9|60%|  
|**datetimetoffset(0)**|8|12|52%|  
|**datetimetoffset(7)**|10|14|49%|  
|**decimal/numeric(1,s)**|5|9|60%|  
|**decimal/numeric(38,s)**|17|21|42%|  
|**vardecimal(p,s)**|**decimal** 형식을 일반적인 예상치로 사용|||  
  
 **데이터 종속 길이 데이터 형식**  
  
|데이터 형식|비-스파스 바이트|스파스 바이트|NULL 백분율|  
|---------------|---------------------|------------------|---------------------|  
|**sql_variant**|기본 데이터 형식에 따라 다름|||  
|**varchar** 또는 **char**|2*|4*|60%|  
|**nvarchar** 또는 **char**|2*|4*+|60%|  
|**varbinary** 또는 **binary**|2*|4*|60%|  
|**xml**|2*|4*|60%|  
|**hierarchyid**|2*|4*|60%|  
  
 *길이는 형식에 포함된 데이터의 평균에 2바이트 또는 4바이트를 더한 값과 같습니다.  
  
## <a name="in-memory-overhead-required-for-updates-to-sparse-columns"></a>스파스 열을 업데이트하려면 메모리 내 오버헤드가 필요함  
 스파스 열을 사용하여 테이블을 디자인하는 경우 행이 업데이트될 때 테이블에서 null이 아닌 스파스 열 각각에 대해 2바이트의 추가 오버헤드가 필요함에 유의해야 합니다. 이러한 추가 메모리 요구 사항으로 인해 이 메모리 오버헤드를 포함한 총 행 크기가 8019를 초과하여 열을 행에 밀어넣을 수 없으므로 예기치 않게 576 오류가 발생하여 업데이트가 실패할 수 있습니다.  
  
 bigint 형식의 600개 스파스 열을 가진 테이블의 예를 살펴 보십시오. 571개의 null이 아닌 열이 있는 경우 디스크의 총 크기는 571 * 12 = 6852바이트입니다. 추가 행 오버로드와 스파스 열 머리글을 포함하면 약 6895바이트로 증가합니다. 페이지에는 여전히 디스크에서 사용 가능한 1124바이트가 있습니다. 그러면 추가 열을 업데이트할 수 있는 것처럼 보일 수 있습니다. 하지만 업데이트 중에 메모리에 2\*(null이 아닌 스파스 열의 수)에 해당하는 추가 오버헤드가 발생합니다. 이 예에서 추가 오버헤드(2 \* 571 = 1142바이트)를 포함하면 디스크의 행 크기가 약 8037바이트로 증가합니다. 이는 최대 허용 크기인 8019바이트를 초과합니다. 모든 열은 고정 길이 데이터 형식이므로 행에 밀어넣을 수 없습니다. 따라서 576 오류가 발생하여 업데이트가 실패합니다.  
  
## <a name="restrictions-for-using-sparse-columns"></a>스파스 열 사용에 대한 제한 사항  
 스파스 열은 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 사용할 수 있으며 다른 모든 열처럼 작동하지만 다음과 같은 제한 사항의 적용을 받습니다.  
  
-   스파스 열은 Null을 허용해야 하며 ROWGUIDCOL 또는 IDENTITY 속성을 사용할 수 없습니다. 스파스 열의 데이터 형식은 **text**, **ntext**, **image**, **timestamp**, 사용자 정의 데이터 형식, **geometry**또는 **geography**일 수 없으며, 스파스 열에 FILESTREAM 특성을 가질 수 없습니다.  
  
-   스파스 열은 기본값을 사용할 수 없습니다.  
  
-   스파스 열은 규칙에 바인딩할 수 없습니다.  
  
-   계산 열은 스파스 열을 포함할 수 있지만 이런 경우에도 계산 열을 SPARSE로 표시할 수 없습니다.  
  
-   스파스 열에 대해 데이터 마스크를 정의할 수 있지만 열 집합의 일부인 스파스 열에는 정의할 수 없습니다.  
  
-   스파스 열은 클러스터형 인덱스 또는 고유 기본 키 인덱스의 일부가 될 수 없습니다. 그러나 스파스 열에 정의된 지속형 계산 열과 비지속형 계산 열 모두 클러스터형 키의 일부가 될 수 있습니다.  
  
-   스파스 열은 클러스터형 인덱스 또는 힙의 파티션 키로 사용될 수 없습니다. 그러나 스파스 열은 비클러스터형 인덱스의 파티션 키로 사용될 수 있습니다.  
  
-   스파스 열은 테이블 변수 및 테이블 반환 매개 변수에 사용되는 사용자 정의 테이블 형식의 일부가 될 수 없습니다.  
  
-   스파스 열은 데이터 압축과 호환되지 않습니다. 따라서 스파스 열을 압축된 테이블에 추가할 수 없을 뿐만 아니라 스파스 열을 포함하는 테이블을 압축할 수도 없습니다.  
  
-   스파스 열에서 스파스가 아닌 열로 또는 스파스가 아닌 열에서 스파스 열로 열을 변경하려면 열의 저장소 형식을 변경해야 합니다. SQL Server 데이터베이스 엔진에서는 다음 절차를 통해 이러한 변경을 수행합니다.  
  
    1.  새 저장소 크기 및 형식으로 테이블에 새 열을 추가합니다.  
  
    2.  테이블의 각 행에 대해 기존 열에 저장된 값을 업데이트하고 새 열로 복사합니다.  
  
    3.  기존 열을 테이블 스키마에서 제거합니다.  
  
    4.  테이블을 다시 작성하거나(클러스터형 인덱스가 없는 경우) 클러스터형 인덱스를 다시 작성하여 이전 열에 사용된 공간을 회수합니다.  
  
    > [!NOTE]  
    >  행에 허용된 최대 행 크기를 초과하는 데이터가 있으면 2단계가 실패합니다. 이 데이터 크기에는 기존 열에 저장된 데이터 및 업데이트되어 새 열에 저장된 데이터의 크기가 포함됩니다. 스파스 열이 포함되지 않은 테이블의 경우 8060바이트, 스파스 열이 포함된 테이블의 경우 8018바이트로 제한됩니다. 데이터 크기로 인한 이 오류는 적합한 열을 행 외부로 밀어낸 경우에도 발생합니다.  
  
-   스파스가 아닌 열을 스파스 열로 변경하면 스파스 열이 Null이 아닌 값에 대해 더 많은 공간을 사용합니다. 행이 최대 행 크기 제한에 가까우면 작업이 실패할 수 있습니다.  
  
## <a name="sql-server-technologies-that-support-sparse-columns"></a>스파스 열을 지원하는 SQL Server 기술  
 이 섹션에서는 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술에서 스파스 열을 지원하는 방법에 대해 설명합니다.  
  
-   트랜잭션 복제  
  
     트랜잭션 복제는 스파스 열을 지원하지만 스파스 열에서 사용할 수 있는 열 집합은 지원하지 않습니다. 열 집합에 대한 자세한 내용은 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)을 참조하세요.  
  
     SPARSE 특성 복제는 [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 을 사용하거나 **에서** 아티클 속성 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]대화 상자를 사용하여 지정되는 스키마 옵션에 의해 결정됩니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 스파스 열이 지원되지 않습니다. 데이터를 이전 버전으로 복제해야 하는 경우 SPARSE 특성을 복제하지 않도록 지정합니다.  
  
     게시된 테이블의 경우 새 스파스 열을 테이블에 추가하거나 기존 열의 스파스 속성을 변경할 수 없습니다. 이러한 작업이 필요한 경우 게시를 삭제한 다음 다시 만듭니다.  
  
-   병합 복제  
  
     병합 복제는 스파스 열 또는 열 집합을 지원하지 않습니다.  
  
-   변경 내용 추적  
  
     변경 내용 추적은 스파스 열 및 열 집합을 지원합니다. 테이블에서 열 집합이 업데이트되면 변경 내용 추적이 이를 전체 행에 대한 업데이트로 처리합니다. 열 집합 업데이트 작업을 통해 업데이트되는 정확한 스파스 열 집합을 알 수 있는 자세한 변경 내용 추적은 제공되지 않습니다. 스파스 열이 DML 문을 통해 명시적으로 업데이트되는 경우에는 해당 열에 대한 변경 내용 추적이 일반적으로 작동하여 변경된 정확한 열 집합을 식별할 수 있습니다.  
  
-   변경 데이터 캡처  
  
     변경 데이터 캡처는 스파스 열을 지원하지만 열 집합은 지원하지 않습니다.  
  
-   열의 스파스 속성은 테이블을 복사할 때 보존되지 않습니다.  
  
## <a name="examples"></a>예  
 이 예의 Document 테이블에는 `DocID` 및 `Title`열을 사용하는 공통 집합이 포함되어 있습니다. Production 그룹은 모든 생산 문서에 대한 `ProductionSpecification` 및 `ProductionLocation` 열을 원하며, Marketing 그룹은 마케팅 문서에 대한 `MarketingSurveyGroup` 열을 원합니다. 이 예의 코드에서는 스파스 열을 사용하는 테이블을 만들고, 테이블에 두 개의 행을 삽입한 다음 테이블에서 데이터를 선택합니다.  
  
> [!NOTE]  
>  이 테이블에는 테이블을 보다 잘 표시하고 읽을 수 있도록 열이 5개만 있습니다. ANSI_NULL_DFLT_ON 옵션이 설정된 경우 스파스 열을 Null 허용으로 선언하는 작업은 선택 사항입니다.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TABLE DocumentStore  
    (DocID int PRIMARY KEY,  
     Title varchar(200) NOT NULL,  
     ProductionSpecification varchar(20) SPARSE NULL,  
     ProductionLocation smallint SPARSE NULL,  
     MarketingSurveyGroup varchar(20) SPARSE NULL ) ;  
GO  
  
INSERT DocumentStore(DocID, Title, ProductionSpecification, ProductionLocation)  
VALUES (1, 'Tire Spec 1', 'AXZZ217', 27);  
GO  
  
INSERT DocumentStore(DocID, Title, MarketingSurveyGroup)  
VALUES (2, 'Survey 2142', 'Men 25 - 35');  
GO  
```  
  
 테이블에서 모든 열을 선택하려면 일반 쿼리 집합을 반환합니다.  
  
```  
SELECT * FROM DocumentStore ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID  Title        ProductionSpecification  ProductionLocation  MarketingSurveyGroup`  
  
 `1      Tire Spec 1  AXZZ217                  27                  NULL`  
  
 `2      Survey 2142  NULL                     NULL                Men 25-35`  
  
 Production 부서는 마케팅 데이터에 관심이 없으므로 다음 쿼리에서처럼 관심 있는 열만 반환하는 열 목록을 사용하려고 합니다.  
  
```  
SELECT DocID, Title, ProductionSpecification, ProductionLocation   
FROM DocumentStore   
WHERE ProductionSpecification IS NOT NULL ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID  Title        ProductionSpecification  ProductionLocation`  
  
 `1      Tire Spec 1  AXZZ217                  27`  
  
## <a name="see-also"></a>참고 항목  
 [열 집합 사용](../../relational-databases/tables/use-column-sets.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
