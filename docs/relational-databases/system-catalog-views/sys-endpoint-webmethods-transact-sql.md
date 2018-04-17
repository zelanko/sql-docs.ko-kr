---
title: sys.endpoint_webmethods (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 039f084d20aa1b64bdd841b9279be5a065e4a9f6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysendpointwebmethods-transact-sql"></a>sys.endpoint_webmethods(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 SOAP 기반 HTTP 끝점에서 정의된 각 SOAP 메서드에 대한 행을 포함합니다. Endpoint_id 및 네임 스페이스 열 조합에는 고유 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|endpoint_id|**int**|웹 메서드가 정의된 끝점의 ID입니다.|  
|네임스페이스|**nvarchar(384)**|웹 메서드의 네임스페이스입니다.|  
|method_alias|**nvarchar(64)**|메서드의 별칭입니다.<br /><br /> 참고: [!INCLUDE[tsql](../../includes/tsql-md.md)] 식별자는 WSDL 메서드 이름에 유효 하지 않은 문자를 허용 합니다.<br /><br /> 별칭은 끝점의 WSDL 설명에 표시된 이름을 웹 메서드를 호출할 때 호출되는 실제 기본 [!INCLUDE[tsql](../../includes/tsql-md.md)] 실행 개체에 매핑하는 데 사용합니다.|  
|object_name|**nvarchar(776)**|NAME = 옵션에 지정된 대로 웹 메서드가 리디렉션되는 개체 이름입니다. 이름 부분에 마침표 (.), 구분 되 고 대괄호를 사용 하 여 구분할 `[``]`합니다.<br /><br /> 개체 이름은 WSDL 옵션에 지정된 대로 세 부분으로 구성되어야 합니다.|  
|result_schema|**tinyint**|응답과 함께 다시 전송할 XSD를 결정하는 옵션입니다(있는 경우).<br /><br /> 0 = 없음<br /><br /> 1 = 표준<br /><br /> 2 = 기본값|  
|result_schema_desc|**nvarchar(60)**|응답과 함께 다시 전송할 XSD를 결정하는 옵션에 대한 설명입니다(있는 경우).<br /><br /> 없음<br /><br /> STANDARD<br /><br /> DEFAULT|  
|result_format|**tinyint**|응답에서 결과의 서식이 지정되는 방식을 결정하는 옵션입니다.<br /><br /> 1 = ALL_RESULTS<br /><br /> 2 = ROWSETS_ONLY<br /><br /> 3 = 없음|  
|result_format_desc|**nvarchar(60)**|응답에서 결과의 서식이 지정되는 방식을 결정하는 옵션에 대한 설명입니다.<br /><br /> ALL_RESULTS<br /><br /> ROWSETS_ONLY<br /><br /> 없음|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [엔드포인트 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
