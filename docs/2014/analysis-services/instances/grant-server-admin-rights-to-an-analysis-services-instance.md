---
title: 서버 관리자 권한 부여 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- administrator rights [Analysis Services]
- server-wide administrative permissions [Analysis Services]
ms.assetid: 20d1234b-a457-4a84-ae08-fe356870c466
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4af61a59de6175d4241cb6b1b9700ff7ba816430
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37328853"
---
# <a name="grant-server-administrator-permissions-analysis-services"></a>서버 관리자 권한 부여(Analysis Services)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 내에서 서버 관리자 역할의 멤버는 해당 인스턴스의 모든 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체와 데이터에 무제한으로 액세스할 수 있습니다. 데이터베이스 작성 또는 처리, 서버 속성 수정, 추적 시작(이벤트 처리용 제외) 등의 서버 차원의 태스크를 수행하려면 사용자가 서버 관리자 역할의 멤버여야 합니다.  
  
 역할 멤버 자격은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 이 설치될 때 설정됩니다. 설치 프로그램을 실행하는 사용자는 서버를 제공할 때 본인을 역할에 추가하거나 다른 사용자를 추가할 수 있습니다. 다음 절차를 사용하여 사후 설치 태스크로 역할 멤버 자격을 수정할 수 있습니다.  
  
## <a name="modify-server-role-membership"></a>서버 역할 멤버 자격 수정  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하고 개체 탐색기에서 인스턴스 이름을 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
2.  **페이지 선택** 창에서 **보안** 을 클릭하고 페이지 맨 아래쪽에서 **추가** 를 클릭하여 서버 역할에 Windows 사용자나 그룹을 하나 이상 추가합니다.  
  
     ![Management studio에서 추가 사용자가 대화 상자](../media/ssas-serveradminadd.png "management studio에서 추가 사용자가 대화 상자")  
  
 설치 시 SQL Server 설치 프로그램에서는 적어도 하나 이상의 사용자 계정을 Analysis Services 시스템 관리자로 지정해야 합니다.  
  
 기본적으로 로컬 관리자 그룹의 멤버는 Analysis Server에서 관리 권한도 부여 받습니다. 로컬 그룹은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버 관리자 역할의 멤버 자격을 명시적으로 부여 받지는 않지만 로컬 관리자는 데이터베이스를 만들고 사용자 및 사용 권한을 추가하고 시스템 관리자에게 허용된 기타 모든 작업을 수행할 수 있습니다. 이 동작은 구성할 수 있습니다. 에 의해 결정 됩니다 합니다 `BuiltinAdminsAreServerAdmins` 로 설정 되어 있는 서버 속성 **true** 기본적으로 합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 이 속성을 변경할 수 있습니다. 자세한 내용은 [Security Properties](../server-properties/security-properties.md)을 참조하세요.  
  
 AMO(Analysis Management Objects)를 사용하여 서버 역할을 관리할 수도 있습니다. 자세한 내용은 [AMO&#40;Analysis Management Objects&#41;를 사용하여 개발](../multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [개체 및 작업에 대 한 액세스 권한 부여 &#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)   
 [보안 역할 &#40;Analysis Services-다차원 데이터&#41;](../multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)  
  
  
