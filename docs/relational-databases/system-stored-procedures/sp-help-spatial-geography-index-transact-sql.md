---
title: sp_help_spatial_geography_index (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geography_index
- sp_help_spatial_geography_index_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geography_index procedure
ms.assetid: c9bf5675-eafc-4d71-bfdb-da963384fa0c
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5775b3fafac1a6310be9f78dcd3d079ae28a76e2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47603741"
---
# <a name="sphelpspatialgeographyindex-transact-sql"></a>sp_help_spatial_geography_index(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  에 대 한 이름 및 지정된 된 속성 집합에 대 한 값을 반환 된 **지리** 공간 인덱스입니다. 결과는 테이블 형식으로 반환됩니다. 인덱스의 핵심 속성 집합만 반환하거나 인덱스의 속성을 모두 반환하도록 선택할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_spatial_geography_index [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ] 'verboseoutput' ]   
     [ , [ @query_sample = ] 'query_sample' ]   
```  
  
## <a name="arguments"></a>인수  
 참조 [저장 프로시저 인수 및 공간 인덱스의 속성](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)합니다.  
  
## <a name="properties"></a>속성  
 참조 [저장 프로시저 인수 및 공간 인덱스의 속성](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 사용자가 이 프로시저에 액세스하려면 PUBLIC 역할을 할당받아야 합니다. 서버 및 개체에 대한 READ ACCESS 권한이 필요합니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="example"></a>예제  
 다음 예제에서는 `sp_help_spatial_geography_index` 조사 하는 **지리** 공간 인덱스 **SIndx_SpatialTable_geography_col2** 테이블에 정의 된 **geography_col** 지정 된 쿼리 예제에 대 한 **@qs**합니다. 이 예에서는 지정된 인덱스의 핵심 속성만 반환합니다.  
  
```  
declare @qs geography  
        ='POLYGON((-90.0 -180, -90 180.0, 90 180.0, 90 -180, -90 -180.0))';  
exec sp_help_spatial_geography_index 'geography_col', 'SIndx_SpatialTable_geography_col2', 0, @qs;  
```  
  
 경계 상자는 **지리** 인스턴스는 전체 지구입니다.  
  
## <a name="requirements"></a>요구 사항  
  
## <a name="see-also"></a>관련 항목  
 [공간 인덱스 저장 프로시저](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)   
 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
