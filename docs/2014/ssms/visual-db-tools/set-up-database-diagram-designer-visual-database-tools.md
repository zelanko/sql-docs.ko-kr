---
title: 데이터베이스 다이어그램 디자이너 설정(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.diagnostic.InstallSqlDiagramSupport
helpviewer_keywords:
- Database Diagram Designer
- database diagrams [SQL Server], Database Diagram Designer
- diagrams [SQL Server], Database Diagram Designer
ms.assetid: 927321ee-b459-4f5b-9719-4a7a95639143
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d71ea2d6a10755ef52e0cac37ddcd2385d82d9cb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63067623"
---
# <a name="set-up-database-diagram-designer-visual-database-tools"></a>데이터베이스 다이어그램 디자이너 설정(Visual Database Tools)
  데이터베이스 다이어그램 디자이너를 사용하려면 먼저 **db_owner** 역할의 멤버가 이 디자이너를 설정하여 다이어그램에 대한 액세스를 제어해야 합니다.  
  
### <a name="to-set-up-database-diagramming"></a>데이터베이스 다이어그램을 설정하려면  
  
1.  개체 탐색기에서 데이터베이스 노드를 확장합니다.  
  
2.  데이터베이스 연결 아래에서 데이터베이스 다이어그램 노드를 확장합니다.  
  
3.  데이터베이스 다이어그램을 설정할지 묻는 메시지가 나타나면 **예** 를 선택합니다.  
  
    > [!NOTE]  
    >  이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 데이터베이스 다이어그램 테이블, 시스템 저장 프로시저 및 시스템 함수가 생성됩니다.  
  
4.  Visual Studio는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 다음 개체를 만듭니다.  
  
    1.  sysdiagrams 테이블  
  
    2.  sp_alterdiagram 저장 프로시저  
  
    3.  sp_creatediagram 저장 프로시저  
  
    4.  sp_dropdiagram 저장 프로시저  
  
    5.  sp_renamediagram 저장 프로시저  
  
    6.  fn_diagramobjects 함수  
  
    7.  sp_helpdiagrams 저장 프로시저  
  
    8.  sp_helpdiagramsdefinition 저장 프로시저  
  
    9. sp_upgraddiagrams 저장 프로시저  
  
## <a name="see-also"></a>참고 항목  
 [Visual Database Tools를 &#40;데이터베이스 다이어그램 소유권 이해&#41;](visual-database-tools.md)   
 [Visual Database Tools&#41;&#40;이전 버전에서 데이터베이스 다이어그램 업그레이드](upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-authorization-transact-sql)  
  
  
