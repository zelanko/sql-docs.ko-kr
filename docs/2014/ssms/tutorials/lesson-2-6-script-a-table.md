---
title: 테이블 스크립팅 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: ea88d736-849e-4368-b55d-06aeee097bf3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 22fae65a5e62be579f751dd3d6d3d0c9a73e7409
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63316403"
---
# <a name="script-a-table"></a>테이블 스크립팅
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서는 스크립트를 만들어 테이블을 선택, 삽입, 업데이트 및 삭제 하 고 저장 프로시저를 작성, 변경, 삭제 또는 실행할 수 있습니다.  
  
 프로시저를 삭제한 다음 프로시저를 만들거나 테이블을 만든 다음 테이블을 변경하는 등 여러 옵션이 있는 스크립트가 필요한 경우가 있습니다. 조합된 스크립트를 만들려면 첫 번째 스크립트를 쿼리 편집기 창에 저장하고 두 번째 스크립트를 클립보드에 저장하여 첫 번째 스크립트 다음에 창에 붙여 넣을 수 있습니다.  
  
## <a name="creating-an-update-script"></a>업데이트 스크립트 만들기  
  
#### <a name="to-create-the-insert-script-for-a-table"></a>테이블에 대한 삽입 스크립트를 만들려면  
  
1.  개체 탐색기에서 사용 중인 서버를 확장하고 **데이터베이스**, [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], **테이블**을 차례로 확장한 다음 **HumanResources.Employee**를 마우스 오른쪽 단추로 클릭하고 **테이블 스크립팅**을 가리킵니다.  
  
2.  바로 가기 메뉴에는 **CREATE**, **DROP**, **DROP 및 CREATE**, **SELECT**, **INSERT**, **UPDATE**및 **DELETE**의 일곱 개의 스크립트 옵션이 있습니다. 
  **UPDATE**를 가리킨 다음 **새 쿼리 편집기 창**을 클릭합니다.  
  
3.  새 쿼리 편집기 창이 열리고 연결이 설정된 다음 전체 Update 문이 표시됩니다.  
  
     이 연습에서는 스크립팅 기능으로 테이블 또는 저장 프로시저 만들기를 스크립팅하는 것 이상의 작업을 수행할 수 있는 방법을 보여 줍니다. 이 새 기능을 사용하면 프로젝트에 데이터 조작 스크립트를 빠르게 추가하고 저장 프로시저를 쉽게 실행할 수 있습니다. 테이블이나 프로시저의 필드가 많을 경우 이 새 기능으로 시간을 크게 절약할 수 있습니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [요약: Transact-SQL 작성](../../tutorials/summary-writing-transact-sql.md)  
  
  
