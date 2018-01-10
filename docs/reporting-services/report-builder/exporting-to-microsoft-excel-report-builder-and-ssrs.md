---
title: "Microsoft Excel로 내보내기(보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 01/09/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-builder
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 74f726fc-2167-47af-9093-1644e03ef01f
caps.latest.revision: "28"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Active
ms.openlocfilehash: 604952211abf63d6dacb111c8170d678acd2d80a
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="exporting-to-microsoft-excel-report-builder-and-ssrs"></a>Microsoft Excel로 내보내기(보고서 작성기 및 SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Excel 렌더링 확장 프로그램은 페이지가 매겨진 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서를 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 형식(.xlsx)으로 렌더링합니다. Excel 렌더링 확장 프로그램에서는 Excel의 열 너비는 보고서의 열 너비를 보다 정확하게 반영합니다.  
  
 형식은 Office Open XML입니다. 이 렌더러에 의해 생성된 파일의 콘텐츠 형식은 **application/vnd.openxmlformats-officedocument.spreadsheetml.sheet** 이고 파일 확장명은 .xlsx입니다.  
  
 장치 정보 설정을 변경하여 이 렌더러의 기본 설정을 일부 변경할 수 있습니다. 자세한 내용은 [Excel Device Information Settings](../../reporting-services/excel-device-information-settings.md)을 참조하세요.  
  
 Excel로 내보내는 방법에 대한 자세한 내용은 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  **String**유형의 매개 변수를 정의할 경우 모든 값을 사용할 수 있는 입력란이 사용자에게 제공됩니다. 보고서 매개 변수가 쿼리 매개 변수에 연결되지 않고 매개 변수 값이 보고서에 포함된 경우 보고서 사용자는 식 구문, 스크립트 또는 URL을 매개 변수 값에 입력하고 보고서를 Excel로 렌더링할 수 있습니다. 이후 다른 사용자가 보고서를 보면서 렌더링된 매개 변수 내용을 클릭할 경우 악의적인 스크립트나 링크가 실수로 실행될 수 있습니다.  
>   
>  악의적인 스크립트를 실수로 실행하는 위험을 줄이기 위해 신뢰할 수 있는 원본의 렌더링된 보고서만 여세요. 보고서를 안전하게 보호하는 방법에 대한 자세한 내용은 [보고서 및 리소스 보안](../../reporting-services/security/secure-reports-and-resources.md)을 참조하세요.  
  
##  <a name="ExcelLimitations"></a> Excel 제한 사항  
 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 은 Excel의 기능 및 해당 파일 형식으로 인해 내보낸 보고서에 대해 제한을 둡니다. 가장 중요한 제한 사항은 다음과 같습니다.  
  
-   최대 열 너비는 255자 또는 1726.5포인트로 제한됩니다. 렌더러에서는 열 너비가 이 제한값을 초과하지 않는지 여부를 확인하지 않습니다.  
  
-   셀의 문자 수는 최대 32,767자로 제한됩니다. 이 값을 초과하면 렌더러는 오류 메시지를 표시합니다.  
  
-   최대 행 높이는 409포인트입니다. 행의 내용이 행 높이가 409포인트를 초과하게 되면 Excel 셀은 409포인트까지의 텍스트 부분 양을 표시합니다. 셀 내용의 나머지는 여전히 셸 내에 있습니다(최대 32,767 문자의 Excel의 최대 수).

-  최대 행 높이가 409포인트이므로 보고서에 있는 셀의 정의된 높이가 409포인트 보다 큰 값인 경우 Excel은 셸 내용을 여러 개의 행으로 분할합니다.
  
-   Excel에서는 워크시트의 최대 개수를 별도로 지정하지 않고 있지만 메모리나 디스크 공간 같은 외부 요인에 따라 워크시트의 수가 제한될 수 있습니다.  
  
-   Excel에서 허용하는 윤곽선 중첩 수준은 최대 7개입니다.  
  
-   다른 항목의 설정/해제 여부를 제어하는 보고서 항목이 설정/해제 대상인 항목의 이전 행 또는 열이나 다음 행 또는 열에 있지 않으면 윤곽선도 비활성화됩니다.  
  
 Excel 제한 사항에 대한 자세한 내용은 [Excel 사양 및 제한 사항](https://support.office.com/article/Excel-specifications-and-limits-CA36E2DC-1F09-4620-B726-67C00B05040F)을 참조하세요.  
  
### <a name="sizes-of-excel-2003-xls-files"></a>Excel 2003 파일(.xls)의 크기  
  
> [!IMPORTANT]  
>  [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003 렌더링 확장 프로그램은 더 이상 사용되지 않습니다. 자세한 내용은 [SQL Server 2016의 SQL Server Reporting Services에서 지원되지 않는 기능](../../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)을 참조하세요.  
  
 보고서를 먼저 내보낸 다음 Excel 2003에 저장할 경우에는 *.xls 통합 문서 파일에 자동으로 적용되는 파일 최적화의 이점을 활용할 수 없습니다. 따라서 파일 크기가 커지고 전자 메일 구독 및 첨부 파일에 문제가 발생할 수 있습니다. 내보내는 보고서의 \*.xls 파일 크기를 줄이려면 \*.xls 파일을 연 다음 통합 문서를 다시 저장합니다. 통합 문서를 다시 저장하면 일반적으로 파일 크기가 40-50%로 줄어듭니다.  
  
> [!NOTE]  
>  Excel 2003에서는 워크시트에서 Excel 셀에 표시되는 문자 수가 약 1000자이지만 수식 입력줄에서는 최대 문자 수까지만 편집할 수 있습니다. 현재 Excel 파일(.xlsx)에는 이러한 제한 사항이 적용되지 않습니다.  
  
### <a name="text-boxes-and-text"></a>입력란 및 텍스트  
 입력란 및 텍스트에는 다음과 같은 제한 사항이 적용됩니다.  
  
-   입력란에 식을 입력하면 식이 Excel 수식으로 변환되지 않습니다. 각 입력란의 값은 보고서 처리 중 평가되고 평가된 식은 각 Excel 셀의 내용으로 내보내집니다.  
  
-   입력란은 하나의 Excel 셀 내에 렌더링됩니다. Excel 셀 내의 개별 텍스트에는 글꼴 크기, 글꼴, 장식 및 글꼴 스타일 서식만 지원됩니다.  
  
-   "윗줄" 텍스트 효과는 Excel에서 지원되지 않습니다.  
  
-   Excel에서는 기본적으로 셀의 왼쪽과 오른쪽에 약 3.75포인트의 안쪽 여백이 추가됩니다. 입력란의 안쪽 여백이 3.75포인트보다 작게 설정되어 있고 텍스트를 간신히 수용할 수 있을 만큼의 너비만 확보되어 있으면 Excel에서 텍스트의 줄이 바뀔 수 있습니다.  
  
    > [!NOTE]  
    >  이 문제를 해결하려면 보고서에서 입력란의 너비를 늘려야 합니다.  
  
### <a name="images"></a>이미지  
 이미지에는 다음과 같은 제한 사항이 적용됩니다.  
  
-   Excel에서는 개별 셀에 대한 배경 이미지를 지원하지 않으므로 보고서 항목의 배경 이미지는 무시됩니다.  
  
-   Excel 렌더링 확장 프로그램은 보고서 본문에 대해서만 배경 이미지를 지원합니다. 보고서에 보고서 본문 배경 이미지가 표시되어 있으면 그 이미지가 워크시트 배경 이미지로 렌더링됩니다.  
  
### <a name="rectangles"></a>사각형  
 사각형에는 다음과 같은 제한 사항이 적용됩니다.  
  
-   보고서 바닥글의 사각형은 Excel로 내보내지지 않습니다. 그러나 보고서 본문, 테이블릭스 셀 등의 사각형은 Excel 셀 범위로 렌더링됩니다.  
  
### <a name="report-headers-and-footers"></a>보고서 머리글 및 바닥글  
 보고서 머리글 및 바닥글에는 다음과 같은 제한 사항이 적용됩니다.  
  
-   Excel 머리글과 바닥글에는 태그를 포함하여 문자를 최대 256자까지 사용할 수 있습니다. 256자 이후의 문자열은 렌더링 확장 프로그램을 통해 잘립니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 보고서 머리글 및 바닥글의 여백을 지원하지 않습니다. Excel로 내보낼 경우 이러한 여백 값은 0으로 설정되며, 여러 데이터 행이 포함된 머리글이나 바닥글의 경우 프린터 설정에 따라 여러 행이 인쇄되지 않을 수 있습니다.  
  
-   Excel로 내보낼 때 머리글 또는 바닥글의 입력란 서식은 유지되지만 맞춤 설정은 유지되지 않습니다. 이는 보고서를 Excel로 렌더링할 때 선행 및 후행 공백이 잘리기 때문입니다.  
  
### <a name="merging-cells"></a>셀 병합  
 셀 병합에는 다음과 같은 제한 사항이 적용됩니다.  
  
-   셀을 병합하면 자동 줄 바꿈이 제대로 적용되지 않습니다. AutoSize 속성을 사용하여 입력란을 렌더링하는 행에 병합된 셀이 있으면 크기 자동 조정이 제대로 적용되지 않습니다.  
  
 Excel 렌더러는 기본적으로 레이아웃 렌더러입니다. 즉, 렌더링되는 보고서의 레이아웃을 가능한 한 Excel 워크시트와 비슷하게 복제하는 것이 목적이므로 보고서 레이아웃을 유지하기 위해 워크시트에서 셀이 병합될 수 있습니다. Excel의 정렬 기능은 셀이 매우 특별한 방식으로 병합된 경우에만 올바르게 작동하므로 이렇게 병합된 셀로 인해 문제가 발생할 수 있습니다. 예들 들어 Excel에서 병합된 셀 범위는 크기가 동일해야 정렬됩니다.  
  
 Excel 워크시트로 내보낸 보고서를 정렬할 수 있어야 하는 경우 다음과 같이 하면 Excel 정렬 기능에 문제를 일으키는 일반적인 원인인 Excel 워크시트에서 병합되는 셀 수를 줄일 수 있습니다.  
  
-   셀이 병합되는 가장 일반적인 원인은 항목이 왼쪽과 오른쪽으로 정렬되어 있지 않기 때문입니다. 모든 보고서 항목의 왼쪽 및 오른쪽 가장자리가 서로 정렬되어 있는지 확인하세요. 항목을 정렬하고 너비를 동일하게 만들면 대부분의 경우 문제가 해결됩니다.  
  
-   모든 항목을 정확하게 정렬해도 일부 열이 계속해서 병합되는 경우도 드물지만 있을 수 있습니다. 이는 Excel 워크시트가 렌더링될 때 내부 단위 변환 및 반올림이 수행되었기 때문일 수 있습니다. RDL(Report Definition Language)에서는 인치, 픽셀, 센티미터 및 포인트와 같은 여러 측정 단위로 위치와 크기를 지정할 수 있습니다. Excel에서는 내부적으로 포인트가 사용됩니다. 인치 및 센티미터를 포인트로 변환할 때 변환 문제와 반올림의 잠재적인 부정확성을 최소화하려면 가장 직접적인 결과에 대해 모든 측정 단위를 정수 포인트로 지정하는 것이 좋습니다. 1인치는 72포인트입니다.  
  
### <a name="report-row-groups-and-column-groups"></a>보고서 행 그룹 및 열 그룹  
 행 그룹 또는 열 그룹이 들어 있는 보고서는 Excel로 내보낼 때 빈 셀을 포함합니다. 통근 거리에 대한 행을 그룹화하는 보고서의 경우 각 통근 거리에 여러 고객이 포함될 수 있습니다. 다음 그림에서는 보고서를 표시합니다.  
  
 ![Reporting Services 웹 포털의 보고서](../../reporting-services/report-builder/media/ssrb-excelexportssrs.png "Reporting Services 웹 포털의 보고서")  
  
 보고서를 Excel로 내보내면 통근 거리 열의 한 셀에만 통근 거리가 표시됩니다. 보고서에서의 텍스트 정렬(위, 가운데 또는 아래)에 따라 값은 첫 번째, 가운데 또는 마지막 셀입니다. 나머지 셀은 비어 있습니다. 고객 이름이 들어 있는 Name 열에 빈 셀이 없습니다. 다음 그림에서는 Excel로 내보낸 후의 보고서를 보여 줍니다. 강조를 위해 빨강 셀 테두리가 추가되었습니다. 회색 상자는 빈 셀입니다. 빨간색 선과 회색 상자는 내보낸 보고서에 포함되지 않습니다.  
  
 ![줄이 포함된 Excel로 내보낸 보고서](../../reporting-services/report-builder/media/ssrb-exportedexcellines.png "줄이 포함된 Excel로 내보낸 보고서")  
  
 즉, 행 그룹 또는 열 그룹의 보고서는 Excel로 내보낸 후, 내보낸 데이터를 피벗 테이블에서 표시하기 전에 수정해야 합니다. 워크시트를 모든 셀에 값이 있는 플랫 테이블로 만들기 위해 누락된 셀에 그룹 값을 추가해야 합니다. 다음 그림에서는 업데이트된 워크시트를 보여 줍니다.  
  
 ![평면화된 Excel로 내보낸 보고서](../../reporting-services/report-builder/media/ssrb-excelexportnomatrix.png "평면화된 Excel로 내보낸 보고서")  
  
 따라서 보고서 데이터의 추가 분석을 위해 보고서를 Excel로 내보내는 특정 용도의 보고서를 만드는 경우 보고서의 행 또는 열에 대해 그룹화를 수행하지 않는 것이 좋습니다.  
  
## <a name="excel-renderer"></a>Excel 렌더러  
  
### <a name="current-xlsx-excel-file-renderer"></a>현재 Excel 파일(.xlsx) 렌더러  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 기본 Excel 렌더러는 현재 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 파일(.xlsx)과 호환되는 버전입니다. 이 옵션은 **웹 포털 및 SharePoint의** 내보내기 **메뉴에 나열되는** Excel [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 옵션입니다.  
  
 이전 Excel 2003(.xls) 렌더러가 아닌 기본 Excel 렌더러를 사용하는 경우 Word, Excel 및 PowerPoint용 Microsoft Office 호환 기능 팩을 설치하면 이전 버전의 Excel에서 내보낸 파일을 열 수 있습니다.  
  
### <a name="excel-2003-xls-renderer"></a>Excel 2003(.xls) 렌더러  
  
> [!IMPORTANT]  
>  [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003 렌더링 확장 프로그램은 더 이상 사용되지 않습니다. 자세한 내용은 [SQL Server 2016의 SQL Server Reporting Services에서 지원되지 않는 기능](../../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)을 참조하세요.  
  
 Excel 2003과 호환되는 이전 버전의 Excel 렌더러는 이제 이름이 Excel 2003으로 지정되어 해당 이름을 사용하여 메뉴에 나열됩니다. 이 렌더러을 통해 생성되는 파일의 콘텐츠 형식은 **application/vnd.ms-excel** 이고 파일 이름 확장명은 .xls입니다.  
  
 기본적으로 **Excel 2003** 메뉴 옵션은 표시되지 않습니다. 관리자가 RSReportServer 구성 파일을 업데이트하여 특정 상황에서 표시되도록 설정할 수 있습니다. Excel 2003 렌더러를 사용하여 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 보고서를 내보내려면 RSReportDesigner 구성 파일을 업데이트합니다.  
  
 다음과 같은 시나리오에서는 **Excel 2003의** 메뉴 옵션 확장이 표시되지 않습니다.  
  
-   보고서 작성기가 연결되지 않은 모드이고 보고서 작성기에서 보고서를 미리 보는 경우. RSReportServer 구성 파일이 보고서 서버에 존재하기 때문에 구성 파일을 읽으려면 보고서를 내보내는 위치의 도구 또는 제품이 보고서 서버에 연결되어 있어야 합니다.  
  
-   보고서 뷰어 웹 파트가 로컬 모드이고 SharePoint 팜이 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버와 통합되지 않은 경우. 자세한 내용은 [보고서 뷰어의 로컬 모드와 보고서 뷰어의 연결 모드 보고서&#40;SharePoint 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md)  
  
 **Excel 2003** 메뉴 옵션 렌더러가 표시되도록 구성된 경우 다음과 같은 시나리오에서 Excel 및 Excel 2003 옵션을 사용할 수 있습니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털 기본 모드  
  
-   Reporting Services가 SharePoint 통합 모드로 설치된 경우의 SharePoint 사이트  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 및 보고서 미리 보기  
  
-   보고서 작성기가 보고서 서버에 연결된 경우.  
  
-   보고서 뷰어 웹 파트가 원격 모드인 경우  
  
 다음 XML에서는 RSReportServer 및 RSReportDesigner 구성 파일의 두 Excel 렌더링 확장 프로그램에 대한 요소를 보여 줍니다.  
  
 `<Extension Name="EXCELOPENXML" Type="Microsoft.ReportingServices.Rendering.ExcelOpenXmlRenderer.ExcelOpenXmlRenderer,Microsoft.ReportingServices.ExcelRendering"/>`  
  
 `<Extension Name="EXCEL" Type="Microsoft.ReportingServices.Rendering.ExcelRenderer.ExcelRenderer,Microsoft.ReportingServices.ExcelRendering" Visible="false"/>`  
  
 EXCELOPENXML 확장은 현재 Excel 파일(.xlsx)에 대한 Excel 렌더러를 정의합니다. EXCEL 확장은 Excel 2003 버전을 정의합니다. `Visible = “false”` 는 Excel 2003 렌더러가 숨겨져 있음을 나타냅니다. 자세한 내용은 [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) 및 [RSReportDesigner 구성 파일](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)을 참조하세요.  
  
### <a name="differences-between-the-current-xlsx-excel-and-excel-2003-renderers"></a>현재 Excel(.xlsx)과 Excel 2003 렌더러의 차이점  
 현재 Excel(.xlsx) 또는 Excel 2003 렌더러를 사용하여 렌더링된 보고서는 일반적으로 동일하며 드문 경우에만 두 형식 간의 차이점을 알 수 있습니다. 다음 표에서는 Excel과 Excel 2003 렌더러를 비교합니다.  
  
|속성|Excel 2003|현재 Excel|  
|--------------|----------------|-------------------|  
|워크시트당 최대 열 수|256|16,384|  
|워크시트당 최대 행 수|65,536|1,048,576|  
|워크시트에 허용된 색상 수|56(색상표)<br /><br /> 보고서에 56개보다 많은 수의 색을 사용한 경우 렌더링 확장 프로그램에서는 필요한 색을 사용자 지정 색상표에 이미 들어 있는 56색 중 하나로 대체합니다.|약 1600만(24비트 색상)|  
|ZIP 압축 파일|InclusionThresholdSetting|ZIP 압축|  
|기본 글꼴 패밀리|Arial|Calibri|  
|기본 글꼴 크기|10pt|11pt|  
|기본 행 높이|12.75pt|15pt|  
  
 보고서는 행 높이를 명시적으로 설정하기 때문에 기본 행 높이는 Excel로 내보낼 때 자동으로 크기가 조정되는 행에만 영향을 줍니다.  
  
##  <a name="ReportItemsExcel"></a> Excel에서의 보고서 항목  
 사각형, 하위 보고서, 보고서 본문 및 데이터 영역은 Excel 셀의 범위로 렌더링됩니다. 입력란, 이미지, 차트, 데이터 막대, 스파크라인, 지도, 계기 및 표시기는 Excel 셀 하나 안에 렌더링해야 합니다. 보고서의 나머지 부분의 레이아웃에 따라 해당 항목이 병합될 수도 있습니다.  
  
 이미지, 차트, 스파크라인, 데이터 막대, 지도, 계기, 표시기 및 선은 한 개의 Excel 셀 안에 배치되지만 실제로 놓이는 위치는 셀의 모눈 위입니다. 선은 셀 테두리로 렌더링됩니다.  
  
 차트, 스파크라인, 데이터 막대, 지도, 계기 및 표시기는 그림으로 내보내집니다. 그림에서 설명하는 데이터(예: 차트의 값 및 멤버 레이블)는 그림과 함께 내보내지지 않으며 보고서 내 데이터 영역의 열이나 행에 포함되어 있지 않은 데이터는 Excel 통합 문서에서 사용할 수 없습니다.  
  
 차트, 스파크라인, 데이터 막대, 지도, 계기 및 표시기 데이터를 사용하려면 보고서를 .csv 파일로 내보내거나 보고서에서 Atom 규격 데이터 피드를 생성하세요. 자세한 내용은 [CSV 파일로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md) 및 [보고서에서 데이터 피드 생성&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="page-sizing"></a>페이지 크기 조정  
 Excel 렌더링 확장 프로그램에서는 페이지 높이 및 너비 설정을 사용하여 Excel 워크시트에 정의할 용지 설정을 결정합니다. Excel에서는 PageHeight 및 PageWidth 속성 설정을 가장 일반적인 용지 크기 중 하나에 맞추려고 시도합니다.  
  
 일치하는 크기를 찾지 못하면 Excel에서는 프린터의 기본 페이지 크기를 사용합니다. 페이지 너비가 페이지 높이보다 작으면 방향이 세로로 설정되고, 그렇지 않으면 방향이 가로로 설정됩니다.  
  
##  <a name="WorksheetTabNames"></a> 워크시트 탭 이름  
 보고서를 Excel로 내보낼 때 페이지 나누기로 만들어진 보고서 페이지는 서로 다른 워크시트로 내보내집니다. 보고서에 초기 페이지 이름을 제공한 경우 Excel 통합 문서의 각 워크시트에는 기본적으로 이 이름이 지정됩니다. 이 이름은 워크시트 탭에 나타납니다. 그러나 통합 문서의 각 워크시트에는 고유한 이름이 있어야 하므로 1에서 시작하고 1씩 증가하는 정수는 각 추가 워크시트의 초기 페이지 이름에 추가됩니다. 예를 들어 초기 페이지 이름이 **Sales Report by Fiscal Year**인 경우 두 번째 워크시트의 이름은 **Sales Report by Fiscal Year1**로 지정되고 세 번째 워크시트의 이름은 **Sales Report by Fiscal Year2**로 지정되는 식으로 이름이 지정됩니다.  
  
 페이지 나누기로 만들어진 모든 보고서 페이지에서 새로운 페이지 이름을 제공하는 경우 각 워크시트에는 연결된 페이지 이름이 지정됩니다. 그러나 이러한 페이지 이름은 고유하지 않을 수 있습니다. 페이지 이름이 고유하지 않은 경우 초기 페이지 이름과 동일한 방식으로 워크시트에 이름이 지정됩니다. 예를 들어 두 그룹의 페이지 이름이 **Sales for NW**인 경우 한 워크시트 탭에는 **Sales for NW**라는 이름이 지정되고 다른 워크시트 탭에는 **Sales for NW1**이라는 이름이 지정됩니다.  
  
 보고서에서 초기 페이지 이름이나 페이지 나누기와 관련된 페이지 이름을 제공하지 않는 경우 워크시트 탭에는 기본 이름 **Sheet1**, **Sheet2**등이 지정됩니다.  
  
 Reporting Services에서는 원하는 방식으로 Excel로 내보낼 수 있는 보고서를 만드는 데 도움이 되도록 보고서, 데이터 영역, 그룹 및 사각형에 대해 설정할 속성을 제공합니다. 자세한 내용은 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)을 참조하세요.  
  
##  <a name="DocumentProperties"></a> 문서 속성  
 Excel 렌더러는 Excel 파일에 다음과 같은 메타데이터를 기록합니다.  
  
|보고서 요소 속성|Description|  
|-------------------------------|-----------------|  
|만든 날짜|보고서 실행 날짜와 시간을 나타내는 ISO 날짜/시간 값입니다.|  
|작성자|Report.Author|  
|Description|Report.Description|  
|LastSaved|보고서 실행 날짜와 시간을 나타내는 ISO 날짜/시간 값입니다.|  
  
##  <a name="PageHeadersFooters"></a> 페이지 머리글 및 바닥글  
 페이지 머리글은 장치 정보 SimplePageHeaders 설정에 따라 각 워크시트 셀 눈금선 위에서 렌더링할 수도 있고, 실제 Excel 워크시트 머리글 섹션에서 렌더링할 수도 있습니다. 기본적으로 머리글은 Excel 워크시트에서 셀 눈금선으로 렌더링됩니다.  
  
 페이지 바닥글은 SimplePageHeaders 설정 값과 상관없이 항상 실제 Excel 워크시트 바닥글 섹션으로 렌더링됩니다.  
  
 Excel 머리글과 바닥글 섹션에는 태그를 포함하여 문자를 최대 256자까지 사용할 수 있습니다. 문자 수가 이보다 많으면 Excel 렌더러에서는 머리글 및/또는 바닥글 문자열의 끝에서부터 태그 문자를 제거하여 전체 문자 수를 줄입니다. 태그 문자를 모두 제거해도 전체 길이가 최대값을 초과하면 오른쪽부터 시작하여 문자열이 잘립니다.  
  
### <a name="simplepageheader-settings"></a>SimplePageHeader 설정  
 기본적으로 장치 정보 SimplePageHeaders 설정은 **False**로 지정되어 있습니다. 따라서 페이지 머리글이 Excel 워크시트 화면에서 보고서의 행으로 렌더링됩니다. 머리글이 들어 있는 워크시트 행은 잠긴 행이 됩니다. Excel에서 창을 고정하거나 고정 해제할 수 있습니다. **인쇄 제목** 옵션을 선택하면 모든 워크시트 페이지에 머리글을 인쇄하도록 자동 설정됩니다.  
  
 Excel의 페이지 레이아웃 탭에서 **인쇄 제목** 옵션을 선택하면 문서 구조 표지를 제외하고 통합 문서의 모든 워크시트 위쪽에 페이지 머리글이 반복하여 표시됩니다. 보고서 머리글 속성 또는 보고서 바닥글 속성 대화 상자에서 **첫 페이지에 인쇄** 또는 **마지막 페이지에 인쇄** 옵션을 선택하지 않은 경우에는 첫 페이지나 마지막 페이지에 각각 머리글이 추가되지 않습니다.  
  
 페이지 바닥글은 Excel 바닥글 섹션에서 렌더링됩니다.  
  
 Excel에 적용되는 제한 사항 때문에 Excel 머리글/바닥글 섹션에서 렌더링할 수 있는 보고서 항목 유형은 입력란으로만 한정됩니다.  
  
##  <a name="Interactivity"></a> 상호 작용  
 Excel에서는 일부 대화형 요소가 지원됩니다. 다음은 특정 동작에 대한 설명입니다.  
  
### <a name="show-and-hide"></a>표시 및 숨기기  
 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 에서 관리하는 방식에는 제약이 따릅니다. 설정/해제할 수 있는 보고서 항목이 들어 있는 그룹, 행 및 열은 Excel 윤곽선으로 렌더링됩니다. Excel에서는 전체 행 또는 열에 걸쳐 행과 열을 확장하거나 축소하는 윤곽선을 만듭니다. 따라서 축소하려고 의도하지 않았던 보고서 항목이 축소될 수도 있습니다. 또한 Excel의 윤곽선 지정 기호가 윤곽선과 겹쳐 화면이 복잡해질 수 있습니다. 이러한 문제를 해결하기 위해 Excel 렌더링 확장 프로그램을 사용할 때는 다음과 같은 윤곽선 지정 규칙이 적용됩니다.  
  
-   설정/해제할 수 있는 보고서 항목이 왼쪽 위 모퉁이에 있으면 Excel에서도 해당 항목을 계속하여 설정/해제할 수 있습니다. 설정/해제할 수 있는 보고서 항목이 왼쪽 위 모퉁이에 있는 설정/해제 가능한 보고서 항목과 가로 또는 세로 공간을 공유하고 있으면 Excel에서 해당 항목을 설정/해제할 수 없습니다.  
  
-   데이터 영역을 행으로 축소할 수 있는지 열로 축소할 수 있는지 결정하기 위해 설정/해제를 제어하는 보고서 항목의 위치와 설정/해제되는 보고서 항목의 위치를 확인합니다. 설정/해제를 제어하는 항목이 설정/해제되는 항목보다 앞에 있으면 항목을 행으로 축소할 수 있습니다. 그렇지 않으면 항목을 열로 축소할 수 있습니다. 설정/해제를 제어하는 항목이 함께 설정/해제되는 영역보다 위나 아래에 있으면 항목이 행으로 렌더링되고 이를 행으로 축소할 수 있습니다.  
  
-   렌더링된 보고서에서 부분합을 배치할 위치를 결정하기 위해 렌더링 확장 프로그램에서는 동적 멤버의 첫째 인스턴스를 확인합니다. 피어 정적 멤버가 바로 위에 있으면 동적 멤버가 부분합으로 간주됩니다. 해당 항목이 요약 데이터임을 가리키는 윤곽선이 설정됩니다. 동적 멤버의 정적 형제가 없으면 멤버의 첫째 인스턴스가 부분합이 됩니다.  
  
-   Excel의 제한 사항 때문에 윤곽선을 최대 7개 수준까지만 중첩할 수 있습니다.  
  
### <a name="document-map"></a>문서 구조  
 보고서에 문서 구조 레이블이 있으면 문서 구조가 렌더링됩니다. 문서 구조는 통합 문서의 첫째 탭 위치에 삽입되는 Excel 표지 워크시트로 렌더링됩니다. 이 워크시트의 이름은 **문서 구조**로 지정됩니다.  
  
 문서 구조에 표시할 텍스트는 보고서 항목이나 그룹의 DocumentMapLabel 속성을 통해 결정됩니다. 문서 구조 레이블은 첫 행의 첫째 열부터 시작하여 보고서에 표시된 것과 같은 순서로 나열됩니다. 각 문서 구조 레이블 셀은 보고서에 표시된 것과 같은 수준 수만큼의 깊이로 들여쓰게 됩니다. 각각의 들여쓰기 수준은 이어지는 열에 레이블을 배치하여 표시됩니다. Excel에서 지원하는 윤곽선 중첩 수준은 최대 256개까지입니다.  
  
 문서 구조 윤곽선은 축소 가능한 Excel 윤곽선으로 렌더링됩니다. 윤곽선 구조는 문서 구조의 중첩 구조와 일치합니다. 윤곽선의 확장 및 축소 상태는 둘째 수준부터 시작합니다.  
  
 구조의 루트 노드는 보고서 이름인 \<*reportname*>.rdl이고 이는 대화형으로 조작할 수 없습니다. 문서 구조 링크 글꼴은 10pt의 Arial입니다.  
  
### <a name="drillthrough-links"></a>드릴스루 링크  
 입력란에 표시되는 드릴스루 링크는 텍스트를 렌더링하는 셀에서 Excel 하이퍼링크로 렌더링됩니다. 이미지와 차트의 드릴스루 링크는 보고서를 렌더링할 때 이미지에 대한 Excel 하이퍼링크로 렌더링됩니다. 드릴스루 링크를 클릭하면 클라이언트의 기본 브라우저가 열리고 대상에 대한 HTML 뷰가 표시됩니다.  
  
### <a name="hyperlinks"></a>하이퍼링크  
 입력란에 표시되는 하이퍼링크는 텍스트를 렌더링하는 셀에서 Excel 하이퍼링크로 렌더링됩니다. 이미지와 차트의 하이퍼링크는 보고서를 렌더링할 때 이미지에 대한 Excel 하이퍼링크로 렌더링됩니다. 하이퍼링크를 클릭하면 클라이언트의 기본 브라우저가 열리고 대상 URL로 이동합니다.  
  
### <a name="interactive-sorting"></a>대화형 정렬  
 Excel에서는 대화형 정렬을 지원하지 않습니다.  
  
### <a name="bookmarks"></a>책갈피  
 입력란의 책갈피 링크는 텍스트를 렌더링하는 셀에서 Excel 하이퍼링크로 렌더링됩니다. 이미지와 차트의 책갈피 링크는 보고서를 렌더링할 때 이미지에 대한 Excel 하이퍼링크로 렌더링됩니다. 책갈피를 클릭하면 책갈피가 설정된 보고서 항목을 렌더링한 위치의 Excel 셀로 이동합니다.  
  
##  <a name="ConditionalFormat"></a> 런타임에 보고서 변경  
 보고서를 여러 형식으로 렌더링해야 하는데 원하는 방식과 필요한 모든 형식으로 렌더링하는 보고서 레이아웃을 만들 수 없는 경우에는 기본 제공 전역 변수인 RenderFormat의 값을 사용하여 런타임에 보고서 모양을 조건부로 변경하는 것이 좋습니다. 이렇게 하면 사용되는 렌더러에 따라 보고서 항목을 숨기거나 표시할 수 있어 각 형식에서 최상의 결과를 얻을 수 있습니다. 자세한 내용은 [기본 제공 Globals 및 Users 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [여러 보고서 렌더링 확장 프로그램의 대화형 기능&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [보고서 항목 렌더링&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
