---
description: sys.http_endpoints(Transact-SQL)
title: sys. http_endpoints (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.http_endpoints
- http_endpoints
- sys.http_endpoints_TSQL
- http_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.http_endpoints catalog view
ms.assetid: 16f59695-ecd9-457e-8874-055af63f8ea7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2672f010bb9345b3ce37ee52ec8aa96d28c79469
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537380"
---
# <a name="syshttp_endpoints-transact-sql"></a>sys.http_endpoints(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  HTTP 프로토콜을 사용하는 서버에 생성된 각 엔드포인트당 하나의 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|** 상속 된 열<>**||[&#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)에서 열을 상속 합니다.|  
|**사이트별**|**nvarchar(128)**|이 사이트에 대한 호스트 컴퓨터의 이름이며 SITE = 옵션으로 지정됩니다.|  
|**url_path**|**nvarchar(4000)**|이 HTTP 엔드포인트에 대한 URL의 경로 부분이며 PATH= 옵션으로 지정됩니다.|  
|**is_clear_port_enabled**|**bit**|1 = CLEAR 포트가 PORT = CLEAR 옵션을 사용하여 활성화되었습니다.|  
|**clear_port**|**int**|CLEAR PORT = 옵션에 지정된 포트 번호입니다.<br /><br /> NULL = 지정되지 않음|  
|**is_ssl_port_enabled**|**bit**|1 = SSL 포트가 PORT = SSL 옵션을 사용하여 활성화되었습니다.|  
|**ssl_port**|**int**|SSL PORT = 옵션에 지정된 포트 번호 값입니다.<br /><br /> NULL = 지정되지 않음|  
|**is_anonymous_enabled**|**bit**|1 = 익명 액세스가 AUTHENTICATION = ANONYMOUS 옵션을 사용하여 활성화되었습니다.|  
|**is_basic_auth_enabled**|**bit**|1 = 기본 인증이 AUTHENTICATION = BASIC 옵션을 사용하여 활성화되었습니다.|  
|**is_digest_auth_enabled**|**bit**|1 = 다이제스트 인증이 AUTHENTICATION = DIGEST 옵션을 사용하여 활성화되었습니다.|  
|**is_kerberos_auth_enabled**|**bit**|1 = 통합 인증이 AUTHENTICATION = KERBEROS 옵션을 사용하여 활성화되었습니다.|  
|**is_ntlm_auth_enabled**|**bit**|1 = 통합 인증이 AUTHENTICATION = NTLM 옵션을 사용하여 활성화되었습니다.|  
|**is_integrated_auth_enabled**|**bit**|1 = 통합 인증이 AUTHENTICATION = INTEGRATED 옵션을 사용하여 활성화되었습니다.|  
|**authorization_realm**|**nvarchar(128)**|HTTP DIGEST 인증 시도의 일부로서 클라이언트에 반환된 힌트입니다. AUTH REALM 옵션의 값입니다.<br /><br /> 지정되지 않았거나 DIGEST 인증이 활성화되지 않았으면 NULL입니다.|  
|**default_logon_domain**|**nvarchar(128)**|BASIC 인증을 활성화한 경우 기본 로그인 도메인입니다. DEFAULT LOGON DOMAIN 옵션의 값입니다.<br /><br /> 지정되지 않았거나 BASIC 인증이 활성화되지 않았으면 NULL입니다.|  
|**is_compression_enabled**|**bit**|1 = COMPRESSION = ENABLED 옵션이 설정되었습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [엔드포인트 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  
  
  
