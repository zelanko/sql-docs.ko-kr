---
title: 결과 집합을 SQL 실행 태스크의 변수에 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- result sets [Integration Services]
- mapping result sets to variables [Integration Services]
- variables [Integration Services], mapping result sets to
ms.assetid: f76738b6-dc75-4ff9-a3dd-8b083d8e410e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 995afe55c1cd1b7d925c9267ba5dfa3aed038358
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66057755"
---
# <a name="map-result-sets-to-variables-in-an-execute-sql-task"></a>결과 집합을 SQL 실행 태스크의 변수에 매핑
  이 항목에서는 결과 집합과 SQL 실행 태스크의 변수 간 매핑을 만드는 방법에 대해 설명합니다. 결과 집합을 변수에 매핑하면 결과 집합을 패키지의 다른 요소에서 사용할 수 있습니다. 예를 들어 스크립트 태스크의 스크립트는 변수를 읽은 다음 결과 집합의 값을 사용할 수 있으며 XML 원본은 변수에 저장된 결과 집합을 사용할 수 있습니다. 부모 패키지에서 결과 집합을 생성하는 경우 결과 집합을 부모 패키지의 변수에 매핑한 다음 부모 변수 값을 저장할 자식 패키지의 부모 패키지 변수 구성을 만들어 패키지 실행 태스크로 호출하는 자식 패키지에서 결과 집합을 사용할 수 있습니다.  
  
 다양한 결과 집합 형식과 결과 집합에 매핑할 수 있는 변수 데이터 형식에 대한 설명은 [SQL 실행 태스크의 결과 집합](control-flow/execute-sql-task.md)을 참조하세요.  
  
### <a name="to-map-a-result-set-to-a-variable"></a>결과 집합을 변수에 매핑하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  **솔루션 탐색기**에서 패키지를 두 번 클릭 하 여 엽니다.  
  
3.  **제어 흐름** 탭을 클릭합니다.  
  
4.  패키지에 아직 SQL 실행 태스크가 포함되어 있지 않으면 패키지의 제어 흐름에 해당 작업을 추가합니다. 자세한 내용은 [제어 흐름에서 태스크 또는 컨테이너 추가 또는 삭제](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md) 를 참조 하세요.  
  .  
  
5.  SQL 실행 태스크를 두 번 클릭합니다.  
  
6.  **SQL 실행 태스크 편집기** 대화 상자의 **일반** 페이지에서 **단일 행**, **전체 결과 집합**또는 **XML** 결과 집합 형식을 선택합니다.  
  
     다양한 결과 집합에 대한 설명은 [SQL 실행 태스크의 결과 집합](result-sets-in-the-execute-sql-task.md)을 참조하세요.  
  
7.  **결과 집합**을 클릭합니다.  
  
8.  결과 집합 매핑을 추가하려면 **추가**를 클릭합니다.  
  
9. **변수 이름** 목록에서 변수를 선택하거나 새 변수를 만듭니다. 자세한 내용은 [패키지에서 사용자 정의 변수의 범위 추가, 삭제, 변경](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)을 참조하세요.  
  
     다양한 결과 집합에 매핑할 수 있는 변수 데이터 형식에 대한 설명은 [SQL 실행 태스크의 결과 집합](result-sets-in-the-execute-sql-task.md)을 참조하세요.  
  
     하나의 변수를 단일 열에 매핑하는 방법과 여러 변수를 여러 열에 매핑하는 방법은 **Result Sets in the Execute SQL Task** 의 [결과 집합으로 변수 채우기](control-flow/execute-sql-task.md)를 참조하십시오.  
  
10. 필요에 따라 **결과 이름** 목록에서 결과 집합의 이름을 수정합니다.  
  
     일반적으로 열 이름을 결과 집합 이름으로 사용하거나 열 목록의 열 서수 위치를 결과 집합으로 사용할 수 있습니다. 열 이름을 결과 집합 이름으로 사용하는 기능은 태스크에서 사용하도록 구성된 공급자에 따라 달라집니다. 일부 공급자만 열 이름을 사용할 수 있습니다.  
  
11. **확인**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL 실행 태스크](control-flow/execute-sql-task.md)   
 [SQL 실행 태스크의 결과 집합](result-sets-in-the-execute-sql-task.md)   
 [패키지 실행 태스크](control-flow/execute-package-task.md)   
 [패키지 구성](../../2014/integration-services/package-configurations.md)   
 [패키지 구성 만들기](../../2014/integration-services/create-package-configurations.md)   
 [자식 패키지에서 변수 및 매개 변수의 값 사용](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)   
 [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md)  
  
  
