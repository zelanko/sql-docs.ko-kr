---
title: 동작 변경에 Analysis Services SQL Server 2014의에서 기능 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 92ebd5cb-afb6-4b62-968f-39f5574a452b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 288f9e0d5a86e34db2fdd81163f229eff5275606
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66064343"
---
# <a name="behavior-changes-to-analysis-services-features-in-sql-server-2014"></a>SQL Server 2014 Analysis Services 기능의 동작 변경 내용
  이 항목에서는 다차원, 테이블 형식, 데이터 마이닝 및 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 배포에 대한 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 의 동작 변경 내용을 설명합니다. 동작 변경 내용은 이전 버전의 SQL Server와 비교해서 현재 버전에서 기능이 작동하고 상호 작용하는 방법에 영향을 줍니다.  
  
> [!NOTE]  
>  반면에 새로운 변경은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 과 통합된 데이터 모델 또는 애플리케이션이 실행되지 않게 하는 변경 내용입니다. 자세한 내용은 [Breaking Changes to Analysis Services Features in SQL Server 2014](breaking-changes-to-analysis-services-features-in-sql-server-2014.md)를 참조하십시오.  
  
 항목 내용  
  
-   [SQL Server 2014의에서 동작 변경 내용](#bkmk_sql2014)  
  
-   [SQL Server 2012 SP1의 동작 변경 내용](#bkmk_sql2012sp1)  
  
-   [SQL Server 2012의에서 동작 변경 내용](#bkmk_sql2012)  
  
##  <a name="bkmk_sql2014"></a> 동작 변경 내용 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 이 릴리스에는 테이블 형식, 다차원, 데이터 마이닝 또는 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 기능에 대해 발표된 새로운 동작 변경 내용이 없습니다.  그러나  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 이(가) [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 및 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 버전과 아주 유사하므로 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]에서 업그레이드하는 경우의 편의를 위해 두 이전 릴리스의 동작 변경 내용을 여기에 제공합니다.  
  
##  <a name="bkmk_sql2012sp1"></a> 동작 변경 내용 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]  
 이 섹션에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 의 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]기능에 대해 보고된 동작 변경 내용을 설명합니다. 이러한 변경 내용은 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]에도 적용됩니다.  
  
|문제점|Description|  
|-----------|-----------------|  
|SQL Server 2008 R2 PowerPivot 통합 문서가 SQL Server 2012 SP1 SharePoint 2013용 PowerPivot에서 사용 시 자동으로 업그레이드되지 않고 모델을 새로 고치지 않습니다. 따라서 예약된 데이터 새로 고침이 SQL Server 2008 R2 PowerPivot 통합 문서에 대해 작동하지 않습니다.|2008 R2 통합 문서가 [!INCLUDE[ssGeminiShortvnext](../includes/ssgeminishortvnext-md.md)]에서 열리지만 예약된 새로 고침이 작동하지 않습니다. 새로 고침 기록을 검토하면 다음과 유사한 오류 메시지가 표시됩니다.<br /> "통합 문서는 지원 되지 않는 PowerPivot 모델이 포함 하는 데 사용 합니다. 통합 문서에서 PowerPivot 모델은 SQL Server 2008 R2 PowerPivot for Excel 2010 형식으로 되어 있습니다. 지원되는 PowerPivot 모델은 다음과 같습니다. <br />SQL Server 2012 PowerPivot for Excel 2010<br />SQL Server 2012 PowerPivot for Excel 2013"<br /><br /> **통합 문서 업그레이드 방법:** 통합 문서를 2012 통합 문서로 업그레이드할 때까지 예약 된 새로 고침이 작동 하지 않습니다. 통합 문서와 통합 문서에 포함된 모델을 업그레이드하려면 다음 중 하나를 수행하세요.<br /><br /> 통합 문서를 다운로드하고 SQL Server 2012 PowerPivot for Excel 추가 기능이 설치된 Microsoft Excel 2010에서 통합 문서를 엽니다. 그런 다음 통합 문서를 저장하고 SharePoint 서버에 게시합니다.<br /><br /> 통합 문서를 다운로드하고 Microsoft Excel 2013에서 엽니다. 그런 다음 통합 문서를 저장하고 SharePoint 서버에 게시합니다.<br /><br /> <br /><br /> 통합 문서 업그레이드에 대 한 자세한 내용은 참조 하세요. [통합 문서 업그레이드 및 예약 된 데이터 새로 고침 &#40;SharePoint 2013&#41;](instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)합니다.|  
|DAX [ALL Function](https://msdn.microsoft.com/library/ee634802(v=sql.120).aspx)의 동작 변경 내용입니다.|[!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]이전에는 시간 인텔리전스에 사용하기 위해 날짜 테이블로 표시에서 [Date] 열을 지정할 때 해당 [Date] 열이 ALL 함수에 대한 인수로 전달되고, 그 후 CALCULATE 함수에 대한 필터로 전달되는 경우 날짜 열의 슬라이서에 관계 없이 테이블의 모든 열에 대한 모든 필터가 무시됩니다<br /><br /> 예:<br /><br /> `= CALCULATE (<expression>, ALL (DateTable[Date]))`<br /><br /> [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]이전에는 ALL에 대해 인수로 전달되는 [Date] 열에 관계 없이 DateTable의 모든 열에 대해 모든 필터가 무시됩니다.<br /><br /> [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 및 Excel 2013의 PowerPivot에서 동작은 ALL에 대해 인수로 전달된 특정 열에 대해서만 필터를 무시합니다.<br /><br /> 새로운 동작의 문제를 해결하려면 사실상 모든 열을 전체 테이블의 필터로 무시하고 인수에서 [Date] 열을 제외할 수 있습니다. 예를 들어<br /><br /> `=CALCULATE (<expression>, ALL(DateTable))`<br /><br /> 이렇게 하면 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]이전의 동작과 동일한 결과가 반환됩니다.|  
  
##  <a name="bkmk_sql2012"></a> 동작 변경 내용 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 이 섹션에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 의 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]기능에 대해 보고된 동작 변경 내용을 설명합니다. 이러한 변경 내용은 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]에도 적용됩니다.  
  
### <a name="analysis-services-multidimensional-mode"></a>Analysis Services, 다차원 모드  
  
#### <a name="nullprocessing-option-set-to-preserve-is-no-longer-supported-for-distinct-count-measures"></a>Preserve로 설정된 NullProcessing 옵션은 고유 카운트 측정값에 대해 더 이상 지원되지 않습니다.  
 이전에 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]를 설정할 수 있었습니다 [NullProcessing 요소 &#40;ASSL&#41; ](https://docs.microsoft.com/bi-reference/assl/properties/nullprocessing-element-assl) 하 `Preserve` 고유 카운트 측정값에 대 한 합니다.  아쉽게도 이 방법으로 인해 종종 잘못된 결과가 생기고 처리 작업이 중단되기도 했습니다. 결과적으로 이 구성은 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서 더 이상 유효하지 않습니다. 사용 하려고 하면 다음 유효성 검사 오류를 발생 합니다. "메타 데이터 관리자에 오류가 있습니다. Preserve는 적합 한 NullProcessing 값 아닙니다는 \<measurename > 고유 카운트 측정값입니다. "  
  
#### <a name="cube-browser-in-management-studio-and-cube-designer-has-been-removed"></a>Management Studio 및 큐브 디자이너에서 큐브 브라우저가 제거됨  
 필드를 Management Studio 또는 큐브 디자이너의 피벗 테이블 구조로 끌어서 놓을 수 있는 큐브 브라우저 컨트롤이 제품에서 제거되었습니다. 이 컨트롤은 OWC(Office Web Control) 구성 요소였습니다. OWC는 Office에서 사용되지 않으며 이제 더 이상 지원되지 않습니다.  
  
### <a name="powerpivot-for-sharepoint"></a>SharePoint용 PowerPivot  
  
#### <a name="higher-permission-requirements-for-using-a-powerpivot-workbook-as-an-external-data-source"></a>PowerPivot 통합 문서를 외부 데이터 원본으로 사용하기 위해서는 더 높은 권한이 필요함  
 Excel 통합 문서에서는 동일한 통합 문서 내에 포함되거나 외부 통합 문서에 있는 PowerPivot 데이터를 렌더링할 수 있습니다. 이전 릴리스에서는 PowerPivot 데이터가 포함되어 있는지 외부에 있는지에 관계없이 사용 권한 요구 사항이 동일했습니다. 따라서 PowerPivot 통합 문서에 대한 **보기만** 권한이 있으면 포함된 연결과 외부 연결 모두에 대해 통합 문서의 모든 PowerPivot 데이터에 액세스할 수 있었습니다.  
  
 이번 릴리스에서는 외부 파일의 PowerPivot 데이터를 렌더링하는 Excel 통합 문서에 대한 사용 권한 요구 사항이 변경되었습니다. 이번 릴리스에서는 클라이언트 애플리케이션에서 외부 PowerPivot 통합 문서에 연결하려면 **읽기** 권한(보다 구체적으로는 **항목 열기** 권한)이 있어야 합니다. 추가 권한은 통합 문서에 포함된 원본 데이터를 보기 위한 다운로드 권한을 사용자에게 부여하도록 지정합니다. 추가 권한은 모델 데이터에 연결하는 클라이언트 애플리케이션이나 통합 문서에서 모델 데이터를 전체적으로 사용할 수 있다는 사실을 반영하므로 사용 권한 요구 사항과 실제 데이터 연결 동작을 보다 잘 조정할 수 있습니다.  
  
 PowerPivot 통합 문서를 외부 데이터 원본으로 계속 사용하려면 외부 PowerPivot 데이터에 연결할 사용자의 SharePoint 권한을 높여야 합니다. 권한을 변경 될 때까지 데이터 원본 연결에서 PowerPivot 통합 문서에 액세스 하려고 할 때 사용자가 다음과 같은 오류가 표시 됩니다. "PowerPivot 웹 서비스 (액세스가 거부 되었습니다 오류를 반환 했습니다. 요청한 문서가 없거나 파일을 열 권한이 없습니다.) "  
  
> [!WARNING]  
>  다음 단계에서는 라이브러리 수준에서 권한 상속을 중단하고 이 라이브러리의 특정 문서에 대해 사용자의 권한을 **보기만** 에서 **읽기** 로 높이는 방법을 설명합니다. 계속 진행하기 전에 기존 사용 권한 및 설명을 신중하게 검토하고 이러한 단계가 자신의 사이트에 적합한지 확인합니다.  
>   
>  또는 라이브러리에서 폴더를 만들고 해당 문서를 모두 해당 폴더로 이동하고, 폴더에 대해 고유한 사용 권한을 설정합니다.  
  
> [!NOTE]  
>  통합 문서가 PowerPivot 갤러리에 저장된 경우 통합 문서에 대한 권한 상속을 중단하면 데이터 새로 고침이 구성된 통합 문서에 대한 축소판 이미지 생성이 중단됩니다. 갤러리에서 통합 문서 및 미리 보기 이미지에 대한 액세스를 동시에 허용하려면 라이브러리의 모든 문서에 대해 라이브러리 수준에서 특정 사용자에게 **읽기** 권한을 부여하는 것을 고려할 수 있습니다.  
  
 사용 권한을 변경하려면 사이트 소유자여야 합니다.  
  
 **읽기 권한 수준 개별 통합 문서에 대 한 사용 권한을 늘리는 방법**  
  
1.  개별 문서의 메뉴를 열려면 아래쪽 화살표를 클릭합니다.  
  
2.  **사용 권한 관리**를 클릭합니다.  
  
3.  기본적으로 라이브러리는 사용 권한을 상속합니다. 이 라이브러리에서 개별 통합 문서의 사용 권한을 변경하려면 **권한 상속 중지**를 클릭합니다.  
  
4.  PowerPivot 통합 문서에 대한 추가 사용 권한이 필요한 사용자 또는 그룹 이름에 해당하는 확인란을 선택합니다. 추가 사용 권한은 이러한 사용자가 포함된 PowerPivot 데이터에 연결하고 해당 데이터를 다른 문서에서 외부 데이터 원본으로 사용할 수 있도록 허용합니다.  
  
5.  **사용자의 사용 권한 편집**을 클릭합니다.  
  
6.  **읽기** 권한을 선택한 다음 **확인**을 클릭합니다.  
  
#### <a name="powerpivot-gallery-new-rules-for-snapshot-generation-for-some-powerpivot-workbooks"></a>PowerPivot 갤러리: 일부 PowerPivot 통합 문서에 대 한 스냅숏 생성에 대 한 새 규칙  
 이 릴리스에는 PowerPivot 갤러리에서 스냅숏 이미지를 생성하고, 정보 출처를 노출할 가능성(즉, 보기 권한이 없는 데이터 원본의 데이터 스냅숏을 표시할 수 있는 가능성)을 없애기 위한 새로운 요구 사항이 도입되었습니다. 이러한 요구 사항은 통합 문서를 볼 때마다 외부 데이터 원본에 연결하는 PowerPivot 통합 문서에만 적용됩니다. 포함된 PowerPivot 데이터를 시각화하는 통합 문서만 사용할 경우 PowerPivot 갤러리에서 스냅숏이 생성되는 방식에서 변경된 점을 확인할 수 없습니다.  
  
 열 때마다 데이터를 새로 고치는 통합 문서의 경우 스냅숏 생성을 위한 새로운 요구 사항은 다음과 같습니다.  
  
-   다른 통합 문서 또는 보고서에서 외부 데이터 원본으로 사용되는 PowerPivot 통합 문서는 데이터를 소비하는 통합 문서와 동일한 라이브러리에 있어야 합니다. 예를 들어 sales-report.xlsx에 데이터를 제공하는 sales-data.xlsx가 있는 경우 스냅숏 이미지를 표시하려면 두 통합 문서 모두 동일한 갤러리에 있어야 합니다.  
  
-   함께 사용되는 통합 문서는 공통된 부모(즉, PowerPivot 갤러리)로부터 권한을 상속해야 합니다. 이 예제에서 sales-data.xlsx 및 sales-report.xlsx는 PowerPivot 갤러리로부터 상속해야 합니다.  
  
 통합 문서가 위 조건 중 하나라도 충족하지 못하면 정상적인 축소판 이미지 대신 다음과 같은 잠금 아이콘이 표시됩니다.  
  
 ![GMNI_PowerPivotGalleryIcon_Locked](media/gmni-powerpivotgalleryicon-locked.gif "GMNI_PowerPivotGalleryIcon_Locked")  
  
#### <a name="new-default-setting-for-load-balancing-requests-changed-from-round-robin-to-health-based"></a>부하 분산 요청에 대한 새 기본 설정이 라운드 로빈에서 상태 기반으로 변경됨  
 PowerPivot 서비스 애플리케이션에는 PowerPivot 데이터에 대한 요청이 팜의 여러 SharePoint용 PowerPivot 서비스에서 분산되는 방식을 결정하는 기본 설정이 포함됩니다. 이전 릴리스에서 기본 설정은 요청이 사용 가능한 서버 간에 순차적으로 분산되는 **라운드 로빈**이었습니다. 이 릴리스에서는 기본값이 **상태 기반**입니다. PowerPivot 서비스 애플리케이션에서는 사용 가능한 메모리 또는 CPU와 같은 서버 상태 통계를 사용하여 xt 요청을 가져올 서버 인스턴스를 결정합니다.  
  
 서버를 이전 릴리스로부터 업그레이드한 경우 PowerPivot 서비스 애플리케이션에는 이전의 기본 설정(**라운드 로빈**)이 보존됩니다. **상태 기반** 할당 방법을 사용하려면 구성 설정을 수정해야 합니다. 자세한 내용은 [만들고 중앙 관리에서 PowerPivot 서비스 응용 프로그램 구성](power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [이전 버전과의 호환성](../../2014/getting-started/backward-compatibility.md)   
 [SQL Server 2014의에서 기능을 서비스의 주요 변경 내용 분석](breaking-changes-to-analysis-services-features-in-sql-server-2014.md)  
  
  
