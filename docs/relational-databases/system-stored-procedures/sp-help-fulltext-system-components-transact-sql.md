---
title: sp_help_fulltext_system_components (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_components_TSQL
- sp_help_fulltext_components
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_system_components
ms.assetid: ac1fc7a0-7f46-4a12-8c5c-8d378226a8ce
caps.latest.revision: 52
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 849f2bbd004c47992c6b6faecf06b5abe5bcc9ea
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sphelpfulltextsystemcomponents-transact-sql"></a>sp_help_fulltext_system_components(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  등록된 단어 분리기, 필터 및 프로토콜 처리기에 대한 정보를 반환합니다. **sp_help_fulltext_system_components** 지정된 된 구성 요소를 사용한 전체 텍스트 카탈로그 및 데이터베이스 식별자 목록도 반환 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_fulltext_system_components   
         { 'all'| [ @component_type = ] 'component_type' }  
    , [ @param = ] 'param'  
```  
  
## <a name="arguments"></a>인수  
 'all'  
 전체 텍스트 구성 요소에 대한 정보를 반환합니다.  
  
 [ **@component_type=** ] *component_type*  
 구성 요소 유형을 지정합니다. *component_type* 다음 중 하나일 수 있습니다.  
  
-   **wordbreaker**  
  
-   **filter**  
  
-   **프로토콜 처리기**  
  
-   **fullpath**  
  
 전체 경로를 지정하는 경우 구성 요소 DLL의 전체 경로에도 *param* 을 지정해야 하며 그렇지 않으면 오류 메시지가 반환됩니다.  
  
 [ **@param=** ] *param*  
 구성 요소 유형에 따라 LCID(로캘 ID), "." 접두사가 있는 LCID(로캘 ID), "." 접두사가 있는 파일 확장명, 프로토콜 처리기의 전체 구성 요소 이름 또는 구성 요소 DLL의 전체 경로 중 하나일 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 다음 결과 집합이 시스템 구성 요소에 대해 반환됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**componenttype**|**sysname**|구성 요소의 유형입니다. 다음 중 하나일 수 있습니다.<br /><br /> filter<br /><br /> 프로토콜 처리기<br /><br /> 단어 분리기|  
|**componentname**|**sysname**|구성 요소의 이름입니다.|  
|**clsid**|**uniqueidentifier**|구성 요소의 클래스 식별자입니다.|  
|**fullpath**|**nvarchar(256)**|구성 요소 위치에 대한 경로입니다.<br /><br /> NULL = 호출자의 구성원이 아닌 **serveradmin** 고정된 서버 역할입니다.|  
|**version**|**nvarchar(30)**|구성 요소 버전입니다.|  
|**manufacturer**|**sysname**|구성 요소 제조업체의 이름입니다.|  
  
 경우에 다음 결과 집합 반환 되거나 둘 이상의 전체 텍스트 카탈로그를 사용 하는 존재 *component_type*합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**dbid**|**int**|데이터베이스의 ID입니다.|  
|**ftcatid**|**int**|전체 텍스트 카탈로그의 ID입니다.|  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요는 **공용** 역할입니다; 그러나 사용자가 볼 수 VIEW DEFINITION 권한을 갖고 있는 전체 텍스트 카탈로그에 대 한 정보입니다. **serveradmin** 고정 서버 역할의 멤버만 **fullpath** 열의 값을 볼 수 있습니다.  
  
## <a name="remarks"></a>주의  
 이 메서드는 업그레이드를 준비할 때 특히 중요합니다. 특정 데이터베이스 내에서 저장 프로시저를 실행하고, 출력을 사용하여 특정 카탈로그가 업그레이드에 영향을 받는지 여부를 지정합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-all-full-text-system-components"></a>1. 모든 전체 텍스트 시스템 구성 요소 나열  
 다음 예에서는 서버 인스턴스에 등록된 모든 전체 텍스트 시스템 구성 요소를 나열합니다.  
  
```  
EXEC sp_help_fulltext_system_components 'all';  
GO  
```  
  
### <a name="b-listing-word-breakers"></a>2. 단어 분리기 나열  
 다음 예에서는 서비스 인스턴스에 등록된 모든 단어 분리기를 나열합니다.  
  
```  
EXEC sp_help_fulltext_system_components 'wordbreaker';  
GO  
```  
  
### <a name="c-determining-whether-a-specific-word-breaker-is-registered"></a>3. 특정 단어 분리기의 등록 여부 확인  
 다음 예에서는 시스템에 설치되어 있으며 서비스 인스턴스에 등록되어 있는 터키어(LCID=1055)용 단어 분리기를 나열합니다. 이 예에서는 매개 변수 이름 지정 **@component_type** 및 **@param**합니다.  
  
```  
EXEC sp_help_fulltext_system_components @component_type = 'wordbreaker', @param = 1055;  
GO  
```  
  
 기본적으로 이 단어 분리기는 설치되지 않으므로 결과 집합이 비어 있습니다.  
  
### <a name="d-determining-whether-a-specific-filter-has-been-registered"></a>4. 특정 필터의 등록 여부 확인  
 다음 예에서는 수동으로 시스템에 설치되어 있으며 서버 인스턴스에 등록되어 있는 .xdoc 구성 요소에 대한 필터를 나열합니다.  
  
```  
EXEC sp_help_fulltext_system_components 'filter', '.xdoc';  
GO  
```  
  
 기본적으로 이 필터는 설치되지 않으므로 결과 집합이 비어 있습니다.  
  
### <a name="e-listing-a-specific-dll-file"></a>5. 특정 .dll 파일 나열  
 다음 예에서는 기본적으로 설치되는 특정 .ddl 파일 `nlhtml.dll`을 나열합니다.  
  
```  
EXEC sp_help_fulltext_system_components 'fullpath',   
   'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\nlhtml.dll';  
GO  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [등록 된 필터와 단어 분리기 보기 또는 변경](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)   
 [검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [검색 필터 구성 및 관리](../../relational-databases/search/configure-and-manage-filters-for-search.md)   
 [전체 텍스트 검색 및 의미 체계 검색 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
