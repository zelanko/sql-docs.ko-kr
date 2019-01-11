---
title: 항목이나 프로젝트 제거 또는 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting project items
- projects [SQL Server Management Studio], item removal
- removing project items
ms.assetid: 3fd92434-70f5-466e-bef0-7e0fd73ddb1c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a94e6cf1ca6c550d2229b198fbfd18ab7d714f12
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804951"
---
# <a name="remove-or-delete-an-item-or-project"></a>항목이나 프로젝트 제거 또는 삭제
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 프로젝트의 프로젝트 항목은 쿼리, 연결 및 기타 파일입니다. 스토리지에서 파일을 지우지 않고 솔루션에서 프로젝트 쿼리 및 기타 파일을 제거할 수 있습니다. 프로젝트 또는 항목이 현재 솔루션에는 유용하지 않지만 다른 솔루션에 포함하려는 경우 해당 프로젝트 또는 항목을 제거합니다.  
  
### <a name="to-remove-a-project-item"></a>프로젝트 항목을 제거하려면  
  
1.  솔루션 탐색기에서 제거할 프로젝트 항목을 선택합니다.  
  
2.  **편집** 메뉴에서 **제거**를 클릭합니다.  
  
3.  확인 대화 상자에서 **제거** 를 클릭하여 프로젝트에서 항목을 제거합니다.  
  
제거된 항목은 계속 파일 시스템에 존재합니다. 따라서 제거된 항목을 원본 솔루션이나 다른 솔루션에 추가할 수 있습니다.  
  
#### <a name="to-remove-a-project"></a>프로젝트를 제거하려면  
  
1.  솔루션 탐색기에서 제거할 프로젝트를 선택합니다.  
  
2.  **편집** 메뉴에서 **제거**를 클릭합니다.  
  
3.  확인 대화 상자에서 **확인**을 클릭하여 솔루션에서 프로젝트를 제거합니다.  
  
프로젝트를 영구히 삭제할 수 있지만 그러기 위해서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 솔루션에서 프로젝트에 대한 참조를 먼저 제거한 다음 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Widows 탐색기를 사용하여 연결된 파일을 스토리지에서 영구히 삭제해야 합니다.  
  
#### <a name="to-delete-a-project"></a>프로젝트를 삭제하려면  
  
1.  솔루션 탐색기에서 솔루션에서 삭제할 프로젝트를 제거합니다.  
  
2.  Windows 탐색기에서 삭제할 프로젝트 또는 항목과 연결된 파일을 찾아서 선택합니다.  
  
3.  **파일** 메뉴에서 **삭제**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
[솔루션 탐색기](../../ssms/solution/solution-explorer.md)  
[프로젝트에 새 항목 추가](../../ssms/solution/add-new-items-to-a-project.md)  
[프로젝트에 기존 항목 추가](../../ssms/solution/add-existing-items-to-a-project.md)  
  
