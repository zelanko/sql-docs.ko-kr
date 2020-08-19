---
description: NDEXPROPERTY(Transact-SQL)
title: INDEXPROPERTY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- INDEXPROPERTY
- INDEXPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INDEXPROPERTY function
- indexes [SQL Server], viewing
- indexes [SQL Server], properties
ms.assetid: 998d5788-4871-44a8-8125-0d9390868b84
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 065b792b1e9edec5bc8e1b12859e9152797ebfb3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417369"
---
# <a name="indexproperty-transact-sql"></a>NDEXPROPERTY(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  지정한 테이블 ID, 인덱스 또는 통계 이름, 속성 이름에 대해 명명된 인덱스 또는 통계 속성 값을 반환합니다. XML 인덱스에 대해서는 NULL을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
INDEXPROPERTY ( object_ID , index_or_statistics_name , property )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *object_ID*  
 인덱스 속성 정보를 제공할 테이블 또는 인덱싱된 뷰의 개체 ID가 포함된 식입니다. *object_ID* 는 **int**입니다.  
  
 *index_or_statistics_name*  
 속성 정보를 반환할 인덱스 또는 통계의 이름이 포함된 식입니다. *index_or_statistics_name*은 **nvarchar(128)** 입니다.  
  
 *property*  
 반환할 데이터베이스 속성의 이름이 포함된 식입니다. *property*는 **varchar(128)** 이며 다음 값 중 하나일 수 있습니다.  
  
> [!NOTE]  
>  달리 언급하지 않는 한 *property*가 유효한 속성 이름이 아니거나, *object_ID*가 유효한 개체 ID가 아니거나, *object_ID*가 지정된 속성에 대해 지원되지 않는 개체 유형이거나 또는 호출자가 개체의 메타데이터를 볼 수 있는 권한이 없는 경우에는 NULL이 반환됩니다.  
  
|속성|Description|값|  
|--------------|-----------------|-----------|  
|**IndexDepth**|인덱스의 깊이입니다.|인덱스 수준의 수입니다.<br /><br /> NULL = XML 인덱스이거나 입력이 잘못되었습니다.|  
|**IndexFillFactor**|인덱스를 만들거나 최근에 다시 만들 때 사용한 채우기 비율 값입니다.|채우기 비율|  
|**IndexID**|지정한 테이블 또는 인덱싱된 뷰에 대한 인덱스의 ID입니다.|Index ID|  
|**IsAutoStatistics**|통계가 ALTER DATABASE의 AUTO_CREATE_STATISTICS 옵션으로 생성되었습니다.|1 = True<br /><br /> 0 = False 또는 XML 인덱스|  
|**IsClustered**|인덱스가 클러스터형입니다.|1 = True<br /><br /> 0 = False 또는 XML 인덱스|  
|**IsDisabled**|인덱스가 비활성화되었습니다.|1 = True<br /><br /> 0 = False<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsFulltextKey**|인덱스가 테이블의 전체 텍스트 및 의미 체계 인덱싱 키입니다.|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 1 = True<br /><br /> 0 = False 또는 XML 인덱스<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsHypothetical**|인덱스가 가상 인덱스이며 데이터 액세스 경로로 직접 사용할 수 없습니다. 가상 인덱스는 열 수준 통계를 보유하며 데이터베이스 엔진 튜닝 관리자에서 유지 관리 및 사용됩니다.|1 = True<br /><br /> 0 = False 또는 XML 인덱스<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsPadIndex**|인덱스가 각 하위 노드에 남겨 둘 빈 공간을 지정합니다.|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 1 = True<br /><br /> 0 = False 또는 XML 인덱스|  
|**IsPageLockDisallowed**|ALTER INDEX의 ALLOW_PAGE_LOCKS 옵션으로 설정된 페이지 잠금 값입니다.|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 1 = 페이지 잠금이 허용되지 않습니다.<br /><br /> 0 = 페이지 잠금이 허용됩니다.<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsRowLockDisallowed**|ALTER INDEX의 ALLOW_ROW_LOCKS 옵션으로 설정된 행 잠금 값입니다.|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상<br /><br /> 1 = 행 잠금이 허용되지 않습니다.<br /><br /> 0 = 행 잠금이 허용됩니다.<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsStatistics**|*index_or_statistics_name*은 CREATE STATISTICS 문 또는 ALTER DATABASE의 AUTO_CREATE_STATISTICS 옵션으로 생성된 통계입니다.|1 = True<br /><br /> 0 = False 또는 XML 인덱스|  
|**IsUnique**|인덱스가 고유합니다.|1 = True<br /><br /> 0 = False 또는 XML 인덱스|  
|**IsColumnstore**|인덱스가 xVelocity 메모리 액세스에 최적화된 columnstore 인덱스입니다.|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상<br /><br /> 1 = True<br /><br /> 0 = False| 
|**IsOptimizedForSequentialKey**|인덱스에 대해 마지막 페이지 삽입 최적화가 사용됩니다.|**적용 대상**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 이상 <br><br>1 = True<br><br>0 = False| 
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="exceptions"></a>예외  
 오류가 발생하거나 호출자가 개체를 볼 수 있는 권한을 갖고 있지 않으면 NULL을 반환합니다.  
  
 사용자는 소유하고 있거나 사용 권한을 부여 받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자가 개체에 대한 사용 권한이 없으면 INDEXPROPERTY와 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예제  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에 있는 `Employee` 테이블의 `PK_Employee_BusinessEntityID` 인덱스에 대한 **IsClustered**, **IndexDepth** 및 **IndexFillFactor** 속성 값을 반환합니다.  
  
```  
SELECT   
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IsClustered')AS [Is Clustered],  
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IndexDepth') AS [Index Depth],  
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IndexFillFactor') AS [Fill Factor];  
  
```  
  
 결과 집합은 다음과 같습니다.  
  
```  
Is Clustered Index Depth Fill Factor   
------------ ----------- -----------   
1            2           0  
  
(1 row(s) affected)  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예는 `FactResellerSales` 테이블의 색인 중 하나의 속성을 검사합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT   
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IsClustered') AS [Is Clustered],  
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IsColumnstore') AS [Is Columnstore Index],  
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IndexFillFactor') AS [Fill Factor];  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [통계](../../relational-databases/statistics/statistics.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [sys.stats_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)  
  
  

