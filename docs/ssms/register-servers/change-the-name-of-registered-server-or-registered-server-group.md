---
title: "등록된 서버 또는 등록된 서버 그룹 이름 변경 | Microsoft Docs"
ms.custom: 
ms.date: 08/02/2016
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-registration
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying registered server or server group names
- server groups [SQL Server]
- Registered Servers [SQL Server], names
- renaming registered server or server group
- names [SQL Server], registered server or server group
ms.assetid: 10e1546b-9edb-400c-8676-2ea1192d6134
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 76b0c8fb0f6ef95348200c04c65b6c3838c33d80
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="change-the-name-of-registered-server-or-registered-server-group"></a>등록된 서버 또는 등록된 서버 그룹 이름 변경
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 등록된 서버 또는 서버 그룹의 이름을 변경하는 방법에 대해 설명합니다. 이 이름은 언제든지 변경할 수 있습니다. 등록된 서버의 서버 이름을 변경하면 이름이 표시되는 방식만 변경됩니다. 다른 서버에 연결하려면 등록된 서버의 연결 속성을 편집해야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
메뉴에서 **보기\\등록된 서버**로 이동하여 **등록된 서버** 창을 엽니다.  
#### <a name="to-change-the-name-of-a-server"></a>서버 이름을 변경하려면  
  
1.  **등록된 서버**에서 **데이터베이스 엔진** , **로컬 서버 그룹**을 차례로 확장합니다.  

2.  서버를 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택한 다음 **서버 등록 속성 편집** 대화 상자 창을 엽니다.
  
3.  **등록된 서버 이름** 입력란에 서버 등록을 위해 새 이름을 입력한 다음 **저장**을 클릭합니다.  
  
#### <a name="to-change-the-name-of-a-server-group"></a>서버 그룹의 이름을 변경하려면  
  
1.  **등록된 서버**에서 **데이터베이스 엔진** , **로컬 서버 그룹**을 차례로 확장합니다.  

2.  서버 그룹을 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택한 다음 **서버 그룹 속성 편집** 대화 상자 창을 엽니다. 
  
3.  **그룹 이름** 입력란에 서버 그룹의 새 이름을 입력한 다음 **저장**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [서버 등록 변경&#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/change-a-server-s-registration-sql-server-management-studio.md)  
  
  
