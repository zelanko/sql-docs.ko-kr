---
title: sys. soap_endpoints (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- soap_endpoints_TSQL
- sys.soap_endpoints
- soap_endpoints
- sys.soap_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.soap_endpoints catalog view
ms.assetid: f50dcbfc-02ed-4a19-9c07-c78a5a1b3224
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 46f42c185a1be2cbf8742a14cc7d897f19430ca1
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85901173"
---
# <a name="syssoap_endpoints-transact-sql"></a>sys.soap_endpoints(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 SOAP 유형 페이로드를 전달하는 서버의 각 엔드포인트에 대해 한 행을 포함합니다. 이 뷰의 모든 행에 대해 HTTP 구성 메타 데이터를 전달 하는 **http_endpoints** 카탈로그 뷰에 동일한 **endpoint_id** 의 해당 행이 있습니다.  
  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**상속 된 열<>**||이 뷰가 상속 하는 열 목록은 [sys. &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)를 참조 하세요.|  
|**is_sql_language_enabled**|**bit**|1 = BATCHES = ENABLED 옵션이 지정되었으므로 임시 SQL 일괄 처리가 엔드포인트에서 허용됩니다.|  
|**wsdl_generator_procedure**|**nvarchar (776)**|이 메서드를 구현하는 저장 프로시저의 세 부분으로 된 이름입니다.<br /><br /> 메서드의 이름은 정확히 세 부분으로 구성된 구문이어야 합니다. 한 부분, 두 부분 또는 네 부분으로 된 이름은 허용되지 않습니다.|  
|**default_database**|**sysname**|DATABASE = 옵션에 지정된 기본 데이터베이스의 이름입니다.<br /><br /> NULL = DEFAULT가 지정되었습니다.|  
|**default_namespace**|**nvarchar (384)**|NAMESPACE = 옵션에 지정 된 기본 네임 스페이스 `https://tempuri.org` 입니다. 대신 default가 지정 된 경우입니다.|  
|**default_result_schema**|**tinyint**|SCHEMA = 옵션의 기본값입니다.<br /><br /> 0 = 없음<br /><br /> 1 = 표준|  
|**default_result_schema_desc**|**nvarchar(60)**|SCHEMA = 옵션의 기본값에 대한 설명입니다.<br /><br /> NONE<br /><br /> STANDARD|  
|**is_xml_charset_enforced**|**bit**|0 = CHARACTER_SET = SQL 옵션이 지정되었습니다.<br /><br /> 1 = CHARACTER_SET = XML 옵션이 지정되었습니다.|  
|**is_session_enabled**|**bit**|0 = SESSION = DISABLE 옵션이 지정되었습니다.<br /><br /> 1 = SESSION = ENABLED 옵션이 지정되었습니다.|  
|**session_timeout**|**int**|SESSION_TIMEOUT = 옵션에 지정된 값입니다.|  
|**login_type**|**nvarchar(60)**|이 엔드포인트에서 허용되는 인증 유형입니다.<br /><br /> WINDOWS<br /><br /> MIXED|  
|**header_limit**|**int**|SOAP 헤더의 최대 허용 크기입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;끝점 카탈로그 뷰](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
