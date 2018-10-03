---
title: 템플릿을 사용하여 스크립트 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: ed48014c-3fc9-48ff-8c0f-8d1822195f14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8387cdaf85d6fd7750229fda86c8cb3122b61d90
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227073"
---
# <a name="create-scripts-using-templates"></a>템플릿을 사용하여 스크립트 만들기
  Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서는 많은 일반 태스크에 사용할 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 포함하는 스크립트 템플릿을 다수 제공합니다. 이러한 템플릿에는 테이블 이름과 같이 사용자가 제공한 값에 대한 매개 변수가 포함됩니다. 매개 변수를 사용하면 이름을 한 번 입력한 다음 스크립트 내에서 필요한 모든 위치에 자동으로 복사할 수 있습니다. 사용자 지정 템플릿을 직접 작성하여 가장 자주 작성하는 스크립트를 지원할 수 있습니다. 템플릿을 이동하거나 템플릿을 보관할 새 폴더를 만들어 템플릿 트리를 다시 구성할 수도 있습니다. 다음 연습에서는 데이터 정렬 템플릿을 지정하여 템플릿으로 데이터베이스를 만듭니다.  
  
## <a name="using-templates"></a>템플릿 사용  
  
#### <a name="to-create-a-script-using-a-template"></a>템플릿을 사용하여 스크립트를 만들려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 **보기** 메뉴에서 **템플릿 탐색기**를 클릭합니다.  
  
2.  템플릿 탐색기에 있는 템플릿이 그룹으로 구성됩니다. **데이터베이스**를 확장한 다음 **데이터베이스 만들기**를 두 번 클릭합니다.  
  
3.  **데이터베이스 엔진에 연결** 대화 상자에서 연결 정보를 지정한 다음 **연결**을 클릭합니다. **데이터베이스 만들기** 템플릿의 내용을 포함하는 새 쿼리 편집기 창이 열립니다.  
  
4.  **쿼리** 메뉴에서 **템플릿 매개 변수 값 지정**을 클릭합니다.  
  
5.  **템플릿 매개 변수 값 지정** 대화 상자의 **값** 열에는 **Database_Name** 매개 변수에 대해 제안된 값이 포함되어 있습니다. **Database Name** 매개 변수 상자에 **Marketing**을 입력한 다음 **확인**을 클릭합니다. "Marketing"이 어떻게 스크립트의 여러 위치에 삽입되는지 확인합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [사용자 지정 템플릿 만들기](lesson-3-2-create-custom-templates.md)  
  
  
