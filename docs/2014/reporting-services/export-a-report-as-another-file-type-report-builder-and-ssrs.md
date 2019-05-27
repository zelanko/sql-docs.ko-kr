---
title: 다른 파일 형식 (보고서 작성기 및 SSRS)으로 보고서 내보내기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: b577568b-ecbd-44c3-be88-31dab6fc38a2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c6da8c1190c07d3df930a2d83937e3a5ec39da32
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109177"
---
# <a name="export-a-report-as-another-file-type-report-builder-and-ssrs"></a>다른 파일 형식으로 보고서 내보내기(보고서 작성기 및 SSRS)
  보고서 작성기 또는 보고서 디자이너에서 보고서를 미리 보면서 CSV, 이미지, PDF, [!INCLUDE[ofprword](../includes/ofprword-md.md)] 또는 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 같은 다른 파일 형식으로 보고서를 렌더링할 수도 있고, 보고서 서버에서 보고서를 보면서 보고서를 렌더링할 수도 있습니다. 보고서를 특정 형식으로 렌더링하면 보고서를 보고서 서버에 게시하지 않고서 보고서를 다른 파일 형식으로 즉시 저장하려는 경우나 보고서를 읽는 사람에게 특정 형식으로 배달된 보고서의 디자인이 어떤 모양일지 미리 확인하려는 경우에 도움이 됩니다. 보고서 서버에서 보고서를 렌더링하면 구독을 설정하려는 경우나 전자 메일을 통해 보고서를 배달하려는 경우 또는 보고서 서버에서 사용할 수 있도록 보고서를 저장하려는 경우에 도움이 됩니다. 자세한 내용은 [구독 및 배달&#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-export-a-report-as-another-file-type-in-report-builder"></a>보고서 작성기에서 보고서를 다른 파일 형식으로 내보내려면  
  
1.  보고서를 미리 봅니다.  
  
2.  리본에서 **내보내기**를 클릭합니다.  
  
3.  사용할 형식을 선택합니다.  
  
     **다른 이름으로 저장** 대화 상자가 열립니다. 기본적으로 파일 이름은 내보낸 보고서의 이름입니다. 필요한 경우 파일 이름을 변경할 수 있습니다.  
  
4.  내보낸 보고서를 저장한 위치로 이동하여 해당 보고서를 엽니다.  
  
> [!NOTE]  
>  해당 파일 형식과 연결된 프로그램이 없기 때문에 선택한 형식으로 보고서를 열 수 없는 경우에는 내보낸 보고서를 저장하거나 보고서를 열기 위한 프로그램을 온라인으로 찾으라는 메시지가 표시됩니다.  
  
### <a name="to-export-a-report-as-another-file-type-in-report-manager"></a>보고서 관리자에서 보고서를 다른 파일 형식으로 내보내려면  
  
1.  보고서 관리자 **홈** 페이지에서 내보낼 보고서를 찾아 이동합니다.  
  
2.  보고서를 클릭합니다.  
  
     보고서가 생성됩니다.  
  
3.  보고서 뷰어 도구 모음에서 **형식 선택** 드롭다운 화살표를 클릭합니다.  
  
4.  사용할 형식을 선택합니다.  
  
5.  **내보내기**를 클릭합니다.  
  
     파일을 열지 저장할지 확인하는 메시지가 나타납니다.  
  
6.  선택한 내보내기 형식으로 보고서를 보려면 **열기**를 클릭합니다.  
  
     \- 또는-  
  
     선택한 내보내기 형식으로 보고서를 즉시 저장하려면 **저장**을 클릭합니다.  
  
     선택한 형식에 연결되어 있는 애플리케이션을 사용하여 보고서가 표시 또는 저장됩니다. **저장**을 클릭하면 보고서를 저장할 위치를 묻는 메시지가 나타납니다.  
  
     **참고** 선택한 파일 형식에 연결된 프로그램이 없어서 지정된 형식으로 보고서를 열 수 없는 경우에는 내보낸 보고서를 저장하거나 보고서를 여는 데 필요한 프로그램을 온라인으로 찾으라는 메시지가 나타납니다.  
  
### <a name="to-export-a-report-as-another-file-type-in-a-sharepoint-library"></a>SharePoint 라이브러리에서 보고서를 다른 파일 형식으로 내보내려면  
  
1.  보고서를 미리 봅니다.  
  
2.  도구 모음에서 **동작**을 클릭하고 **내보내기**를 가리킨 다음 사용할 형식을 선택합니다.  
  
     **파일 다운로드** 대화 상자가 열립니다.  
  
3.  선택한 내보내기 형식으로 보고서를 보려면 **열기**를 클릭합니다.  
  
     \- 또는-  
  
     선택한 내보내기 형식으로 보고서를 즉시 저장하려면 **저장**을 클릭합니다.  
  
     선택한 형식에 연결되어 있는 애플리케이션을 사용하여 보고서가 표시 또는 저장됩니다. **저장**을 클릭하면 보고서를 저장할 위치를 묻는 메시지가 나타납니다.  
  
     필요한 경우 내보낸 보고서의 파일 이름을 변경합니다.  
  
     **참고** 선택한 파일 형식에 연결된 프로그램이 없어서 지정된 형식으로 보고서를 열 수 없는 경우에는 내보낸 보고서를 저장하거나 보고서를 여는 데 필요한 프로그램을 온라인으로 찾으라는 메시지가 나타납니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서를 내보내는 &#40;보고서 작성기 및 SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md)   
 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [여러 보고서 렌더링 확장 프로그램의 대화형 기능 &#40;보고서 작성기 및 SSRS&#41;](report-builder/interactive-functionality-different-report-rendering-extensions.md)  
  
  
