---
title: sys.soap_endpoints (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- soap_endpoints_TSQL
- sys.soap_endpoints
- soap_endpoints
- sys.soap_endpoints_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.soap_endpoints catalog view
ms.assetid: f50dcbfc-02ed-4a19-9c07-c78a5a1b3224
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 38bc05ab3d49716f2c4fc484098c4ff838bc634e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="syssoapendpoints-transact-sql"></a>sys.soap_endpoints(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 SOAP 유형 페이로드를 전달하는 서버의 각 끝점에 대해 한 행을 포함합니다. 이 뷰의 모든 행에 대 한 해당 행이 동일한 **endpoint_id** 에 **sys.http_endpoints** HTTP 구성 메타 데이터를 전달 주는 카탈로그 뷰입니다.  
  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**< 상속 된 열 >**||이 뷰가 상속 하는 열 목록은 참조 [sys.endpoints &#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**is_sql_language_enabled**|**bit**|1 = BATCHES = ENABLED 옵션이 지정되었으므로 임시 SQL 일괄 처리가 끝점에서 허용됩니다.|  
|**wsdl_generator_procedure**|**nvarchar(776)**|이 메서드를 구현하는 저장 프로시저의 세 부분으로 된 이름입니다.<br /><br /> 메서드의 이름은 정확히 세 부분으로 구성된 구문이어야 합니다. 한 부분, 두 부분 또는 네 부분으로 된 이름은 허용되지 않습니다.|  
|**default_database**|**sysname**|DATABASE = 옵션에 지정된 기본 데이터베이스의 이름입니다.<br /><br /> NULL = DEFAULT가 지정되었습니다.|  
|**기본 네임 스페이스**|**nvarchar(384)**|DEFAULT가 대신 지정된 경우 NAMESPACE = 옵션 또는 'http://tempuri.org'에 지정된 기본 네임스페이스입니다.|  
|**default_result_schema**|**tinyint**|SCHEMA = 옵션의 기본값입니다.<br /><br /> 0 = 없음<br /><br /> 1 = 표준|  
|**default_result_schema_desc**|**nvarchar (60)**|SCHEMA = 옵션의 기본값에 대한 설명입니다.<br /><br /> 없음<br /><br /> STANDARD|  
|**is_xml_charset_enforced**|**bit**|0 = CHARACTER_SET = SQL 옵션이 지정되었습니다.<br /><br /> 1 = CHARACTER_SET = XML 옵션이 지정되었습니다.|  
|**is_session_enabled**|**bit**|0 = SESSION = DISABLE 옵션이 지정되었습니다.<br /><br /> 1 = SESSION = ENABLED 옵션이 지정되었습니다.|  
|**session_timeout**|**int**|SESSION_TIMEOUT = 옵션에 지정된 값입니다.|  
|**login_type**|**nvarchar (60)**|이 끝점에서 허용되는 인증 유형입니다.<br /><br /> WINDOWS<br /><br /> MIXED|  
|**header_limit**|**int**|SOAP 헤더의 최대 허용 크기입니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [끝점 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
