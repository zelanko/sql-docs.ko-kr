---
title: MSSQLSERVER_2501 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2501 (Database Engine error)
ms.assetid: 895aafe3-a4e7-4ed8-acc5-93be76ef3664
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e4246f2779b9b3b38ba2c0872e30066d2fbd607b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver2501"></a>MSSQLSERVER_2501
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2501|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_NO_SUCH_TABLE_NAME|  
|메시지 텍스트|이름이 'NAME'인 테이블 또는 개체를 찾을 수 없습니다. 시스템 카탈로그를 확인하십시오.|  
  
## <a name="explanation"></a>설명  
지정한 개체를 찾을 수 없습니다.  
  
### <a name="possible-causes"></a>가능한 원인  
이 오류는 다음과 같은 문제로 인해 발생할 수 있습니다.  
  
-   개체가 올바르게 지정되지 않았습니다.  
  
-   개체가 없거나 문에서 사용하기 전에 삭제되었습니다.  
  
-   개체가 있지만 사용자에게 표시되지 않았습니다. 예를 들어 사용자에게 해당 개체에 대한 사용 권한이 없거나 해당 개체가 사용자에게 표시되지 않는 내부 테이블일 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
  
-   현재의 데이터베이스 컨텍스트가 올바른지 확인하십시오. 자세한 내용은 [USE&#40;Transact-SQL&#41;](~/t-sql/language-elements/use-transact-sql.md)를 참조하세요.  
  
-   테이블 또는 개체 이름의 철자가 올바른지 확인하십시오.  
  
-   개체가 포함된 스키마 이름을 확인하십시오. 기본(**dbo**) 스키마가 아닌 다른 스키마에 개체가 속할 경우 두 부분으로 구성된 형식 *schema_name.object_name*을 사용하여 테이블 또는 개체 이름을 지정해야 합니다.  
  
-   개체가 시스템 테이블에 있는지 확인하십시오. 테이블 또는 기타 스키마 범위 개체가 있는지 확인하려면 [sys.objects](~/relational-databases/system-catalog-views/sys-objects-transact-sql.md) 카탈로그 뷰를 쿼리하세요. 개체가 시스템 테이블에 없는 경우 개체가 삭제되었거나 사용자에게 해당 개체 메타데이터를 볼 수 있는 권한이 없는 것입니다. 개체 메타데이터를 보는 방법에 대한 자세한 내용은 [메타데이터 표시 유형 구성](~/relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[카탈로그 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
