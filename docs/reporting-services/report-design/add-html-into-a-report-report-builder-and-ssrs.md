---
title: 보고서에 HTML 추가(보고서 작성기) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 30bd631a-f774-48e7-a13a-b6c2eb54d9bb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e18753c105eb63343bf57977f8ced3a0cf0fe9e6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081626"
---
# <a name="add-html-into-a-report-report-builder-and-ssrs"></a>보고서에 HTML 추가(보고서 작성기 및 SSRS)
  자리 표시자를 사용하여 데이터 세트의 필드에서 보고서에 사용할 HTML을 가져올 수 있습니다. 기본적으로 자리 표시자는 일반 텍스트를 나타내므로 자리 표시자 태그 형식을 HTML로 변경해야 합니다. 자세한 내용은 [보고서로 HTML 가져오기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/importing-html-into-a-report-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-html-from-a-field-in-your-dataset-into-a-text-box"></a>데이터 세트에 있는 필드의 HTML을 입력란에 추가하려면  
  
1.  **삽입** 탭에서 **목록**을 클릭합니다. 디자인 화면을 클릭한 다음 끌어 원하는 크기의 상자를 만듭니다.  
  
     **데이터 세트 속성** 대화 상자가 열립니다. 보고서에 포함된 데이터 세트나 공유 데이터 세트를 사용할 수 있습니다. 자세한 내용은 [데이터 세트 속성 대화 상자, 쿼리&#40;보고서 작성기&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md) 또는 [데이터 세트 속성 대화 상자, 쿼리](https://msdn.microsoft.com/library/1fa34a4b-7de0-4e92-99fa-bc28a206773f)를 참조하세요.  
  
2.  **삽입** 탭에서 **입력란**을 클릭합니다. 목록을 클릭한 다음 끌어 원하는 크기의 상자를 만듭니다.  
  
3.  데이터 세트의 HTML 필드를 입력란으로 끌어옵니다. 해당 필드에 대한 자리 표시자가 만들어집니다.  
  
4.  자리 표시자를 마우스 오른쪽 단추로 클릭한 다음 **자리 표시자 속성**을 클릭합니다.  
  
5.  **일반** 탭에서 **값** 상자에 3단계에서 끌어 놓은 필드로 계산되는 식이 들어 있는지 확인합니다.  
  
6.  **HTML - HTML 태그를 스타일로 해석**을 클릭합니다. 이렇게 하면 필드가 HTML로 평가됩니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [숫자 및 날짜 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [선, 색 및 이미지 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-lines-colors-and-images-report-builder-and-ssrs.md)   
 [자리 표시자 속성 대화 상자, 일반&#40;보고서 작성기 및 SSRS&#41;](https://msdn.microsoft.com/library/7a867736-a3b0-4b5a-b3e5-fe7c8d7618a8)  
  
  
