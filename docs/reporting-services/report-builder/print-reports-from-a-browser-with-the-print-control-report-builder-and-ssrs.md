---
title: "인쇄 컨트롤 (보고서 작성기 및 SSRS)를 사용 하 여 브라우저에서 보고서를 인쇄 합니다. | Microsoft Docs"
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
ms.assetid: 10054250-d915-4bcb-8a1d-26837db4e932
caps.latest.revision: 13
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3674bb697d86ac79906aa4ee5172ad24030a22fc
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs"></a>인쇄 컨트롤을 사용하여 브라우저에서 보고서 인쇄(보고서 작성기 및 SSRS)
  보고서를 인쇄하는 데 가장 많이 사용되는 클라이언트 응용 프로그램은 브라우저이지만 브라우저 인쇄 기능이 보고서 인쇄에 이상적이지는 않습니다. 브라우저의 인쇄 기능은 웹 페이지 인쇄용으로 개발되었기 때문입니다. 일반적으로 브라우저에서 인쇄하는 페이지에는 웹 페이지의 모든 시각적 요소뿐만 아니라 페이지나 웹 사이트를 식별하는 머리글 및 바닥글 정보가 포함됩니다. 브라우저에서 인쇄하면 현재 창의 내용이 인쇄됩니다. 여러 페이지로 구성된 보고서의 경우 브라우저에서는 첫 페이지만 인쇄됩니다. 보고서 페이지가 인쇄된 페이지보다 크면 첫 페이지도 제대로 인쇄되지 않을 수 있습니다.  
  
 브라우저에 표시되는 보고서의 인쇄 품질을 향상시키고 여러 페이지를 인쇄하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 제공하는 클라이언트 쪽 인쇄 기능을 사용하는 것이 좋습니다. 클라이언트 쪽 인쇄 기능에서 제공하는 표준 **인쇄** 대화 상자를 사용하여 프린터를 선택하고 페이지와 여백을 지정하고 인쇄 전에 보고서를 미리 볼 수 있습니다. 브라우저의 **파일** 메뉴에 있는 **인쇄** 명령 대신 클라이언트 쪽 인쇄 기능을 사용할 수 있습니다. 클라이언트 쪽 인쇄 기능을 사용하면 웹 페이지 인쇄 결과물에 나타나는 추가 요소 없이 보고서가 디자인된 그대로 인쇄됩니다.  
  
 클라이언트 쪽 인쇄를 사용하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX 컨트롤을 설치해야 합니다. 자세한 내용은 [Reporting Services에 대한 클라이언트 쪽 인쇄 기능 설정 및 해제](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="print-options"></a>인쇄 옵션  
 보고서의 인쇄 속성을 구성하려면 **인쇄** 대화 상자에서 **속성** 단추를 클릭합니다. **용지 크기** 는 보고서 정의에 지정된 보고서 페이지 크기의 기본 높이와 너비에 의해 결정됩니다. 사용 가능한 값은 프린터 종류와 기능에 따라 다릅니다. 너비와 높이에 표시되는 기본값은 컴퓨터에 구성된 인쇄 드라이버에 의해 결정됩니다. 기본값을 변경하면 새로운 치수로 보고서가 인쇄됩니다. 페이지 너비와 높이는 각각 **방향**으로 결정되며 방향은 **세로** 또는 **가로**로 설정됩니다. 표시되는 기본 방향은 보고서의 페이지 너비와 높이에 따라 다릅니다.  
  
> [!NOTE]  
>  **인쇄** 대화 상자와 너비, 높이 및 페이지 방향에 대한 기본 프린터 설정은 보고서 정의에 의해 결정됩니다.  
  
### <a name="print-preview"></a>인쇄 미리 보기  
 보고서를 미리 보려면 **인쇄** 대화 상자에서 **미리 보기** 단추를 클릭합니다. 미리 보기를 클릭하면 보고서의 첫 페이지가 별도의 미리 보기 창에서 열립니다. 보고서 서버에서 보고서가 렌더링됨에 따라 추가 페이지도 표시됩니다. 미리 보는 보고서는 EMF 형식으로 렌더링됩니다. 이전 페이지나 다음 페이지로 이동할 수 있으며 마지막 페이지에서는 **다음** 단추가 비활성화됩니다.  
  
### <a name="adjusting-print-margins"></a>인쇄 여백 조정  
 보고서를 인쇄하기 전에 렌더링된 EMF 보고서에서 인쇄 여백을 수정할 수 있습니다. 이렇게 하려면 **인쇄** 대화 상자에서 **미리 보기** 단추를 클릭합니다. 미리 보기 페이지의 위쪽에서 **여백** 단추를 클릭합니다. 그러면 여백 대화 상자가 표시됩니다. 원하는 대로 위쪽, 아래쪽, 오른쪽 및 왼쪽 여백을 구성합니다. [!INCLUDE[clickOK](../../includes/clickok-md.md)]대화 상자가 닫히고 렌더링 미리 보기 및 인쇄에 대 한 설정이 저장 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 인쇄 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [보고서 &#40; 인쇄 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)  
  
  

