---
title: 소스 제어에 프로젝트 추가 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- adding projects
- projects [SQL Server Management Studio], adding
ms.assetid: fd4616b2-a564-4a66-ac53-d1f5cba213c2
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3f0c63dec978d50ef8544c86c6cc4811f55ef195
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185050"
---
# <a name="add-projects-to-source-control"></a>원본 제어에 프로젝트 추가
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 솔루션은 여러 스크립트 프로젝트를 호스팅할 수 있습니다. 프로젝트를 원본 제어에 추가하는 방법은 프로젝트가 속하는 솔루션이 원본 제어에서 사용 중인지 여부에 따라 다릅니다. 솔루션이 원본 제어에서 사용 중일 경우 솔루션을 체크 인하면 프로젝트가 원본 제어에 자동으로 추가됩니다. 솔루션을 체크 인하에서는 방법에 대 한 자세한 내용은 참조 [파일 체크 인](../../2014/database-engine/check-in-files.md)합니다.  
  
 이 프로젝트가 속하는 솔루션이 원본 제어에서 사용 중이 아니면 해당 솔루션을 원본 제어에 추가할 수 있습니다. 이렇게 하면 솔루션의 프로젝트가 자동으로 추가됩니다. 소스 제어에 솔루션을 추가 하는 방법에 대 한 자세한 내용은 참조 [소스 제어에 솔루션 추가](../../2014/database-engine/add-solutions-to-source-control.md)합니다.  
  
 소스 제어에 솔루션을 추가 하지 않을 경우 사용할 수 있습니다는 **소스 제어에 추가 선택** 프로젝트를 수동으로 추가 하려면 명령입니다.  
  
 데이터베이스 개체는 원본 제어 공급자가 직접 보호하지 않지만 데이터베이스 개체의 스크립트를 만들어 원본 제어 하에 저장할 수 있습니다.  
  
### <a name="to-add-a-project-to-source-control"></a>원본 제어에 프로젝트를 추가하려면  
  
1.  솔루션 탐색기에서 프로젝트를 선택합니다.  
  
2.  에 **파일** 메뉴에서 **소스 제어**, 클릭 하 고 **소스 제어에 선택한 프로젝트 추가**합니다.  
  
    > [!NOTE]  
    >  사용 하는 경우는 **소스 제어에 선택한 프로젝트 추가** 소스 제어에서 솔루션에 속해 있는 프로젝트를 추가 하려면 명령에서 소스 제어에서 솔루션의 하위 프로젝트를 추가 하거나 추가 하려면 할지 여부를 묻는 메시지가 표시 별도 폴더와 프로젝트입니다.  
  
3.  로그온하라는 메시지가 표시되면 원본 제어 공급자에 로그온합니다.  
  
4.  **SourceSafe 프로젝트에 추가** 대화 상자가 나타납니다. 프로젝트의 이름에 표시 된 **프로젝트** 상자입니다.  
  
5.  에 **폴더** 목록에서 프로젝트를 저장할 폴더를 엽니다. 클릭 수 있습니다 **만들기** 에 표시 된 이름의 폴더를 만들려고는 **프로젝트** 상자입니다.  
  
## <a name="see-also"></a>관련 항목  
 [원본 제어에 솔루션 및 프로젝트 추가](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)  
  
  