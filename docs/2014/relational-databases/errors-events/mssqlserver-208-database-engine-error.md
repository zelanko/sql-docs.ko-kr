---
title: MSSQLSERVER_208 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 208 (Database Engine error)
ms.assetid: 4b1895f5-3197-4da1-af86-954c93507956
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b87a950c29cf202124e27b319eb56fb6a6e1857d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62914918"
---
# <a name="mssqlserver208"></a>MSSQLSERVER_208
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|208|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQ_BADOBJECT|  
|메시지 텍스트|개체 이름 '%.*ls'이(가) 잘못되었습니다.|  
  
## <a name="explanation"></a>설명  
 지정한 개체를 찾을 수 없습니다.  
  
### <a name="possible-causes"></a>가능한 원인  
 이 오류는 다음과 같은 문제로 인해 발생할 수 있습니다.  
  
-   개체가 올바르게 지정되지 않았습니다.  
  
-   개체가 현재 데이터베이스 또는 지정된 데이터베이스에 없습니다.  
  
-   개체가 있지만 사용자에게 표시되지 않았습니다. 예를 들어 사용자에게 해당 개체에 대한 사용 권한이 없거나 해당 개체가 EXECUTE 문 내에서 만들어졌지만 EXECUTE 문의 외부에서 액세스되었을 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 다음 정보를 확인하고 적절하게 문을 수정하십시오.  
  
-   개체 이름의 철자가 올바른지 여부.  
  
-   현재의 데이터베이스 컨텍스트가 올바른지 여부. 데이터베이스 이름이 지정되지 않은 개체는 현재 데이터베이스에 있어야 합니다. 데이터베이스 컨텍스트를 설정하는 방법은 [USE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql)를 참조하세요.  
  
-   개체가 시스템 테이블에 있는지 여부. 테이블 또는 기타 스키마 범위 개체가 있는지 확인하려면 **sys.objects** 카탈로그 뷰를 쿼리하세요. 개체가 시스템 테이블에 없는 경우 개체가 삭제되었거나 사용자에게 해당 개체 메타데이터를 볼 수 있는 권한이 없는 것입니다. 개체 메타데이터를 볼 수 있는 권한에 대한 자세한 내용은 [메타데이터 표시 유형 구성](../security/metadata-visibility-configuration.md)을 참조하세요.  
  
-   개체가 사용자의 기본 스키마에 포함되어 있는지 여부. 그렇지 않으면 *schema_name.object_name*과 같이 두 부분으로 구성된 형식을 사용하여 개체를 지정해야 합니다. 스칼라 반환 함수는 항상 두 부분 이상으로 구성된 이름을 사용하여 호출해야 합니다.  
  
-   데이터베이스 데이터 정렬의 대/소문자 구분.  
  
     데이터베이스에서 대/소문자 구분 데이터 정렬을 사용하면 개체 이름과 데이터베이스 개체의 대/소문자가 일치해야 합니다. 예를 들어 대/소문자 구분 데이터 정렬을 사용하는 데이터베이스에서 개체가 **MyTable**로 지정된 경우 개체를 **mytable** 또는 **Mytable**로 지칭하는 쿼리는 개체 이름이 일치하지 않으므로 208 오류를 반환하게 됩니다.  
  
     다음 문을 실행하여 데이터베이스 데이터 정렬을 확인할 수 있습니다.  
  
    ```  
    SELECT collation_name FROM sys.databases WHERE name = 'database_name';  
    ```  
  
     데이터 정렬 이름의 약어 CS는 해당 데이터 정렬에서 대/소문자를 구분한다는 의미입니다. 예를 들어 Latin1_General_CS_AS는 대/소문자와 악센트를 구분하는 데이터 정렬입니다. CI는 대/소문자를 구분하지 않는 데이터 정렬을 나타냅니다.  
  
-   사용자에게 개체에 액세스할 수 있는 권한이 있는지 여부. 사용자의 개체 사용 권한을 확인하려면 **Has_Perms_By_Name** 시스템 함수를 사용하세요.  
  
## <a name="see-also"></a>관련 항목  
 [USE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql)   
 [메타 데이터 표시 유형 구성](../security/metadata-visibility-configuration.md)   
 [HAS_PERMS_BY_NAME&#40;Transact-SQL&#41;](/sql/t-sql/functions/has-perms-by-name-transact-sql)  
  
  
