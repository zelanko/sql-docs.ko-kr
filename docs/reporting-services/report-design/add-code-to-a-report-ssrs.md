---
title: "보고서에 코드 추가(SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- code [Reporting Services]
- custom code [Reporting Services]
- expressions [Reporting Services], code
- adding code
- reports [Reporting Services], code
ms.assetid: 00ef8fc6-99fe-49b2-8a22-7eb475881dc4
caps.latest.revision: "41"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: af3ca4fdc6db5647288eeddb4da5d8d7e63edcf9
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="add-code-to-a-report-ssrs"></a>보고서에 코드 추가(SSRS)
  모든 식에서 고유한 사용자 지정 코드를 호출할 수 있습니다. 다음과 같은 두 가지 방법으로 코드를 제공할 수 있습니다.  
  
-   [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 으로 작성된 코드를 보고서에 직접 포함합니다. 코드가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 또는 <xref:System.Math> 가 아닌 <xref:System.Convert>를 참조하는 경우 보고서에 해당 참조를 추가해야 합니다. 자세한 내용은 [보고서에 어셈블리 참조 추가&#40;SSRS&#41;](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md)를 참조하세요. 코드에서 만들 수 있는 기타 참조에 대한 자세한 내용은 [보고서 디자이너의 식에 포함된 사용자 지정 코드 및 어셈블리 참조&#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)를 참조하세요.  
  
-   [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]를 사용하여 사용자 지정 코드 어셈블리를 제공합니다. 사용자 지정 어셈블리를 제공하는 경우 보고서를 작성하는 컴퓨터와 보고서를 보는 보고서 서버 모두에 해당 어셈블리를 설치해야 합니다. 자세한 내용은 [Using Custom Assemblies with Reports](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)을(를) 참조하세요.  
  
### <a name="to-add-embedded-code-to-a-report"></a>보고서에 포함 코드를 추가하려면  
  
1.  **디자인** 뷰에서 보고서 테두리 바깥쪽의 디자인 화면을 마우스 오른쪽 단추로 클릭하고 **보고서 속성**을 클릭합니다.  
  
2.  **코드**를 클릭합니다.  
  
3.  **사용자 지정 코드**에 코드를 입력합니다. 코드에 오류가 있으면 보고서 실행 시 경고가 발생합니다. 다음 예에서는 " `ChangeWord` "라는 단어를 "`Bike`"로 바꾸는`Bicycle`라는 사용자 지정 함수를 만듭니다.  
  
    ```  
    Public Function ChangeWord(ByVal s As String) As String  
       Dim strBuilder As New System.Text.StringBuilder(s)  
       If s.Contains("Bike") Then  
          strBuilder.Replace("Bike", "Bicycle")  
          Return strBuilder.ToString()  
          Else : Return s  
       End If  
    End Function  
    ```  
  
4.  다음 예에서는 하나의 식을 사용하여 Category라는 데이터 집합 필드를 이 함수에 전달하는 방법을 보여 줍니다.  
  
    ```  
    =Code.ChangeWord(Fields!Category.Value)  
    ```  
  
     범주 값을 표시하는 테이블 셀에 이 식을 추가하면 해당 행의 데이터 집합 필드에 "Bike"라는 단어가 있을 때마다 해당 테이블 셀 값이 "Bicycle"이라는 단어를 대신 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 속성 대화 상자, 코드](http://msdn.microsoft.com/library/955d4b11-17b4-4f1c-9690-6e7af54caea7)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [매개 변수 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
