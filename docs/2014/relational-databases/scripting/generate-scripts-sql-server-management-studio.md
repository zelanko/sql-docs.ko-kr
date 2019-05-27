---
title: 스크립트 생성(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 9711c617-3c68-4e5a-aea3-befc64d51524
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8aa65678c9604cac609ca1a914e542724d354872
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090359"
---
# <a name="generate-scripts-sql-server-management-studio"></a>스크립트 생성(SQL Server Management Studio)
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 생성하는 두 가지 메커니즘을 제공합니다. **스크립트 생성 및 게시 마법사**를 사용하여 여러 개체에 대한 스크립트를 만들 수 있습니다. 또한 **개체 탐색기** 에서 **스크립팅**메뉴를 사용하여 개별 개체 또는 여러 개체에 대한 스크립트를 생성할 수도 있습니다.  
  
1.  **메서드를 선택 합니다.**  [생성 및 게시 스크립트 마법사](#GenPubScriptWiz), [개체 탐색기 스크립팅 메뉴](#OEScriptAsMenu)  
  
2.  **스크립트를 메뉴로 사용:**  [단일 개체 스크립팅](#ScriptSingleObject)하십시오 [개체 탐색기를 사용 하 여 두 개체 스크립팅](#ScriptTwoObjectsOE), [개체 탐색기 정보를 사용 하 여 두 개체 스크립팅](#ScriptTwoObjectsOED)  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
 요구 사항에 가장 적합한 메커니즘을 선택합니다.  
  
###  <a name="GenPubScriptWiz"></a> 스크립트 생성 및 게시 마법사  
 **스크립트 생성 및 게시 마법사** 를 사용하여 다양한 개체에 대한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 만들 수 있습니다. 이 마법사는 데이터베이스의 모든 개체 또는 사용자가 선택한 개체의 하위 집합에 대한 스크립트를 생성합니다. 이 마법사에는 사용 권한, 데이터 정렬, 제약 조건 등을 포함할지 여부와 같은 여러 스크립트 옵션이 있습니다. 마법사를 사용하는 방법은 [Generate and Publish Scripts Wizard](generate-and-publish-scripts-wizard.md)를 참조하십시오.  
  
###  <a name="OEScriptAsMenu"></a> 개체 탐색기 스크립팅 메뉴  
 **개체 탐색기 스크립팅** 메뉴를 사용하여 단일 개체, 여러 개체 또는 단일 개체에 대한 여러 문을 스크립팅할 수 있습니다. 여러 스크립트 유형 중 하나를 선택할 수 있습니다. 예를 들어 개체를 만들거나 변경하거나 삭제할 수 있습니다. 쿼리 편집기 창의 스크립트를 파일이나 클립보드에 저장할 수 있습니다. 스크립트는 유니코드 형식으로 만들어집니다.  
  
##  <a name="ScriptSingleObject"></a> 단일 개체의 스크립트를 생성하려면  
 **단일 개체를 스크립팅하려면**  
  
1.  개체 탐색기에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장한 다음 스크립팅할 개체가 포함된 데이터베이스를 확장합니다.  
  
3.  개체의 범주를 확장합니다. 예를 들어 **테이블** 또는 **뷰** 노드를 확장합니다.  
  
4.  개체를 마우스 오른쪽으로 클릭하여 **\<개체 유형> 스크립팅**을 가리킵니다. 예를 들어 **테이블 스크립팅**을 가리킵니다.  
  
5.  스크립트 유형을 가리킵니다(예: **CREATE** 또는 **ALTER**).  
  
6.  스크립트를 저장할 위치를 선택합니다(예: **새 쿼리 편집기 창** 또는 **클립보드**).  
  
##  <a name="ScriptTwoObjectsOE"></a> 개체 탐색기를 사용하여 두 개체에 대한 스크립트를 생성하려면  
 **개체 탐색기를 사용하여 두 개체를 스크립팅하려면**  
  
 프로시저를 삭제한 다음 프로시저를 만들거나 테이블을 만든 다음 테이블을 변경하는 등 여러 옵션이 있는 스크립트가 필요한 경우가 있습니다. 아래의 여러 개체에 대한 스크립트 생성 프로세스는 테이블, 뷰, 저장 프로시저 등 여러 개체 유형을 참조하는 스크립트를 만들어야 하는 경우에도 작동합니다.  
  
1.  개체 탐색기에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장한 다음 스크립팅할 개체가 포함된 데이터베이스를 확장합니다.  
  
3.  스크립팅할 첫 번째 개체를 마우스 오른쪽 단추로 클릭하고 **\<개체 유형> 스크립팅**을 가리키고 **다른 이름으로 저장** 선택 항목에서 **새 쿼리 편집기 창**을 출력 대상으로 선택합니다.  
  
4.  스크립팅할 두 번째 개체를 찾습니다.  
  
5.  개체를 마우스 오른쪽 단추로 클릭하고 **\<개체 유형> 스크립팅**을 가리키고 **다른 이름으로 저장** 선택 항목에서 **클립보드**를 출력 대상으로 선택합니다.  
  
6.  첫 번째 개체에 대해 열린 쿼리 편집기 창에서 클립보드에 저장된 두 번째 개체에 대한 스크립트를 붙여 넣습니다.  
  
##  <a name="ScriptTwoObjectsOED"></a> 개체 탐색기 정보를 사용하여 두 개체에 대한 스크립트를 생성하려면  
 **개체 탐색기 정보를 사용하여 두 개체를 스크립팅하려면**  
  
 **개체 탐색기 정보** 창을 사용하여 동일한 범주의 여러 개체에 대한 스크립트를 생성할 수 있습니다.  
  
1.  개체 탐색기에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **데이터베이스**를 확장한 다음 스크립팅할 개체가 포함된 데이터베이스를 확장합니다.  
  
3.  스크립팅할 개체 유형의 범주 노드(예: **테이블** 노드)로 이동합니다.  
  
4.  **F7** 을 선택하거나 **보기**메뉴를 열고 **개체 탐색기 정보** 를 선택하여 **개체 탐색기 정보**창을 엽니다.  
  
5.  스크립팅할 개체 중 하나를 마우스 왼쪽 단추로 클릭합니다.  
  
6.  Crtl 키를 누른 채로 스크립팅할 두 번째 개체를 마우스 왼쪽 단추로 클릭합니다.  
  
7.  선택된 개체 중 하나를 마우스 오른쪽 단추로 클릭하고 **\<개체 유형> 스크립팅**을 선택합니다.  
  
  
