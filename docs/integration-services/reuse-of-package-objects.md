---
title: "패키지 개체 다시 사용 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- GUID regenerating [Integration Services]
- reusing packages
- templates [Integration Services]
- copying packages
- regenerating package GUID
ms.assetid: 08f723bf-15b5-44bd-9a46-04e8781bfbfb
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 31653debba3400f6a5f3a5b23474bd3055e02522
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="reuse-of-package-objects"></a>패키지 개체 다시 사용
  다시 사용하려는 자주 사용되는 패키지 기능입니다. 예를 들어 태스크 집합을 만든 경우 항목을 모두 그룹으로 다시 사용하거나 다른 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트에서 만든 연결 관리자와 같은 단일 항목을 다시 사용하려고 할 수 있습니다.  
  
## <a name="copy-and-paste"></a>복사 및 붙여넣기  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 및 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너는 패키지 개체 복사 및 붙여넣기를 지원합니다. 여기에는 제어 흐름 항목, 데이터 흐름 항목 및 연결 관리자가 포함될 수 있습니다. 프로젝트 간 및 패키지 간에 복사하여 붙여 넣을 수 있습니다. 솔루션에 여러 개의 프로젝트가 포함된 경우 프로젝트 간에 복사할 수 있으며 프로젝트는 다른 유형일 수 있습니다.  
  
 솔루션에 여러 개의 패키지가 포함된 경우 해당 패키지 간에 복사하고 붙여 넣을 수 있습니다. 패키지는 같은 프로젝트나 다른 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트에 있을 수 있습니다. 그러나 유효성 여부에 관계없이 패키지 개체에 다른 개체에 대한 종속성이 있을 수 있습니다. 예를 들어 SQL 실행 태스크에는 연결 관리자를 사용하고 태스크가 작동하도록 이를 복사해야 합니다. 또한 일부 패키지 개체는 패키지에 특정 개체를 포함해야 하며 이 개체가 없으면 복사한 개체를 패키지에 성공적으로 붙여 넣을 수 없습니다. 예를 들면 데이터 흐름 태스크가 없는 패키지에 데이터 흐름을 붙여 넣을 수 없습니다.  
  
 같은 패키지를 반복해서 복사할 수 있습니다. 복사 프로세스가 수행되지 않도록 하려면 이러한 패키지를 템플릿으로 지정하고 새 패키지를 만들 때 이러한 패키지를 템플릿으로 사용합니다.  
  
 패키지 개체를 복사하면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 자동으로 새 GUID를 새 개체의 **ID** 속성에 할당하고 **Name** 속성을 업데이트합니다.  
  
 변수는 복사할 수 없습니다. 태스크와 같은 개체에서 변수를 사용하는 경우 대상 패키지에 변수를 다시 만들어야 합니다. 반대로 전체 패키지를 복사하는 경우 패키지의 변수도 복사됩니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [패키지 개체 복사](../integration-services/copy-package-objects.md)  
  
-   [프로젝트 항목 복사](http://msdn.microsoft.com/library/1606c54d-20f9-49f3-a4ef-caad83a772aa)  
  
-   [패키지 템플릿으로 패키지 저장](http://msdn.microsoft.com/library/efe66cec-3933-4f6e-8d35-fe3d300de66c)  
  
  
