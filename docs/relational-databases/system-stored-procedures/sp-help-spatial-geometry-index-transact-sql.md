---
title: sp_help_spatial_geometry_index (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_index
- sp_help_spatial_geometry_index_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_index procedure
ms.assetid: f1bcefb1-09c8-4b49-8c51-5d471065849f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 56db1455b1b85ea50fc5bdea7f6f3d06778d329f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749345"
---
# <a name="sp_help_spatial_geometry_index-transact-sql"></a>sp_help_spatial_geometry_index(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **기 하 도형** 공간 인덱스에 대해 지정 된 속성 집합의 이름과 값을 반환 합니다. 결과는 테이블 형식으로 반환됩니다. 인덱스의 핵심 속성 집합만 반환하거나 인덱스의 속성을 모두 반환하도록 선택할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_spatial_geometry_index [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ] 'verboseoutput'   
     [ , [ @query_sample = ] 'query_sample']   
```  
  
## <a name="arguments"></a>인수  
 [공간 인덱스 저장 프로시저의 인수 및 속성을](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)참조 하세요.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 [공간 인덱스 저장 프로시저의 인수 및 속성을](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 사용자가 이 프로시저에 액세스하려면 PUBLIC 역할을 할당받아야 합니다. 서버 및 개체에 대한 READ ACCESS 권한이 필요합니다.  
  
## <a name="remarks"></a>설명  
 NULL 값이 포함된 속성은 반환 집합에 포함되지 않습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 `sp_help_spatial_geometry_index` 를 사용 하 여 ** \@ qs**의 지정 된 쿼리 샘플에 대 한 테이블 **geometry_col** 에 정의 된 **SIndx_SpatialTable_geometry_col2** 공간 인덱스를 조사 합니다. 이 예에서는 지정된 인덱스의 핵심 속성만 반환합니다.  
  
```  
declare @qs geometry  
        ='POLYGON((-90.0 -180.0, -90.0 180.0, 90.0 180.0, 90.0 -180.0, -90.0 -180.0))';  
exec sp_help_spatial_geometry_index 'geometry_col', 'SIndx_SpatialTable_geometry_col2', 0, @qs;  
```  
  
## <a name="see-also"></a>참고 항목  
 [공간 인덱스 저장 프로시저](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index_xml](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)   
 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
