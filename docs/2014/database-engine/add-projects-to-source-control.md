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
ms.topic: conceptual
helpviewer_keywords:
- adding projects
- projects [SQL Server Management Studio], adding
ms.assetid: fd4616b2-a564-4a66-ac53-d1f5cba213c2
caps.latest.revision: 27
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f2fc1ae6eadef04ee183e5551a88ed480a696cf2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37148274"
---
# <a name="add-projects-to-source-control"></a>원본 제어에 프로젝트 추가
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 솔루션은 여러 스크립트 프로젝트를 호스팅할 수 있습니다. 프로젝트를 원본 제어에 추가하는 방법은 프로젝트가 속하는 솔루션이 원본 제어에서 사용 중인지 여부에 따라 다릅니다. 솔루션이 원본 제어에서 사용 중일 경우 솔루션을 체크 인하면 프로젝트가 원본 제어에 자동으로 추가됩니다. 솔루션에서 확인 하는 방법에 대 한 자세한 내용은 참조 하세요. [파일에서 확인](../../2014/database-engine/check-in-files.md)합니다.  
  
 이 프로젝트가 속하는 솔루션이 원본 제어에서 사용 중이 아니면 해당 솔루션을 원본 제어에 추가할 수 있습니다. 이렇게 하면 솔루션의 프로젝트가 자동으로 추가됩니다. 소스 제어에 솔루션을 추가 하는 방법에 대 한 자세한 내용은 참조 하세요. [소스 제어에 솔루션 추가](../../2014/database-engine/add-solutions-to-source-control.md)합니다.  
  
 소스 제어에 솔루션을 추가 하려면 사용할 수는 **소스 제어에 추가 선택** 프로젝트를 수동으로 추가 하는 명령입니다.  
  
 데이터베이스 개체는 원본 제어 공급자가 직접 보호하지 않지만 데이터베이스 개체의 스크립트를 만들어 원본 제어 하에 저장할 수 있습니다.  
  
### <a name="to-add-a-project-to-source-control"></a>원본 제어에 프로젝트를 추가하려면  
  
1.  솔루션 탐색기에서 프로젝트를 선택합니다.  
  
2.  에 **파일** 메뉴에서 **소스 제어**를 클릭 하 고 **소스 제어에 선택한 프로젝트 추가**합니다.  
  
    > [!NOTE]  
    >  사용 하는 경우는 **소스 제어에 선택한 프로젝트 추가** 소스 제어 솔루션에 속하는 프로젝트를 추가 하는 명령, 소스 제어 솔루션의 하위 프로젝트를 추가 하거나 추가할 것인지 묻는 별도 폴더와 프로젝트입니다.  
  
3.  로그온하라는 메시지가 표시되면 원본 제어 공급자에 로그온합니다.  
  
4.  합니다 **SourceSafe 프로젝트에 추가** 대화 상자가 나타납니다. 프로젝트의 이름을 표시 합니다 **프로젝트** 상자입니다.  
  
5.  에 **폴더** 목록에서 프로젝트를 저장할 폴더를 엽니다. 를 클릭할 수 있습니다 **만들기** 에 표시 이름을 사용 하 여 폴더를 만들어 합니다 **프로젝트** 상자입니다.  
  
## <a name="see-also"></a>관련 항목  
 [원본 제어에 솔루션 및 프로젝트 추가](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)  
  
  
