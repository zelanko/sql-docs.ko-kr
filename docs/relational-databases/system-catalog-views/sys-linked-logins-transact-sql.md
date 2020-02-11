---
title: sys. linked_logins (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.linked_logins
- sys.linked_logins_TSQL
- linked_logins_TSQL
- linked_logins
dev_langs:
- TSQL
helpviewer_keywords:
- sys.linked_logins catalog view
ms.assetid: af57bf0c-a265-410f-9bab-63b78569b4a6
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: dfde20205de71a302c7ba8151fc6171cecc05a08
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68140676"
---
# <a name="syslinked_logins-transact-sql"></a>sys.linked_logins(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로컬 서버에서 연결된 해당 서버로의 분산 쿼리 및 RPC에서 사용할 수 있도록 연결된 서버 로그인 매핑당 한 행씩을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|**Sys. servers**의 서버 ID입니다.|  
|**local_principal_id**|**int**|매핑이 적용되는 서버 보안 주체입니다.<br /><br /> 0 = 와일드카드 또는 공용입니다.|  
|**uses_self_credential**|**bit**|1일 경우 매핑은 세션에서 자체의 자격 증명을 사용해야 함을 나타냅니다. 그렇지 않은 경우 0은 세션에서 제공된 이름과 암호를 사용함을 나타냅니다.|  
|**remote_name**|**sysname**|연결할 때 사용할 원격 사용자 이름입니다. 암호 역시 저장되지만 카탈로그 뷰 인터페이스에서는 표시되지 않습니다.|  
|**modify_date**|**datetime**|연결된 로그인을 마지막으로 변경한 날짜입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [연결 된 서버 카탈로그 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)  
  
  
