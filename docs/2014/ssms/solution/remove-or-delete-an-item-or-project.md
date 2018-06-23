---
title: 항목이나 프로젝트 제거 또는 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- deleting project items
- projects [SQL Server Management Studio], item removal
- removing project items
ms.assetid: 3fd92434-70f5-466e-bef0-7e0fd73ddb1c
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7834be297cef98d18f78d74999750bf347454bb9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182691"
---
# <a name="remove-or-delete-an-item-or-project"></a>항목이나 프로젝트 제거 또는 삭제
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 프로젝트의 프로젝트 항목은 쿼리, 연결 및 기타 파일입니다. 저장소에서 파일을 지우지 않고 솔루션에서 프로젝트 쿼리 및 기타 파일을 제거할 수 있습니다. 프로젝트 또는 항목이 현재 솔루션에는 유용하지 않지만 다른 솔루션에 포함하려는 경우 해당 프로젝트 또는 항목을 제거합니다.  
  
### <a name="to-remove-a-project-item"></a>프로젝트 항목을 제거하려면  
  
1.  솔루션 탐색기에서 제거할 프로젝트 항목을 선택합니다.  
  
2.  **편집** 메뉴에서 **제거**를 클릭합니다.  
  
3.  확인 대화 상자에서 **제거** 를 클릭하여 프로젝트에서 항목을 제거합니다.  
  
 제거된 항목은 계속 파일 시스템에 존재합니다. 따라서 제거된 항목을 원본 솔루션이나 다른 솔루션에 추가할 수 있습니다.  
  
#### <a name="to-remove-a-project"></a>프로젝트를 제거하려면  
  
1.  솔루션 탐색기에서 제거할 프로젝트를 선택합니다.  
  
2.  **편집** 메뉴에서 **제거**를 클릭합니다.  
  
3.  확인 대화 상자에서 **확인**을 클릭하여 솔루션에서 프로젝트를 제거합니다.  
  
 프로젝트를 영구히 삭제할 수 있지만 그러기 위해서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 솔루션에서 프로젝트에 대한 참조를 먼저 제거한 다음 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Widows 탐색기를 사용하여 연결된 파일을 저장소에서 영구히 삭제해야 합니다.  
  
#### <a name="to-delete-a-project"></a>프로젝트를 삭제하려면  
  
1.  솔루션 탐색기에서 솔루션에서 삭제할 프로젝트를 제거합니다.  
  
2.  Windows 탐색기에서 삭제할 프로젝트 또는 항목과 연결된 파일을 찾아서 선택합니다.  
  
3.  **파일** 메뉴에서 **삭제**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [솔루션 탐색기](solution-explorer.md)   
 [프로젝트에 새 항목을 추가 합니다.](add-new-items-to-a-project.md)   
 [프로젝트에 기존 항목 추가](add-existing-items-to-a-project.md)  
  
  