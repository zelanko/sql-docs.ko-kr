---
title: INDEXPROPERTY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 56
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 2f793612ff0fa46e2fd72f6a51e48eae30602fdf
ms.contentlocale: ko-kr
ms.lasthandoff: 10/24/2017

---
# <a name="indexproperty-transact-sql"></a>NDEXPROPERTY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정한 테이블 ID, 인덱스 또는 통계 이름, 속성 이름에 대해 명명된 인덱스 또는 통계 속성 값을 반환합니다. XML 인덱스에 대해서는 NULL을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
INDEXPROPERTY ( object_ID , index_or_statistics_name , property )   
```  
  
## <a name="arguments"></a>인수  
 *object_ID*  
 인덱스 속성 정보를 제공할 테이블 또는 인덱싱된 뷰의 개체 ID가 포함된 식입니다. *object_ID* 은 **int**합니다.  
  
 *index_or_statistics_name*  
 속성 정보를 반환할 인덱스 또는 통계의 이름이 포함된 식입니다. *index_or_statistics_name* 은 **nvarchar (128)**합니다.  
  
 *속성*  
 반환할 데이터베이스 속성의 이름이 포함된 식입니다. *속성* 은 **varchar (128)**, 다음이 값 중 하나일 수 있습니다.  
  
> [!NOTE]  
>  달리 언급 하지 않는 한 NULL이 반환 됩니다 *속성* 올바른 속성 이름이 아닙니다 *object_ID* 는 유효한 개체 id *object_ID* 는 지원 되지 않는 개체 형식입니다. 지정된 된 속성을 기다리거나 없는 개체의 메타 데이터를 볼 수 있는 권한이 있습니다.  
  
|속성|Description|값|  
|--------------|-----------------|-----------|  
|**IndexDepth**|인덱스의 깊이입니다.|인덱스 수준의 수입니다.<br /><br /> NULL = XML 인덱스이거나 입력이 잘못되었습니다.|  
|**IndexFillFactor**|인덱스를 만들거나 최근에 다시 만들 때 사용한 채우기 비율 값입니다.|채우기 비율|  
|**IndexID**|지정한 테이블 또는 인덱싱된 뷰에 대한 인덱스의 ID입니다.|Index ID|  
|**IsAutoStatistics**|통계가 ALTER DATABASE의 AUTO_CREATE_STATISTICS 옵션으로 생성되었습니다.|1 = True<br /><br /> 0 = False 또는 XML 인덱스|  
|**IsClustered**|인덱스가 클러스터형입니다.|1 = True<br /><br /> 0 = False 또는 XML 인덱스|  
|**IsDisabled**|인덱스가 비활성화되었습니다.|1 = True<br /><br /> 0 = False<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsFulltextKey**|인덱스가 테이블의 전체 텍스트 및 의미 체계 인덱싱 키입니다.|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 1 = True<br /><br /> 0 = False 또는 XML 인덱스<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsHypothetical**|인덱스가 가상 인덱스이며 데이터 액세스 경로로 직접 사용할 수 없습니다. 가상 인덱스는 열 수준 통계를 보유하며 데이터베이스 엔진 튜닝 관리자에서 유지 관리 및 사용됩니다.|1 = True<br /><br /> 0 = False 또는 XML 인덱스<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsPadIndex**|인덱스가 각 하위 노드에 남겨 둘 빈 공간을 지정합니다.|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 1 = True<br /><br /> 0 = False 또는 XML 인덱스|  
|**IsPageLockDisallowed**|ALTER INDEX의 ALLOW_PAGE_LOCKS 옵션으로 설정된 페이지 잠금 값입니다.|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 1 = 페이지 잠금이 허용되지 않습니다.<br /><br /> 0 = 페이지 잠금이 허용됩니다.<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsRowLockDisallowed**|ALTER INDEX의 ALLOW_ROW_LOCKS 옵션으로 설정된 행 잠금 값입니다.|**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 1 = 행 잠금이 허용되지 않습니다.<br /><br /> 0 = 행 잠금이 허용됩니다.<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsStatistics**|*index_or_statistics_name* 는 CREATE STATISTICS 문 또는 ALTER DATABASE의 AUTO_CREATE_STATISTICS 옵션으로 만든 통계입니다.|1 = True<br /><br /> 0 = False 또는 XML 인덱스|  
|**IsUnique**|인덱스가 고유합니다.|1 = True<br /><br /> 0 = False 또는 XML 인덱스|  
|**IsColumnstore**|인덱스가 xVelocity 메모리 액세스에 최적화된 columnstore 인덱스입니다.|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> 1 = True<br /><br /> 0 = False|  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="exceptions"></a>예외  
 오류가 발생하거나 호출자가 개체를 볼 수 있는 권한을 갖고 있지 않으면 NULL을 반환합니다.  
  
 사용자는 소유하고 있거나 사용 권한을 부여 받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자가 개체에 대한 사용 권한이 없으면 INDEXPROPERTY와 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 에 대 한 값을 반환 하는 다음 예제는 **IsClustered**, **IndexDepth**, 및 **IndexFillFactor** 에 대 한 속성의 `PK_Employee_BusinessEntityID` 는 의인덱스`Employee`테이블에 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스입니다.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예제에는 인덱스 중 하나의 속성을 검사 하 고 `FactResellerSales` 테이블입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [통계](../../relational-databases/statistics/statistics.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [sys.stats_columns &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)  
  
  


