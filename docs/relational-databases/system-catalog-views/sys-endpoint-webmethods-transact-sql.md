---
title: sys. endpoint_webmethods (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.endpoint_webmethods_TSQL
- sys.endpoint_webmethods
- endpoint_webmethods_TSQL
- sys.http_soap_methods_TSQL
- endpoint_webmethods
- sys.http_soap_methods
dev_langs:
- TSQL
helpviewer_keywords:
- sys.endpoint_webmethods catalog view
ms.assetid: 7dad0cf6-eafa-47cf-98cc-75ba8d3c7959
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e5221cee27953e91015ca0b50075392c4314403f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893274"
---
# <a name="sysendpoint_webmethods-transact-sql"></a>sys.endpoint_webmethods(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 SOAP 기반 HTTP 엔드포인트에서 정의된 각 SOAP 메서드에 대한 행을 포함합니다. endpoint_id 및 namespace 열의 조합은 고유합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|endpoint_id|**int**|웹 메서드가 정의된 엔드포인트의 ID입니다.|  
|네임스페이스|**nvarchar (384)**|웹 메서드의 네임스페이스입니다.|  
|method_alias|**nvarchar (64)**|메서드의 별칭입니다.<br /><br /> 참고: [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자는 WSDL 메서드 이름에서 유효 하지 않은 문자를 허용 합니다.<br /><br /> 별칭은 엔드포인트의 WSDL 설명에 표시된 이름을 웹 메서드를 호출할 때 호출되는 실제 기본 [!INCLUDE[tsql](../../includes/tsql-md.md)] 실행 개체에 매핑하는 데 사용합니다.|  
|object_name|**nvarchar (776)**|NAME = 옵션에 지정된 대로 웹 메서드가 리디렉션되는 개체 이름입니다. 이름 부분은 마침표 (.)로 구분 되 고 대괄호를 사용 하 여 구분 됩니다 `[``]` .<br /><br /> 개체 이름은 WSDL 옵션에 지정된 대로 세 부분으로 구성되어야 합니다.|  
|result_schema|**tinyint**|응답과 함께 다시 전송할 XSD를 결정하는 옵션입니다(있는 경우).<br /><br /> 0 = 없음<br /><br /> 1 = 표준<br /><br /> 2 = 기본값|  
|result_schema_desc|**nvarchar(60)**|응답과 함께 다시 전송할 XSD를 결정하는 옵션에 대한 설명입니다(있는 경우).<br /><br /> NONE<br /><br /> STANDARD<br /><br /> DEFAULT|  
|result_format|**tinyint**|응답에서 결과의 서식이 지정되는 방식을 결정하는 옵션입니다.<br /><br /> 1 = ALL_RESULTS<br /><br /> 2 = ROWSETS_ONLY<br /><br /> 3 = NONE|  
|result_format_desc|**nvarchar(60)**|응답에서 결과의 서식이 지정되는 방식을 결정하는 옵션에 대한 설명입니다.<br /><br /> ALL_RESULTS<br /><br /> ROWSETS_ONLY<br /><br /> NONE|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;끝점 카탈로그 뷰](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
