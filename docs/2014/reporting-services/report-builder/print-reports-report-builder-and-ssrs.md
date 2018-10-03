---
title: 보고서 인쇄(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 4bad1b6e-7d94-4b17-9502-ccd3dce0fdd9
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 0b0f0b2087471d8f0c905b1a173eff57a0be7fd4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096703"
---
# <a name="print-reports-report-builder-and-ssrs"></a>보고서 인쇄(보고서 작성기 및 SSRS)
  보고서 서버에 보고서를 저장한 후에는 내보낸 보고서를 보는 데 사용되는 응용 프로그램, 보고서 관리자 또는 브라우저에서 보고서를 보고 인쇄할 수 있습니다. 보고서를 저장하기 전 미리 볼 때 해당 보고서를 인쇄할 수 있습니다.  
  
 모든 인쇄 작업은 요청 시 클라이언트 컴퓨터에서 처리됩니다. 보고서 서버에서 웹 서버에 연결되어 있는 프린터로 직접 인쇄 작업을 라우팅할 수 있는 서버 쪽 인쇄 기능은 없습니다. 프린터와 인쇄 옵션은 개별 보고서 사용자가 표준 **인쇄** 대화 상자를 사용하여 선택합니다.  
  
 인쇄 결과물에 맞게 보고서를 디자인하려는 보고서 작성자는 페이지 나누기, 페이지 머리글과 바닥글, 식 및 배경 이미지를 사용하여 인쇄 기반 디자인을 만들 수 있습니다. 인쇄 결과물에 맞는 보고서 디자인 요소의 예에는 모든 보고서의 뒷면에 인쇄되는 "규정 및 내용"이나 레터헤드와 같은 그래픽 및 텍스트 요소가 포함될 수 있습니다.  
  
 여러 렌더링 형식에 대해 페이지 매김이 구현되는 방식으로 인해 렌더링 형식에 따라 일부 보고서에서는 최적의 인쇄 결과물을 얻지 못할 수 있습니다. 다음 목록에서는 이에 대한 예를 보여 줍니다.  
  
1.  보고서 페이지는 데이터 양의 변화를 수용할 수 있도록 디자인됩니다. 예를 들어 행렬을 포함하는 보고서에서 사용자가 행과 열을 대화형으로 토글하면 이에 맞게 페이지가 가로와 세로 방향으로 모두 늘어납니다. 행렬을 확장하지 않는 사용자에게는 행렬을 확장하는 사용자와는 다른 인쇄 결과가 나타납니다.  
  
2.  같은 보고서에 가로 모드와 세로 모드의 페이지를 함께 사용할 수 없으며 브라우저 또는 다른 응용 프로그램에서 렌더링된 보고서 레이아웃과 함께 존재하거나 이를 대체하는 인쇄 기반 레이아웃을 만들 수 없습니다.  
  
3.  내보낸 보고서 인쇄물에는 대부분 사용자가 컴퓨터 모니터에서 볼 때 보고서에 표시되는 항목이 모두 포함됩니다. 보고서 디자인 화면의 공백이 유지됩니다. 빈 페이지를 가로로 추가하거나 제거하려면 보고서 페이지 너비를 변경합니다.  
  
> [!NOTE]  
>  브라우저의 인쇄 명령을 사용할 경우 HTML 보고서 인쇄물에는 첫 번째 페이지의 내용만 포함됩니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 클라이언트 인쇄 기능을 사용하여 HTML 보고서를 인쇄하면 보다 나은 결과를 얻을 수 있습니다. 자세한 내용은 [인쇄 컨트롤을 사용 하 여 브라우저에서 보고서 인쇄 &#40;보고서 작성기 및 SSRS&#41;](print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="in-this-section"></a>섹션 내용  
 [인쇄 컨트롤을 사용 하 여 브라우저에서 보고서 인쇄 &#40;보고서 작성기 및 SSRS&#41;](print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)  
 클라이언트 쪽 인쇄 기능을 사용하여 웹 브라우저나 보고서 관리자에서 보고서를 인쇄하는 방법을 설명합니다.  
  
 [다른 응용 프로그램에서 보고서를 인쇄 합니다. &#40;보고서 작성기 및 SSRS&#41;](print-reports-from-other-applications-report-builder-and-ssrs.md)  
 다른 응용 프로그램으로 내보낸 보고서를 인쇄하는 방법을 설명합니다.  
  
 [보고서 인쇄 &#40;보고서 작성기 및 SSRS&#41;](print-a-report-report-builder-and-ssrs.md)  
 보고서를 인쇄하는 방법, 페이지 여백을 조절하는 방법, 하드 페이지 나누기 렌더러(PDF, 이미지 또는 인쇄)로 렌더링할 보고서의 용지 크기를 지정하는 방법에 대한 단계별 지침을 제공합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서를 내보내는 &#40;보고서 작성기 및 SSRS&#41;](export-reports-report-builder-and-ssrs.md)   
 [페이지 머리글 및 바닥글 &#40;보고서 작성기 및 SSRS&#41;](../report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [이미지 &#40;보고서 작성기 및 SSRS&#41;](../report-design/images-report-builder-and-ssrs.md)   
 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)  
  
  
