---
title: MSSQLSERVER_2501 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2501 (Database Engine error)
ms.assetid: 895aafe3-a4e7-4ed8-acc5-93be76ef3664
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9d4920be6af560cbd5bd1d7699dd6378cdc2db3b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914853"
---
# <a name="mssqlserver2501"></a>MSSQLSERVER_2501
    
## <a name="details"></a>설명  
  
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
  
-   현재의 데이터베이스 컨텍스트가 올바른지 확인하십시오. 자세한 내용은 [USE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql)를 참조하세요.  
  
-   테이블 또는 개체 이름의 철자가 올바른지 확인하십시오.  
  
-   개체가 포함된 스키마 이름을 확인하십시오. 기본(**dbo**) 스키마가 아닌 다른 스키마에 개체가 속할 경우 두 부분으로 구성된 형식 *schema_name.object_name*을 사용하여 테이블 또는 개체 이름을 지정해야 합니다.  
  
-   개체가 시스템 테이블에 있는지 확인하십시오. 테이블 또는 기타 스키마 범위 개체가 있는지 확인하려면 [sys.objects](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql) 카탈로그 뷰를 쿼리하세요. 개체가 시스템 테이블에 없는 경우 개체가 삭제되었거나 사용자에게 해당 개체 메타데이터를 볼 수 있는 권한이 없는 것입니다. 개체 메타데이터를 보는 방법에 대한 자세한 내용은 [메타데이터 표시 유형 구성](../security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql)  
  
  
