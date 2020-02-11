---
title: 모든 이벤트에 대 한 필드 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], getting fields
- xe
ms.assetid: 4e4ee03f-5bca-42ed-a37c-db1c82e3aad2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0838367ad699c1278bb6ec42f28161ba76c6fd5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66064785"
---
# <a name="get-the-fields-for-all-events"></a>모든 이벤트에 대한 필드 가져오기
  이 태스크를 수행하려면 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 쿼리 편집기를 사용합니다.  
  
 이 프로시저의 문이 끝나면 쿼리 편집기의 **결과** 탭에 다음 열이 표시됩니다.  
  
-   package_name  
  
-   event_name  
  
-   event_field  
  
-   field_type  
  
-   column_type  
  
 위의 정보는 버킷팅 대상을 사용하는 이벤트 세션을 구성하는 경우 사용할 수 있습니다. 자세한 내용은 [SQL Server Extended Events Targets](../../2014/database-engine/sql-server-extended-events-targets.md)을 참조하세요.  
  
## <a name="before-you-begin"></a>시작하기 전에  
 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 확장 이벤트 세션을 만들기 전에 이벤트와 연관된 필드에 대한 정보를 얻는 것이 좋습니다.  
  
## <a name="to-get-the-fields-for-all-events-using-query-editor"></a>쿼리 편집기를 사용하여 모든 이벤트에 대한 필드를 가져오려면  
  
-   쿼리 편집기에서 다음 문을 실행합니다.  
  
    ```  
    select p.name package_name, o.name event_name, c.name event_field, c.type_name field_type, c.column_type column_type  
    from sys.dm_xe_objects o  
    join sys.dm_xe_packages p  
          on o.package_guid = p.guid  
    join sys.dm_xe_object_columns c  
          on o.name = c.object_name  
    where o.object_type = 'event'  
    order by package_name, event_name  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [dm_xe_objects &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
