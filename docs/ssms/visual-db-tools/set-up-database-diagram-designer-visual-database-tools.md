---
description: 데이터베이스 다이어그램 디자이너 설정(Visual Database Tools)
title: 데이터베이스 다이어그램 디자이너 설정
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.diagnostic.InstallSqlDiagramSupport
helpviewer_keywords:
- Database Diagram Designer
- database diagrams [SQL Server], Database Diagram Designer
- diagrams [SQL Server], Database Diagram Designer
ms.assetid: 927321ee-b459-4f5b-9719-4a7a95639143
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: b993b6503f721ddfb88f2c34b09df3cc7ded0a68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417799"
---
# <a name="set-up-database-diagram-designer-visual-database-tools"></a>데이터베이스 다이어그램 디자이너 설정(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
 데이터베이스 다이어그램 디자이너를 사용하려면 먼저 **db_owner** 역할의 멤버가 이 디자이너를 설정하여 다이어그램에 대한 액세스를 제어해야 합니다.  
  
### <a name="to-set-up-database-diagramming"></a>데이터베이스 다이어그램을 설정하려면  
  
1.  개체 탐색기에서 데이터베이스 노드를 확장합니다.  
  
2.  데이터베이스 연결 아래에서 데이터베이스 다이어그램 노드를 확장합니다.  
  
3.  데이터베이스 다이어그램을 설정할지 묻는 메시지가 나타나면 **예** 를 선택합니다.  
  
    > [!NOTE]  
    > 이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 데이터베이스 다이어그램 테이블, 시스템 저장 프로시저 및 시스템 함수가 생성됩니다.  
  
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
[데이터베이스 다이어그램 소유권 이해&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/understand-database-diagram-ownership-visual-database-tools.md)  
[이전 버전에서 데이터베이스 다이어그램 업그레이드&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)  
[ALTER AUTHORIZATION(Transact-SQL)](https://msdn.microsoft.com/8c805ae2-91ed-4133-96f6-9835c908f373)  
  
