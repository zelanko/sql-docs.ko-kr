---
title: 예상 실행 계획 표시 | Microsoft 문서
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- zoom [SQL Server]
- estimated execution plan [SQL Server]
- displaying execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
- customizing execution plan display [SQL Server]
- modifying execution plan display
- custom zoom [SQL Server]
ms.assetid: e94aa576-4c0c-4c54-ad05-6c3432cc615b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d58470fa6427a37510f28ca1305c1ab4c7927697
ms.sourcegitcommit: ba7fb4b9b4f0dbfe77a7c6906a1fde574e5a8e1e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52302766"
---
# <a name="display-the-estimated-execution-plan"></a>예상 실행 계획 표시
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 그래픽 예상 실행 계획을 작성하는 방법에 대해 설명합니다. 예상 실행 계획이 작성되면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 또는 일괄 처리가 실행되지 않습니다. 이 때문에 예상 실행 계획에는 실제 리소스 사용량 메트릭 또는 런타임 경고와 같은 런타임 정보가 포함되지 않습니다. 대신 쿼리가 실제로 실행되었을 때 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]이 사용할 가능성이 가장 큰 쿼리 실행 계획과 계획에서 몇 가지 작업을 통과하는 예상 행 수가 생성된 실행 계획에 표시됩니다.  
  
 이 기능을 사용하려면 사용자가 그래픽 실행 계획을 생성하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 실행하기 위한 적절한 권한을 갖고 있어야 하며 쿼리가 참조하는 모든 데이터베이스에 대한 SHOWPLAN 권한이 허용되어야 합니다.  
  
## <a name="to-display-the-estimated-execution-plan-for-a-query"></a>쿼리의 예상 실행 계획을 표시하려면  
  
1.  도구 모음에서 **데이터베이스 엔진 쿼리**를 클릭합니다. **파일 열기** 도구 모음 단추를 클릭하여 기존 쿼리를 열고 예상 실행 계획을 표시할 수도 있습니다.  
  
2.  예상 실행 계획을 표시할 쿼리를 입력합니다.  
  
3.  **쿼리** 메뉴에서 **예상 실행 계획 표시** 를 클릭하거나 **예상 실행 계획 표시** 도구 모음 단추를 클릭합니다. 예상 실행 계획은 결과 창의 **실행 계획** 탭에 표시됩니다. 

    ![도구 모음에서 예상 실행 계획 단추](../../relational-databases/performance/media/estimatedexecplantoolbar.png "도구 모음에서 예상 실행 계획 단추")    

    추가 정보를 보려면 논리 및 물리 연산자 아이콘 위에 마우스를 올리고 잠시 대기하여 도구 설명을 표시하고 연산자에 대한 설명 및 속성을 확인합니다. 또는 속성 창에서 연산자 속성을 확인할 수 있습니다. 속성이 보이지 않으면 연산자를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 속성을 확인할 연산자를 선택합니다.  

    ![계획 연산자에서 속성을 마우스 오른쪽 단추로 클릭](../../relational-databases/performance/media/planproperties.png "계획 연산자에서 속성을 마우스 오른쪽 단추로 클릭")    
  
4.  실행 계획 표시 크기를 변경하려면 실행 계획을 마우스 오른쪽 단추로 클릭한 다음 실행 계획, **축소**, **확대**, **사용자 지정 확대/축소**또는 **크기에 맞게**를 선택합니다. **축소** 및 **확대** 를 사용하면 실행 계획을 고정된 크기만큼 확대 또는 축소시킬 수 있습니다. **사용자 지정 확대/축소** 를 사용하면 사용자가 원하는 표시 배율을 정의할 수 있습니다(예: 80%로 축소). **크기에 맞게** 는 결과 창에 맞게 실행 계획을 확대합니다. 또는 CTRL 키와 마우스 휠의 조합을 사용하여 **동적 확대/축소**를 활성화합니다.  

5.  실행 계획의 표시를 이동하려면 세로 및 가로 스크롤 막대를 사용하거나 실행 계획의 **빈 영역을 클릭하고 있으면서** **마우스를 끌어서 놓습니다**. 또는 실행 계획 창의 오른쪽 아래 모서리에서 더하기(+) 기호를 클릭하고 있어 전체 실행 계획의 간단한 지도를 표시합니다.
 
> [!NOTE] 
> 또는 [SET SHOWPLAN_XML](../../t-sql/statements/set-showplan-xml-transact-sql.md)을 사용하여 각 문을 실행하지 않고 실행 계획 정보만 반환합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 사용한 경우 *결과* 탭에 실행 계획을 그래픽 형식으로 여는 링크가 포함됩니다.   
