---
title: "다중 사용자 환경(Visual Database Tools) | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- users [SQL Server], multiuser environments
- conflict resolution [Visual Database Tools]
- multiple users making database changes
- multiuser environments [Visual Database Tools]
- database modifications [SQL Server]
- version control [Visual Database Tools]
- Visual Database Tools [SQL Server], multiuser environments
ms.assetid: 330bd48c-9427-4967-b58e-b7c492d5ee36
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 856d43b504fad6aa72bf23dcfe9eff3ff6384246
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="multiuser-environments-visual-database-tools"></a>다중 사용자 환경(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 다중 사용자 환경은 작업하고 있는 동일한 데이터베이스에 다른 사용자가 연결하여 변경할 수 있는 환경입니다. 결과적으로 여러 명의 사용자가 동시에 동일한 데이터베이스 개체에서 작업할 수 있습니다. 따라서 다중 사용자 환경에서 현재 사용자가 작업 중인 데이터베이스를 다른 사용자가 변경할 수 있으며 그 반대의 경우도 가능합니다.  
  
다중 사용자 환경에서 데이터베이스로 작업할 때 가장 중요한 것은 액세스 권한입니다. 데이터베이스에 대한 권한에 따라 데이터베이스에서 작업할 수 있는 범위가 결정됩니다. 예를 들어, 데이터베이스의 개체를 변경하려면 해당 데이터베이스에 대한 적절한 쓰기 권한이 있어야 합니다. 데이터베이스의 권한에 대한 자세한 내용은 데이터베이스 설명서를 참조하십시오. 자세한 내용은 [사용 권한 및 Visual Database Tools&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/permissions-and-visual-database-tools-visual-database-tools.md)를 참조하세요.  
  
테이블의 변경 내용을 저장할 때 테이블 디자이너는 변경 내용을 마지막으로 저장한 이후 데이터베이스가 수정되지 않았는지 확인합니다. 다른 사용자가 변경한 경우 사용자는 데이터베이스가 수정되었다는 통보를 받게 됩니다. 따라서 이와 같이 충돌하는 변경 내용을 조정해야 할 수 있습니다. 자세한 내용은 [여러 사용자가 변경한 내용 조정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/reconcile-changes-made-by-multiple-users-visual-database-tools.md)을 참조하세요.  
  
다중 사용자 환경에서는 변경 내용이 충돌하는 경우를 방지하기 위해 특별히 주의해야 할 사항이 있습니다. 자세한 내용은 [데이터베이스의 단계적 개발 문제&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/issues-of-database-evolution-visual-database-tools.md)를 참조하세요.  
  
문제를 방지하기 위한 방법 중 하나로 데이터베이스의 복사본을 사용할 수 있습니다. 예를 들어, 테스트 데이터베이스 같은 복사본에 변경 작업을 수행하고 충돌 문제를 오프라인으로 해결한 다음 이러한 변경 내용을 원본 데이터베이스에서 실행하기 위한 변경 스크립트를 만들 수 있습니다. 자세한 내용은 [개발, 테스트 및 프로덕션 데이터베이스&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/development-test-and-production-databases-visual-database-tools.md)를 참조하세요.  
  
