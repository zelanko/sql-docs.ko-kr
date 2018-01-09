---
title: "AMO 보안 클래스 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Management Objects, security
- security [AMO]
- AMO, security
ms.assetid: e3d5012a-8121-40de-9244-1fc824228693
caps.latest.revision: "23"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c06206ff2d9c66230a496e49e3681edd2bb5f312
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="amo-security-classes"></a>AMO 보안 클래스
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]이 항목에는 다음 섹션이 포함 됩니다.  
  
-   [Role 및 RoleMember 개체](#RolesMembers)  
  
-   [사용 권한 개체](#Permissions)  
  
 다음 그림에서는 이 항목에 설명된 클래스의 관계를 보여 줍니다.  
  
 ![이 항목에서 amo에서 보안 클래스 설명](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-securityclasses.gif "AMO의 보안 클래스는이 항목의 내용")  
  
##  <a name="RolesMembers"></a>Role 및 RoleMember 개체  
 <xref:Microsoft.AnalysisServices.Role> 개체를 데이터베이스의 역할 컬렉션에 추가한 다음 Update 메서드를 사용하여 서버로 업데이트하면 <xref:Microsoft.AnalysisServices.Role> 개체가 만들어집니다. <xref:Microsoft.AnalysisServices.Role> 개체를 사용하려면 먼저 업데이트해야 합니다.  
  
 <xref:Microsoft.AnalysisServices.Role> 개체를 제거하려면 <xref:Microsoft.AnalysisServices.Role> 개체의 Drop 메서드를 사용하여 삭제해야 합니다. 역할 컬렉션의 Remove 메서드를 사용하더라도 역할이 서버에서 제거되지는 않습니다. 해당 역할이 응용 프로그램에 표시되지 않을 뿐입니다. <xref:Microsoft.AnalysisServices.Role> 개체에 연결된 권한이 있으면 해당 개체를 삭제할 수 없습니다.  
  
 A <xref:Microsoft.AnalysisServices.RoleMember> 사용자 역할의 멤버 컬렉션에 추가 하 고 업데이트 하 여 개체를 만듭니다는 <xref:Microsoft.AnalysisServices.Role> Update 메서드를 사용 하 여 서버에는 개체입니다. 서버 관리자 또는 데이터베이스 관리자에게만 역할을 만들 수 있는 권한이 있습니다. 먼저 <xref:Microsoft.AnalysisServices.Role> 개체를 서버로 업데이트해야 해당 멤버가 사용자에게 권한이 부여된 개체를 사용할 수 있습니다.  
  
 <xref:Microsoft.AnalysisServices.RoleMember> 개체를 제거하려면 컬렉션의 Remove 메서드를 사용하여 컬렉션에서 개체를 제거한 다음 Update 메서드를 사용하여 역할을 업데이트해야 합니다.  
  
 이러한 개체에 사용할 수 있는 메서드와 속성에 대한 자세한 내용은 <xref:Microsoft.AnalysisServices.Role>의 <xref:Microsoft.AnalysisServices.RoleMember> 및 <xref:Microsoft.AnalysisServices>를 참조하십시오.  
  
##  <a name="Permissions"></a>사용 권한 개체  
 <xref:Microsoft.AnalysisServices.Permission> 개체를 개체의 권한 컬렉션에 추가한 다음 Update 메서드를 사용하여 서버로 업데이트하면 <xref:Microsoft.AnalysisServices.Permission> 개체가 만들어집니다.  
  
 <xref:Microsoft.AnalysisServices.Permission> 개체를 제거하려면 개체의 Drop 메서드를 사용하여 삭제해야 합니다. 권한 컬렉션의 Remove 메서드를 사용하더라도 <xref:Microsoft.AnalysisServices.Permission> 개체가 서버에서 제거되지는 않습니다. 해당 권한이 응용 프로그램에 표시되지 않을 뿐입니다. 역할에 연결된 권한이 있으면 역할을 삭제할 수 없습니다.  
  
 사용할 수 있는 메서드 및 속성에 대한 자세한 내용은 <xref:Microsoft.AnalysisServices.Permission>의 <xref:Microsoft.AnalysisServices>을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 <xref:Microsoft.AnalysisServices>   
 [AMO 보안 개체 프로그래밍](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-security-objects.md)   
 [사용 권한 및 사용 권한 &#40; Analysis Services-다차원 데이터 &#41;](http://msdn.microsoft.com/library/59fa3573-f985-46cb-8042-7da71bd59a7b)   
 [AMO 클래스 소개](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [논리적 아키텍처 &#40; Analysis Services-다차원 데이터 &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [데이터베이스 개체 &#40; Analysis Services-다차원 데이터 &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
