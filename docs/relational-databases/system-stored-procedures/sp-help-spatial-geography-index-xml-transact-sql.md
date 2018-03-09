---
title: sp_help_spatial_geography_index_xml (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geography_index_xml_TSQL
- sp_help_spatial_geography_index_xml
dev_langs: TSQL
helpviewer_keywords: sp_help_spatial_geography_index_xml procedure
ms.assetid: 821d4127-3ce5-4474-8561-043404a20d81
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ffc4f49e8087189e9fd7d364d4d9ee3cc668573a
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpspatialgeographyindexxml-transact-sql"></a>sp_help_spatial_geography_index_xml(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  에 대 한 이름 및 지정된 된 속성 집합에 대 한 값을 반환는 **geography** 공간 인덱스입니다. 인덱스의 핵심 속성 집합만 반환하거나 인덱스의 속성을 모두 반환하도록 선택할 수 있습니다.  
  
 결과는 선택한 속성의 이름과 값을 표시하는 XML 조각으로 반환됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_spatial_geography_index_xml [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ] 'verboseoutput' ]   
     [ , [ @query_sample = ] 'query_sample' ]   
     [ ,.[ @xml_output = ] 'xml_output' ]   
```  
  
## <a name="arguments"></a>인수  
 참조 [인수 및 공간 인덱스의 속성에 대 한 저장 프로시저](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)합니다.  
  
## <a name="properties"></a>속성  
 참조 [인수 및 공간 인덱스의 속성에 대 한 저장 프로시저](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 사용자가 이 프로시저에 액세스하려면 PUBLIC 역할을 할당받아야 합니다. 서버 및 개체에 대한 READ ACCESS 권한이 필요합니다.  
  
## <a name="remarks"></a>주의  
 NULL 값이 포함된 속성은 반환 집합에 포함되지 않습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `sp_help_spatial_geography_index_xml` 공간 인덱스를 조사 하려면 **SIndx_SpatialTable_geography_col2** 테이블에 정의 된 **geography_col** 지정된 쿼리 샘플에 대 한  **@qs**. 이 예에서는 지정된 인덱스의 핵심 속성을 선택한 속성의 이름과 값을 표시하는 XML 조각으로 반환합니다.  
  
 [XQuery](../../xquery/xquery-basics.md) 그런 다음 특정 속성이 반환 하는 결과 집합에서 실행 됩니다.  
  
```  
declare @qs geography  
        ='POLYGON((-90.0 -180, -90 180.0, 90 180.0, 90 -180, -90 -180.0))';  
declare @x xml;  
exec sp_help_spatial_geography_index_xml 'geography_col', 'SIndx_SpatialTable_geography_col2', 0, @qs, @x output;  
select @x.value('(/Primary_Filter_Efficiency/text())[1]', 'float');  
```  
  
 비슷한 [sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md),이 저장된 프로시저의 속성에 더 간단한 프로그래밍 방식의 액세스를 제공는 **geography** 공간 인덱스 및 결과 집합을 XML 보고서입니다.  
  
 경계 상자는 **geography** 는 전체 지구입니다.  
  
## <a name="requirements"></a>요구 사항  
  
## <a name="see-also"></a>관련 항목:  
 [공간 인덱스 저장 프로시저](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)   
 [공간 인덱스 개요](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [XQuery 기초](../../xquery/xquery-basics.md)   
 [XQuery 언어 참조](../../xquery/xquery-language-reference-sql-server.md)  
  
  
