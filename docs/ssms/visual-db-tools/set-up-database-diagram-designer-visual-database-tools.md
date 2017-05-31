---
title: "데이터베이스 다이어그램 디자이너 설정(Visual Database Tools) | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.diagnostic.InstallSqlDiagramSupport
helpviewer_keywords:
- Database Diagram Designer
- database diagrams [SQL Server], Database Diagram Designer
- diagrams [SQL Server], Database Diagram Designer
ms.assetid: 927321ee-b459-4f5b-9719-4a7a95639143
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9afcf20de2220aee5d9be2763a0b274ec738e48c
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="set-up-database-diagram-designer-visual-database-tools"></a>데이터베이스 다이어그램 디자이너 설정(Visual Database Tools)
데이터베이스 다이어그램 디자이너를 사용하려면 먼저 **db_owner** 역할의 멤버가 이 디자이너를 설정하여 다이어그램에 대한 액세스를 제어해야 합니다.  
  
### <a name="to-set-up-database-diagramming"></a>데이터베이스 다이어그램을 설정하려면  
  
1.  개체 탐색기에서 데이터베이스 노드를 확장합니다.  
  
2.  데이터베이스 연결 아래에서 데이터베이스 다이어그램 노드를 확장합니다.  
  
3.  데이터베이스 다이어그램을 설정할지 묻는 메시지가 나타나면 **예** 를 선택합니다.  
  
    > [!NOTE]  
    > 이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스에 데이터베이스 다이어그램 테이블, 시스템 저장 프로시저 및 시스템 함수가 생성됩니다.  
  
4.  Visual Studio는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]인스턴스에서 다음 개체를 만듭니다.  
  
    1.  sysdiagrams 테이블  
  
    2.  sp_alterdiagram 저장 프로시저  
  
    3.  sp_creatediagram 저장 프로시저  
  
    4.  sp_dropdiagram 저장 프로시저  
  
    5.  sp_renamediagram 저장 프로시저  
  
    6.  fn_diagramobjects 함수  
  
    7.  sp_helpdiagrams 저장 프로시저  
  
    8.  sp_helpdiagramsdefinition 저장 프로시저  
  
    9. sp_upgraddiagrams 저장 프로시저  
  
## <a name="see-also"></a>관련 항목:  
[데이터베이스 다이어그램 소유권 이해&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/understand-database-diagram-ownership-visual-database-tools.md)  
[이전 버전에서 데이터베이스 다이어그램 업그레이드&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)  
[ALTER AUTHORIZATION(Transact-SQL)](http://msdn.microsoft.com/en-us/8c805ae2-91ed-4133-96f6-9835c908f373)  
  

