---
title: 데이터베이스 다이어그램 소유권 이해(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.diagnostic.CannotOpenWithInvalidOwner
helpviewer_keywords:
- diagrams [SQL Server], ownership
- database diagrams [SQL Server], ownership
- owners [SQL Server], database diagrams
ms.assetid: 4a27a48e-c4ef-4017-82b8-0cac4d0bbcac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6056a5136d8aceab338a18b32ecfac35a1af0364
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63204702"
---
# <a name="understand-database-diagram-ownership-visual-database-tools"></a>데이터베이스 다이어그램 소유권 이해(Visual Database Tools)
  데이터베이스 다이어그램 디자이너를 사용하려면 먼저 db_owner 역할([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 역할)의 멤버로 설정하여 다이어그램에 대한 액세스를 제어해야 합니다. 각 다이어그램에는 반드시 한 명의 소유자(다이어그램을 만든 사용자)가 있어야 합니다. 다이어그램을 설정 하는 방법은 참조 하세요 [데이터베이스 다이어그램 디자이너 설정 &#40;Visual Database Tools&#41;](visual-database-tools.md)합니다.  
  
 다이어그램 소유권과 관련하여 유의할 점은 다음과 같습니다.  
  
-   데이터베이스에 대한 액세스 권한이 있는 사용자는 누구든지 다이어그램을 만들 수 있지만, 일단 작성된 다이어그램은 db_owner 역할의 멤버와 다이어그램 작성자만 볼 수 있습니다.  
  
-   다이어그램의 소유권은 db_owner 역할이 있는 멤버에게만 전달할 수 있습니다. 다이어그램 소유권을 전달하려면 이전 소유자가 데이터베이스에서 제거된 상태여야 합니다.  
  
-   다이어그램의 소유자가 데이터베이스에서 제거된 후에도 db_owner 역할을 가진 멤버가 해당 다이어그램을 열려고 시도할 때까지 이 다이어그램은 데이터베이스에 유지됩니다. db_owner 멤버는 이러한 다이어그램을 열려고 시도할 때 다이어그램의 소유권을 계승할지 여부를 선택할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 다이어그램 작업 &#40;Visual Database Tools&#41;](work-with-database-diagrams-visual-database-tools.md)   
 [데이터베이스 다이어그램 디자이너 설정&#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
