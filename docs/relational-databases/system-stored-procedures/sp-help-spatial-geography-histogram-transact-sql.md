---
description: sp_help_spatial_geography_histogram(Transact-SQL)
title: sp_help_spatial_geography_histogram (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geography_histogram_TSQL
- sp_help_spatial_geography_histogram
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geography_histogram
ms.assetid: 5c5bd319-055d-4cd6-8c5a-06354cc056cc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0e1ba161b0baefa42b68960c26941926fb226288
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546107"
---
# <a name="sp_help_spatial_geography_histogram-transact-sql"></a>sp_help_spatial_geography_histogram(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  공간 인덱스에 대한 표 매개 변수의 키 지정을 용이하게 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_spatial_geography_histogram [ @tabname =] 'tabname'   
     [ , [ @colname = ] 'columnname' ]   
     [ , [ @resolution = ] 'resolution' ]  
     [ , [ @sample = ] 'tablesample' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @tabname = ] 'tabname'` 공간 인덱스가 지정 된 테이블의 정규화 된 이름 또는 정규화 되지 않은 이름입니다.  
  
 따옴표는 정규화된 테이블이 지정된 경우에만 필요합니다. 데이터베이스 이름을 포함한 정규화된 이름인 경우 반드시 현재 데이터베이스의 이름을 사용해야 합니다. *tabname* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @colname = ] 'columnname'` 지정 된 공간 열의 이름입니다. *columnname* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @resolution = ] 'resolution'` 경계 상자를 확인 하는 것입니다. 유효한 값은 10부터 5000까지입니다. *resolution* 은 **tinyint**이며 기본값은 없습니다.  
  
`[ @sample = ] 'sample'` 사용 되는 테이블의 백분율입니다. 유효한 값은 0에서 100 까지입니다. *tablesample* 은 **float**입니다. 기본값은 100입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 테이블 값이 반환됩니다. 다음 표에서는 테이블의 열 내용에 대해 설명합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**cellid**|**int**|각 셀의 고유한 ID를 나타내며 1부터 셉니다.|  
|**셀씩**|**geography**|각 셀을 나타내는 사각의 다각형입니다. 셀 셰이프는 공간 인덱싱에 사용된 셀 셰이프와 동일합니다.|  
|**row_count**|**bigint**|셀에 접해 있거나 셀을 포함하는 공간 개체 수를 나타냅니다.|  
  
## <a name="permissions"></a>사용 권한  
 사용자는 **public** 역할의 멤버 여야 합니다. 서버 및 개체에 대한 READ ACCESS 권한이 필요합니다.  
  
## <a name="remarks"></a>설명  
 SSMS 공간 탭은 결과를 그래픽으로 나타냅니다. 공간 창에서 결과를 쿼리하여 결과 항목의 대략적인 개수를 가져올 수 있습니다.  
  
> [!NOTE]  
>  테이블의 개체가 셀 한 개를 넘어갈 수 있으므로 테이블에 있는 셀 합계는 실제 개체의 개수보다 커야 합니다.  
  
 **지리** 형식에 대 한 경계 상자는 전체 구형입니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 데이터베이스의 테이블에 대해  **sp_help_spatial_geography_histogram** 를 호출 합니다 `Person.Address` [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
```  
EXEC sp_help_spatial_geography_histogram @tabname = Person.Address, @colname = SpatialLocation, @resolution = 64, @sample = 30;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;공간 인덱스 저장 프로시저 &#40;](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)  
  
  
