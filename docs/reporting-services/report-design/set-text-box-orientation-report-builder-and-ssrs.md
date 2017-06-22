---
title: "입력란 방향 (보고서 작성기 및 SSRS) 설정 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 64bd53f4-2f31-4732-8c2e-64c7b54b6972
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4cc52b4687f9a2c944ea3a93c15b637d894c7a96
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="set-text-box-orientation-report-builder-and-ssrs"></a>입력란 방향 설정(보고서 작성기 및 SSRS)
페이지가 매겨진 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 보고서에서 다음과 같은 여러 방향으로 입력란을 회전할 수 있습니다.   
* 가로로   
* 세로로(텍스트를 위에서 아래로 읽는 경우 90도 회전)  
* 270도 회전(텍스트를 아래에서 위로 읽는 경우)   
  
텍스트가 아니라 입력란을 회전하기 때문에 방향은 입력란의 모든 텍스트에 적용됩니다. 텍스트의 일부에 대해 다른 방향을 지정할 수는 없습니다. 회전된 텍스트를 포함하도록 열 너비와 행 높이를 수동으로 조정합니다.  
  
 텍스트 방향을 지정할 때 사용하는 WritingMode 속성은 **입력란 속성** 대화 상자에 없습니다. 속성 창에 있으며 여기서 해당 속성을 설정합니다.   
  
## <a name="to-rotate-text"></a>텍스트를 회전하려면  
  
1.  보고서를 만들거나 기존 보고서를 열고 디자인 화면에 [입력란을 추가](../../reporting-services/report-design/add-move-or-delete-a-text-box-report-builder-and-ssrs.md) 합니다.  
  
3.  회전할 입력란을 선택합니다.  
  
2.  속성 창이 열려 있지 않으면 **보기** 탭에서 **속성** 확인란을 선택합니다.  
  
4.  속성 창에서 WritingMode 속성을 찾은 다음 입력란에 적용할 텍스트 방향을 선택합니다.  
  
    > [!NOTE]  
    >  속성 창의 속성이 범주로 구성되어 있는 경우 WritingMode는 **지역화** 범주에 있습니다.  
  
5.  목록 상자에서 **Horizontal**, **Vertical**또는 **Rotate270**을 선택합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [입력란&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)   
 [자습서: 텍스트 서식 지정&#40;보고서 작성기&#41;](../../reporting-services/tutorial-format-text-report-builder.md)  
  
  
