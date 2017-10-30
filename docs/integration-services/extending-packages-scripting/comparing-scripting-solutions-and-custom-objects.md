---
title: "스크립팅 솔루션과 사용자 지정 개체를 비교 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- managed tasks [Integration Services]
- Script task [Integration Services], vs. custom managed tasks
- SSIS Script task, vs. custom managed tasks
- custom tasks [Integration Services], scripts
ms.assetid: c0aea822-a21e-44e1-a3d3-8777bd0a1c34
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8d0d387c56513475df9764b0c11f2e8bdb8ed728
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="comparing-scripting-solutions-and-custom-objects"></a>스크립팅 솔루션과 사용자 지정 개체 비교
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 스크립트 태스크 또는 스크립트 구성 요소에서는 관리되는 사용자 지정 태스크 또는 데이터 흐름 구성 요소에서 사용할 수 있는 기능의 대부분을 구현할 수 있습니다. 다음은 개발자의 요구 사항에 적합한 태스크 유형을 선택할 때 고려할 사항입니다.  
  
-   구성 또는 기능이 개별 패키지에 고유한 경우 사용자 지정 개체를 개발하는 대신 스크립트 태스크나 스크립트 구성 요소를 만들어야 합니다.  
  
-   기능이 일반적이고 나중에 다른 패키지에서 사용하거나 다른 개발자가 사용할 수도 있는 경우 스크립팅 솔루션을 사용하는 대신 사용자 지정 개체를 만들어야 합니다. 사용자 지정 개체는 모든 패키지에서 사용할 수 있는 반면 스크립트는 해당 스크립트가 만들어진 패키지에서만 사용할 수 있습니다.  
  
-   동일한 패키지 내에서 코드를 다시 사용하려는 경우 사용자 지정 개체를 만드는 것이 좋습니다. 스크립트 태스크나 구성 요소 간에 코드를 복사하면 코드의 여러 복사본을 관리 및 업데이트하기가 어려워지므로 유지 관리 성능이 떨어집니다.  
  
-   시간이 경과하면서 구현이 변경될 경우 사용자 지정 개체를 사용하는 것이 좋습니다. 사용자 지정 개체는 부모 패키지와는 별도로 개발 및 배포할 수 있는 반면, 스크립팅 솔루션은 업데이트할 경우 패키지 전체를 다시 배포해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [사용자 지정 개체를 사용한 패키지 확장](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
  
  

