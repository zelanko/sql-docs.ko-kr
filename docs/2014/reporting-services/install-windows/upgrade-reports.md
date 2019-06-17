---
title: 보고서 업그레이드 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], upgrading
- published reports [Reporting Services], upgrades
- custom report items, upgrading
- Reporting Services, upgrades
- upgrading Reporting Services
- snapshots [Reporting Services], upgrading
- report definition files [Reporting Services]
- .rdl files
ms.assetid: a1a10c67-7462-4562-9b07-a8822188a161
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8f97567188cc3c1f4e4082be1c4c1378ca97122f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108603"
---
# <a name="upgrade-reports"></a>Upgrade Reports
  보고서 정의 파일(.rdl)은 다음과 같은 방법으로 자동 업그레이드됩니다.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 보고서 디자이너에서 보고서를 열면 보고서 정의가 현재 지원되는 RDL 스키마로 업그레이드됩니다. 프로젝트 속성에 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 보고서 서버를 지정하면 보고서 정의는 대상 서버와 호환되는 스키마에 저장됩니다.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치를 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 설치로 업그레이드한 경우 보고서 서버에 게시된 기존 보고서 및 스냅숏은 처음 처리되는 시점에서 새 스키마로 컴파일되고 자동으로 업그레이드됩니다. 자동으로 업그레이드할 수 없는 보고서는 이전 버전 호환 모드를 사용하여 처리됩니다. 보고서 정의는 원래 스키마에 유지됩니다.  
  
 보고서 정의 파일을 보고서 서버 또는 SharePoint 사이트에 직접 업로드하는 경우에는 보고서가 업그레이드되지 않습니다. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 에서 보고서 정의를 업그레이드해야만 .rdl 파일을 업그레이드할 수 있습니다.  
  
 로컬 또는 보고서 서버에서 보고서를 업그레이드한 후 추가적인 오류, 경고 및 메시지가 나타날 수 있습니다. 이것은 내부 보고서 개체 모델 및 처리 구성 요소가 변경됨에 따라 보고서에서 근본적인 문제를 감지하고 메시지를 표시하기 때문입니다. 자세한 내용은 [Reporting Services Backward Compatibility](../reporting-services-backward-compatibility.md)을 참조하세요.  
  
 에 대 한 새 기능에 대 한 자세한 내용은 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]를 참조 하세요 [새로운 &#40;Reporting Services&#41;](../what-s-new-reporting-services.md)합니다.  
  
 항목 내용  
  
-   [업그레이드 가능한 버전](#bkmk_versionsupported)  
  
-   [보고서 정의 파일(.rdl) 및 보고서 디자이너](#bkmk_rdlfiles)  
  
-   [게시된 보고서 및 보고서 스냅숏](#bkmk_publishedreports_and_snapshots)  
  
-   [이전 버전 호환 모드](#bkmk_backcompat)  
  
-   [하위 보고서가 있는 보고서 업그레이드](#bkmk_subreports)  
  
-   [사용자 지정 보고서 항목이 있는 보고서 업그레이드](#bkmk_CRIs)  
  
-   [CRI 변환 대화 상자](#bkmk_convertCRIdialog)  
  
##  <a name="bkmk_versionsupported"></a> 업그레이드 가능한 버전  
 이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 만든 보고서는 업그레이드할 수 있습니다. 여기에는 다음과 같은 버전이 포함됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 서비스 팩 1  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 서비스 팩 2  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
##  <a name="bkmk_rdlfiles"></a> 보고서 정의 파일(.rdl) 및 보고서 디자이너  
 보고서 정의 파일에는 .rdl 파일의 유효성을 검사하는 데 사용되는 보고서 정의 스키마의 버전을 지정하는 RDL 네임스페이스에 대한 참조가 포함되어 있습니다.  
  
 이전 네임스페이스용으로 만든 보고서의 .rdl 파일을 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 보고서 디자이너에서 열면 자동으로 백업 파일이 만들어지고 보고서가 현재 네임스페이스로 업그레이드됩니다. 이 방법은 보고서 정의 파일을 업그레이드할 수 있는 유일한 방법입니다.  
  
 설정한 배포 속성은 보고서 정의 파일이 저장된 스키마에 영향을 줄 수 있습니다. 자세한 내용은 [SQL Server Data Tools의 배포 및 버전 지원&#40;SSRS&#41;](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)을 참조하세요.  
  
 이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 만든 .rdl 파일을 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 보고서 서버에 업로드할 수 있으며 이러한 파일은 처음 사용할 때 자동으로 업그레이드됩니다. 보고서 서버는 보고서 정의 파일을 원래 형식으로 저장합니다. 보고서는 처음 볼 때 자동으로 업그레이드되지만 저장된 보고서 정의 파일은 변경되지 않은 상태로 유지됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 보고서 정의 네임스페이스가 있는 보고서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 보고서 서버에 게시하거나 업로드할 수 없습니다.  
  
 보고서, 보고서 서버 또는 보고서 디자이너에 대한 현재 RDL 스키마를 확인하려면 [보고서 정의 스키마 버전 찾기&#40;SSRS&#41;](../reports/find-the-report-definition-schema-version-ssrs.md)를 참조하세요.  
  
##  <a name="bkmk_publishedreports_and_snapshots"></a> 게시된 보고서 및 보고서 스냅숏  
 처음 사용할 때 보고서 서버는 게시된 기존 보고서와 보고서 스냅숏을 새 보고서 정의 스키마로 업그레이드하려고 합니다. 이때 사용자는 특정 동작을 수행할 필요가 없습니다. 이러한 업그레이드 시도는 사용자가 보고서 또는 보고서 스냅숏을 보거나 보고서 서버에서 구독을 처리할 때 수행됩니다. 보고서 정의는 대체되지 않고 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 보고서 서버의 원래 스키마에 계속 저장됩니다. 업그레이드할 수 없는 보고서는 이전 버전 호환 모드에서 실행됩니다.  
  
##  <a name="bkmk_backcompat"></a> 이전 버전 호환 모드  
 성공적으로 업그레이드된 보고서는 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 보고서 처리기를 사용하여 처리되고 업그레이드할 수 없는 보고서를 처리 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 처리기의 이전 버전과 호환성 모드입니다. 하나의 보고서를 이 두 보고서 처리기에서 모두 처리할 수는 없습니다. 처음 사용할 때 보고서는 업그레이드되거나 이전 버전 호환으로 표시됩니다.  
  
 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 보고서 처리기만 새 기능을 지원합니다. 보고서를 업그레이드할 수 없는 경우에도 렌더링된 보고서를 계속 볼 수는 있지만 새 기능을 사용할 수는 없습니다. 새 기능을 사용하려면 보고서를 성공적으로 업그레이드해야 합니다.  
  
##  <a name="bkmk_subreports"></a> 하위 보고서가 있는 보고서 업그레이드  
 보고서에 하위 보고서가 있는 경우 업그레이드하는 동안 다음과 같은 네 가지 상황 중 하나가 발생할 수 있습니다.  
  
-   주 보고서와 모든 하위 보고서를 성공적으로 업그레이드할 수 있습니다. 이러한 보고서는 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 보고서 처리기를 사용하여 처리됩니다.  
  
-   주 보고서와 모든 하위 보고서를 업그레이드할 수 없습니다. 이러한 보고서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 처리기를 사용하여 처리됩니다.  
  
-   주 보고서는 업그레이드할 수 있지만 하나 이상의 하위 보고서를 업그레이드할 수 없습니다. 주 보고서에서 처리 되는 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 보고서 처리기를 되지만 렌더링된 된 보고서 메시지를 보여 줍니다. "오류: 하위 보고서가 처리할 수 없습니다 "업그레이드할 수 없습니다. 하위 보고서가 나타나는 위치에 있습니다.  
  
-   주 보고서를 업그레이드할 수 없지만 하나 이상의 하위 보고서는 업그레이드할 수 있습니다. 주 보고서에서 처리 되는 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 보고서 처리기를 되지만 렌더링된 된 보고서 메시지를 보여 줍니다. "오류: 하위 보고서가 처리할 수 없습니다 "경우 하위 보고서가 나타나는 위치에 있습니다.  
  
 오류를 표시 하는 경우 "오류: 하위 보고서를 처리할 수 없습니다", 동일한 버전의 보고서 처리기에서 보고서를 처리할 수 있도록 주 보고서 또는 하위 보고서의 정의 변경 해야 합니다.  
  
 드릴스루 보고서는 독립적인 보고서로 처리되므로 이러한 제한이 없습니다.  
  
##  <a name="bkmk_CRIs"></a> 사용자 지정 보고서 항목이 있는 보고서 업그레이드  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서에는 타사 소프트웨어 공급업체에서 제공하고 보고서 작성 컴퓨터 및 보고서 서버의 시스템 관리자가 설치한 CRI(사용자 지정 보고서 항목)가 포함될 수 있습니다. CRI가 포함된 보고서는 다음과 같은 방법으로 업그레이드할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버는 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 보고서 서버로 업그레이드됩니다. 보고서 서버에 게시된 보고서는 처음 사용할 때 자동으로 업그레이드됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서는 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 보고서 서버로 업로드됩니다. 보고서는 처음 사용할 때 자동으로 업그레이드됩니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서를 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 보고서 디자이너에서 엽니다. 원본 보고서의 백업 복사본이 만들어집니다. 다음 두 가지 경우 중 하나가 발생합니다.  
  
    1.  보고서에 있는 모든 CRI에 지원되지 않는 기능이 포함되어 있지 않습니다. CRI가 새 보고서 정의 스키마의 보고서 항목으로 변환되어 전체 보고서가 업그레이드됩니다. 이 파일을 저장하면 현재 RDL 네임스페이스에 저장됩니다.  
  
    2.  보고서에 있는 하나 이상의 CRI에 지원되지 않는 기능이 포함되어 있습니다. CRI를 변경할지 아니면 변경하지 않고 유지할지 묻는 대화 상자가 나타납니다.  
  
     자세한 내용은 이 항목의 뒷부분에 나오는 [보고서 디자이너에서 CRI가 있는 보고서 열기](#OpeningaReport) 를 참조하세요.  
  
 보고서 서버, [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 또는 보고서의 현재 RDL 네임스페이스를 확인하는 방법은 [보고서 정의 스키마 버전 찾기&#40;SSRS&#41;](../reports/find-the-report-definition-schema-version-ssrs.md)를 참조하세요.  
  
### <a name="upgrading-reports-on-a-report-server"></a>보고서 서버에서 보고서 업그레이드  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보고서 서버로 업그레이드된 보고서 서버에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 2005 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 보고서를 처음으로 실행하면 보고서가 자동으로 보고서 서버에서 지원하는 현재 보고서 정의 네임스페이스로 업그레이드됩니다. 보고서는 업그레이드 전의 보고서 서버에 있을 수 있습니다. 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 보고서 디자이너에서 보고서 서버로 게시되거나 보고서 관리자를 통해 업로드될 수 있습니다.  
  
 다음 표에서는 보고서 서버에서 보고서에 있는 특정 유형의 CRI에 대해 수행하는 업그레이드 동작을 보여 줍니다.  
  
|CRI 유형|보고서 서버 업그레이드 동작|  
|--------------|----------------------------------|  
|타사 CRI|업그레이드가 수행되지 않습니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 처리기를 사용하여 처리됩니다.|  
|지원되지 않는 기능이 없는 Dundas 2005 Chart CRI|최신 RDL 스키마로 업그레이드됩니다. 모든 Dundas 2005 Chart CRI가 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]와 호환되는 차트 데이터 영역으로 변환됩니다.<br /><br /> [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 보고서 처리기를 사용하여 처리됩니다.|  
|지원되지 않는 기능이 없는 Dundas 2005 Gauge CRI|최신 RDL 스키마로 업그레이드됩니다. 모든 Dundas 2005 Gauge CRI가 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]와 호환되는 게이지 데이터 영역으로 변환됩니다.<br /><br /> [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 보고서 처리기를 사용하여 처리됩니다.|  
|지원되지 않는 기능이 있는 Dundas 2005 Chart CRI|업그레이드가 수행되지 않습니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 처리기를 사용하여 처리됩니다.|  
|지원되지 않는 기능이 있는 Dundas 2005 Gauge CRI|업그레이드가 수행되지 않습니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 처리기를 사용하여 처리됩니다.|  
  
###  <a name="OpeningaReport"></a> 보고서 디자이너에서 CRI가 있는 보고서 열기  
 여는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 보고서 디자이너에서 cri가 있는 보고서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]는 보고서가 새 보고서 정의 스키마로 업그레이드 됩니다. 보고서에 있는 CRI에 따라 다음 동작 중 하나가 수행됩니다.  
  
-   타사 CRI가 검색됩니다. 보고서 작성 컴퓨터에 설치된 CRI 버전이 새 RDL 스키마와 호환되지 않으면 디자인 화면에 빨간 X가 있는 입력란이 표시됩니다. 새 RDL 스키마와 호환되는 타사 공급업체의 새 CRI 버전을 설치하려면 시스템 관리자에게 문의해야 합니다.  
  
-   Dundas 2005 Chart 또는 Gauge CRI가 검색되고 모든 인스턴스에 지원되는 기능이 포함되어 있습니다. 모든 Dundas 2005 Chart 및 Gauge CRI가 도구 상자에 표시되는 Reporting Services 차트 및 계기 보고서 항목으로 변환됩니다. 이러한 항목을 기본 차트 및 계기 보고서 항목이라고 합니다.  
  
-   Dundas 2005 Chart 또는 Gauge CRI가 검색되고 일부 인스턴스에 지원되지 않는 기능이 포함되어 있습니다. 지원되지 않는 기능은 이 섹션 다음에 설명되어 있습니다. 모든 CRI를 기본 보고서 항목으로 변환할지 여부를 선택할 수 있습니다.  
  
    -   CRI를 변환하면 보고서가 새 RDL 스키마로 업그레이드되고 Dundas 2005 Chart 및 Gauge CRI가 해당 기본 차트 및 계기 보고서 항목으로 변환되지만 지원되지 않는 기능은 제거됩니다. 렌더링된 보고서에서는 CRI가 이와 다른 방식으로 표시될 수 있습니다.  
  
    -   CRI를 변환하지 않도록 선택하면 보고서가 새 RDL 스키마로 업그레이드되지만 CRI가 타사 CRI로 처리됩니다. 새 RDL 보고서 스키마와 호환되는 새 CRI를 설치하려면 시스템 관리자와 타사 공급업체의 도움이 필요합니다. 새 CRI를 사용할 수 없으면 보고서 디자이너에 빨간 X가 있는 입력란이 표시됩니다.  
  
 기존 보고서를 새 보고서 정의 스키마로 업그레이드하는 유일한 방법은 보고서를 업그레이드한 후 보고서 작성 환경에 저장하는 것입니다.  
  
### <a name="unsupported-dundas-2005-chart-custom-report-item-functionality"></a>지원되지 않는 Dundas 2005 Chart 사용자 지정 보고서 항목 기능  
 다음은 Dundas 2005 Chart CRI에 대해 지원되지 않는 기능입니다.  
  
-   주석  
  
-   사용자 지정 범례 항목  
  
-   다음과 같은 이름의 사용자 지정 특성  
  
    -   CUSTOM_CODE_CS  
  
    -   CUSTOM_CODE_VB  
  
    -   CUSTOM_CODE_COMPILED_ASSEMBLY  
  
         예를 들어 .rdl 파일에 다음 섹션이 포함되어 있으면 업그레이드하기 전에 이를 제거해야 합니다.  
  
        ```  
        <CustomProperty>  
         <Name>CUSTOM_CODE_CS</Name>  
         <Value>dXNpWERwegfdfgiobxxl3bmc... </Value>  
        </CustomProperty>  
        ```  
  
### <a name="unsupported-dundas-2005-gauge-custom-report-item-functionality"></a>지원되지 않는 Dundas 2005 Gauge 사용자 지정 보고서 항목 기능  
 다음은 Dundas 2005 Gauge CRI에 대해 지원되지 않는 기능입니다.  
  
-   숫자 표시기  
  
-   상태 표시기  
  
-   사용자 지정 이미지  
  
###  <a name="bkmk_convertCRIdialog"></a> CRI 변환 대화 상자  
 이 보고서에는 지원되지 않는 기능이 있는 CRI(사용자 지정 보고서 항목)가 포함되어 있습니다. CRI는 보고서에 데이터를 표시하는 사용자 지정 개체를 지원하는 RDL(Report Definition Language)에 대한 확장입니다. CRI에는 타사 소프트웨어 공급업체에서 제공하는 디자인 타임 및 런타임 구성 요소가 포함되어 있습니다.  
  
> [!NOTE]  
>  보고서 서버에서 사용자 지정 항목을 지원하도록 선택하는 것은 시스템 관리자가 결정할 일입니다. 보고서에서 CRI를 보려는 경우 보고서를 미리 보려면 보고서 제작 클라이언트에 CRI 구성 요소를 설치해야 하고 게시 또는 업로드된 보고서를 보려면 보고서 서버에 CRI 구성 요소를 설치해야 합니다. 자세한 내용은 [사용자 지정 보고서 항목](../custom-report-items/custom-report-items.md) 및 타사 소프트웨어 공급업체의 설명서를 참조하세요.  
  
 일부 CRI를 새 보고서 정의 형식의 보고서 항목으로 변환할 수 있습니다. 변환할 수 있는 CRI 목록은 [Upgrading Reports](upgrade-reports.md)를 참조하세요. 다음 목록을 사용하여 이 보고서에서 CRI를 변환할지 여부를 결정할 수 있습니다.  
  
-   **예** 가능한 경우 보고서의 모든 CRI를 변환하려면 **예** 를 선택합니다. CRI에서 지원하지 않는 기능은 업그레이드할 수 없으며 보고서 정의 파일에서 제거됩니다. 지원하지 않는 기능 목록은 [Upgrading Reports](upgrade-reports.md)를 참조하세요. 보고서를 볼 때 CRI가 보고서에 다른 방식으로 표시될 수 있습니다.  
  
-   **아니요** 보고서에서 CRI를 변환하지 않으려면 **아니요** 를 선택합니다. 이러한 CRI는 현재 버전의 보고서 처리기에서는 표시할 수 없습니다. 시스템 관리자가 새 보고서 정의 형식과 호환되는 타사 소프트웨어 공급업체가 제공하는 새 버전의 CRI를 설치하려는 경우에는 **아니요**를 선택해야 합니다. 새 버전을 사용할 수 있을 때까지 보고서에 CRI가 빨간색 X가 있는 비어 있는 입력란으로 표시됩니다.  
  
 두 경우 모두 보고서는 새 보고서 정의 형식으로 업그레이드되며 원래 보고서의 백업 복사본은 *\<보고서 이름>* `-` Backup.rdl로 저장됩니다. 보고서를 보고서 작성 도구에 저장하는 경우 업그레이드된 보고서가 새 보고서 정의 형식으로 저장됩니다. 보고서를 게시하는 경우 보고서는 컴퓨터에 먼저 저장된 다음 보고서 서버에 게시됩니다. 업그레이드된 버전의 보고서가 보고서 서버에 게시됩니다.  
  
 보고서를 저장하지 않는 경우 원래 보고서가 그대로 유지됩니다. 그러나 이 보고서를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 의 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 버전이나 최신 보고서 정의 형식을 사용하는 보고서 제작 환경에서 편집할 수는 없습니다. 보고서 관리자를 사용하여 보고서를 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 보고서 서버로 업로드하여 원래 버전의 보고서를 계속 실행할 수 있습니다. 자세한 내용은 [파일 또는 보고서 업로드&#40;보고서 관리자&#41;](../reports/upload-a-file-or-report-report-manager.md)를 참조하세요.  
  
 보고서 서버에 게시하는 대신 보고서를 업로드하는 경우 보고서 처리기가 처음 사용 시 보고서 업그레이드 가능 여부를 결정합니다. 업그레이드가 불가능한 보고서는 이전 버전과의 호환성 모드에서 처리되며 계속해서 이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]로 표시됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 업그레이드 및 마이그레이션](upgrade-and-migrate-reporting-services.md)   
 [SQL Server 2014에서에서 SQL Server Reporting Services의 주요 변경 내용](../breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)   
 [SQL Server 2014에서에서 SQL Server Reporting Services 동작 변경 내용](../behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [SQL Server 2014에서에서 SQL Server Reporting Services에 지원 되지 않는 기능](../discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)   
 [사용자 지정 보고서 항목](../custom-report-items/custom-report-items.md)   
 [보고서 서버 데이터베이스 업그레이드](upgrade-a-report-server-database.md)  
  
  
