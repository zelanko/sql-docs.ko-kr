---
title: "보고서에 어셈블리 참조 추가(SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- code [Reporting Services]
- custom assemblies [Reporting Services], referencing
- custom code [Reporting Services]
- adding assembly references
- assemblies [Reporting Services], references
ms.assetid: 0a03939e-48ce-4c30-b227-98533f2e0ccb
caps.latest.revision: "43"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: c58d1678086858bf1aeda3998386805184f7c4b1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="add-an-assembly-reference-to-a-report-ssrs"></a>보고서에 어셈블리 참조 추가(SSRS)
  <xref:System.Math> 또는 <xref:System.Convert>에 없는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 클래스에 대한 참조가 포함된 사용자 지정 코드를 포함하는 경우 보고서 처리기가 이름을 확인할 수 있도록 보고서에 대한 어셈블리 참조를 제공해야 합니다. 자세한 내용은 [보고서에 코드 추가&#40;SSRS&#41;](../../reporting-services/report-design/add-code-to-a-report-ssrs.md)를 참조하세요.  
  
### <a name="to-add-an-assembly-reference-to-a-report"></a>보고서에 어셈블리 참조를 추가하려면  
  
1.  **디자인** 뷰에서 보고서 테두리 바깥쪽의 디자인 화면을 마우스 오른쪽 단추로 클릭하고 **보고서 속성**을 클릭합니다.  
  
2.  **참조**를 클릭합니다.  
  
3.  **어셈블리 추가 또는 제거**에서 **추가**를 클릭한 다음 줄임표 단추를 클릭하여 해당 어셈블리를 찾습니다.  
  
4.  **클래스 추가 또는 제거**에서 **추가**를 클릭한 다음 클래스의 이름을 입력하고 보고서 내에서 사용할 인스턴스 이름을 제공합니다.  
  
    > [!NOTE]  
    >  인스턴스 기반 멤버에 대해서만 클래스 이름과 인스턴스 이름을 지정하십시오. **클래스** 목록에서 정적 멤버를 지정하지 마십시오. 자세한 내용은 [보고서 디자이너의 식에 포함된 사용자 지정 코드 및 어셈블리 참조&#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)를 나타냅니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목:  
 [보고서에서 사용자 지정 어셈블리 사용](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [보고서 속성 대화 상자, 참조](http://msdn.microsoft.com/library/4639d368-9918-4bb1-9953-7a724ca78dea)  
  
  
