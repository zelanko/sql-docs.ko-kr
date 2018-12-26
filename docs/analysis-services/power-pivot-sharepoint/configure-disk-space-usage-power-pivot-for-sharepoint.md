---
title: 디스크 공간 사용 (SharePoint 용 파워 피벗) 구성 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 24d96feb0e57bf0b1c62532cca63ddf07f96f21c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34024750"
---
# <a name="configure-disk-space-usage-power-pivot-for-sharepoint"></a>디스크 공간 사용 구성(SharePoint용 Power Pivot)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 배포에서는 더욱 빠르게 다시 로드하기 위해 호스트 컴퓨터의 디스크 공간을 사용하여 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스를 캐시합니다. 메모리에 로드되는 각 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스는 이후에 새 요청을 처리하기 위해 신속하게 다시 로드될 수 있도록 디스크에 먼저 캐시됩니다. 기본적으로 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 에서는 사용 가능한 모든 디스크 공간을 사용하여 해당 데이터베이스를 캐시하지만 사용되는 디스크 공간 크기를 제한하는 속성을 설정하여 이 동작을 수정할 수 있습니다.  
  
 이 항목에서는 디스크 공간 사용량에 대한 제한을 설정하는 방법에 대해 설명합니다.  
  
 이 항목에서는 콘텐츠 데이터베이스에 저장된 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스(Excel 통합 문서에 포함됨)의 디스크 공간 관리에 대한 지침을 제공하지 않습니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스는 크기가 클 수 있으므로 팜의 저장 용량이 많이 필요할 수 있습니다. 또한 버전 관리를 사용하는 경우 동일한 콘텐츠 데이터베이스에 데이터의 복사본이 여러 개 있을 수 있으므로 콘텐츠 저장에 필요한 디스크 공간의 크기가 더 늘어날 수 있습니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스가 디스크 관리에서 중요한 고려 대상이긴 하지만 SharePoint 팜에 저장하는 다른 콘텐츠와 독립적으로 관리될 수 있지는 않습니다. 기업에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서의 사용이 늘어나면 디스크 공간을 더욱 자세히 모니터링해야 합니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 관리 대시보드에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서 활동을 추적하고 더 이상 사용되지 않는 통합 문서를 제거할 수도 있습니다.  
  
## <a name="how-power-pivot-for-sharepoint-manages-cached-databases"></a>SharePoint용 Power Pivot에서 캐시된 데이터베이스를 관리하는 방법  
 캐시를 관리하기 위해 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스는 일정한 간격으로 백그라운드 작업을 실행하여 콘텐츠 라이브러리에 최신 버전이 있는 사용되지 않거나 오래된 데이터베이스를 정리합니다. 정리 작업의 목적은 메모리에서 비활성 데이터베이스를 언로드하고 파일 시스템에서 사용하지 않는 캐시된 데이터베이스를 삭제하는 것입니다. 정리 작업은 장기적인 유지 관리를 위해 수행되며 데이터베이스가 시스템에 무기한 남아 있지 않도록 합니다. 활성 서버에서 데이터베이스는 서버의 메모리 부족, SharePoint에서의 데이터베이스 삭제 또는 콘텐츠 라이브러리에 있는 최신 버전의 데이터베이스로 인해 더 자주 제거될 수 있습니다.  
  
 정리 작업은 예약할 수 없지만 다음을 수행하는 서버 구성 속성을 설정하여 캐시 파일 관리를 사용자 지정할 수 있습니다.  
  
-   캐시에 사용되는 디스크 공간의 크기에 대한 제한을 설정합니다.  
  
-   최대 디스크 공간에 도달하는 경우 삭제할 데이터 크기를 지정합니다.  
  
## <a name="how-to-check-disk-space-usage"></a>디스크 공간 사용량을 확인하는 방법  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 은 SharePoint 팜의 응용 프로그램 서버에 설치됩니다. 각 설치에는 백업 폴더가 포함된 데이터 디렉터리가 있습니다. 백업 폴더에는 컴퓨터의 Analysis Services 인스턴스에 의해 캐시되는 모든 데이터 파일이 들어 있습니다. 기본적으로 백업 폴더는 다음 경로에서 찾을 수 있습니다.  
  
 `%drive%:\Program Files\Microsoft SQL Server\MSAS10_50.PowerPivot\OLAP\Backup\Sandboxes\<serviceApplicationName>`  
  
 캐시에 사용되는 총 디스크 공간의 크기를 확인하려면 백업 폴더의 크기를 확인해야 합니다. 중앙 관리에는 현재 캐시 크기에 대해 보고하는 속성이 없습니다.  
  
 백업 폴더는 로컬 컴퓨터의 메모리에 로드되는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스에 대한 공통 캐시 저장소를 제공합니다. 팜에 여러 개의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 애플리케이션이 정의되어 있는 경우 그 중 한 애플리케이션이 로컬 서버를 사용하여 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터를 로드하고 이후에 해당 데이터를 캐시할 수 있습니다. 데이터 로드 및 캐시 모두 Analysis Services 서버 작업입니다. 따라서 총 디스크 공간 사용량은 Analysis Services 인스턴스 수준에서 백업 폴더에 대해 관리됩니다. 따라서 디스크 공간 사용량을 제한하는 구성 설정은 SharePoint 애플리케이션 서버에서 실행되는 SQL Server Analysis Services 인스턴스에 대해 설정됩니다.  
  
 캐시에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스만 포함됩니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스는 단일 부모 폴더(백업 폴더) 아래의 여러 파일에 저장됩니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스가 Excel 통합 문서의 내부 데이터로 사용되기 때문에 데이터베이스 이름은 설명이 포함되지 않은 GUID 기반 이름입니다. 아래의 GUID 폴더  **\<serviceApplicationName >** 의 부모 폴더는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스입니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스가 서버에 로드되면 각 데이터베이스에 대한 추가 폴더가 만들어집니다.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터가 팜의 모든 Analysis Services 인스턴스에 로드될 수 있기 때문에 동일한 데이터가 팜의 여러 컴퓨터에서 캐시될 수도 있습니다. 이는 디스크 공간 사용보다 성능에 도움이 되지만 데이터가 디스크에 이미 있는 경우 데이터에 더 빠르게 액세스할 수 있다는 이점이 있습니다.  
  
 디스크 공간 사용량을 즉시 줄이려면 서비스를 종료한 다음 백업 폴더에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스를 삭제하면 됩니다. 다음에 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터가 쿼리될 때 데이터베이스의 최신 복사본이 다시 캐시되므로 파일을 수동으로 삭제하는 것은 임시 조치에 불과합니다. 영구적인 해결 방법에는 캐시에 사용되는 디스크 공간을 제한하는 방법이 있습니다.  
  
 시스템 수준에서 디스크 공간이 부족할 때 알리는 전자 메일 경고를 만들 수 있습니다. Microsoft System Center에는 전자 메일 경고 기능이 포함되어 있습니다. 파일 서버 리소스 관리자, 작업 스케줄러 또는 PowerShell 스크립트를 사용하여 경고를 설정할 수도 있습니다. 부족한 디스크 공간에 대한 알림을 설정하는 데 대한 유용한 정보를 얻으려면  
  
-   [파일 서버 리소스 관리자의 새로운 소식](http://technet.microsoft.com/library/hh831746.aspx) (http://technet.microsoft.com/library/hh831746.aspx)합니다.  
  
-   [Windows Server 2008 r 2 용 파일 서버 리소스 관리자 단계별 가이드](http://go.microsoft.com/fwlink/?LinkID=204875) (http://go.microsoft.com/fwlink/?LinkID=204875)합니다.  
  
-   [Windows Server 2008에서 부족 한 디스크 공간 경고 설정](http://go.microsoft.com/fwlink/?LinkID=204870) ( http://go.microsoft.com/fwlink/?LinkID=204870)합니다.  
  
## <a name="how-to-limit-the-amount-of-disk-space-used-for-storing-cached-files"></a>캐시된 파일의 저장에 사용되는 디스크 공간 크기를 제한하는 방법  
  
1.  중앙 관리의 애플리케이션 관리에서 **서버의 서비스 관리**를 클릭합니다.  
  
2.  **SQL Server Analysis Services**를 클릭합니다.  
  
     제한은 서비스 애플리케이션 수준에서 설정되는 것이 아니라 물리적 서버에서 실행되는 Analysis Services 인스턴스에 대해 설정됩니다. 로컬 Analysis Services 인스턴스를 사용하는 모든 서비스 애플리케이션은 해당 인스턴스에 대해 설정된 단일 최대 디스크 공간 제한을 따릅니다.  
  
3.  디스크 사용에서 **총 디스크 공간** 의 값(GB)을 설정하여 캐싱 목적으로 사용되는 공간 크기의 상한값을 설정합니다. 기본값은 0이며 이 값을 사용하면 Analysis Services에서 사용 가능한 모든 디스크 공간을 사용할 수 있습니다.  
  
4.  디스크 사용의 **최근 ‘n’ 시간 내에 캐시된 데이터베이스 삭제** 설정에서 디스크 공간이 최대 한계일 경우 캐시를 비우기 위해 최근에 사용된 기준을 지정합니다.  
  
     기본값은 4시간이며, 이는 4시간 이상 비활성 상태인 모든 데이터베이스가 파일 시스템에서 삭제된다는 의미입니다. 비활성 상태이지만 아직 메모리에 있는 데이터베이스는 언로드된 다음 파일 시스템에서 삭제됩니다.  
  
## <a name="how-to-limit-how-long-a-database-is-kept-in-the-cache"></a>데이터베이스가 캐시에 유지되는 기간을 제한하는 방법  
  
1.  중앙 관리의 애플리케이션 관리에서 **서비스 애플리케이션 관리**를 클릭합니다.  
  
2.  **기본 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램**을 클릭하여 관리 대시보드를 엽니다.  
  
3.  동작에서 **서비스 애플리케이션 설정 구성**을 클릭합니다.  
  
4.  디스크 캐시 섹션에서 비활성 데이터베이스가 새 요청을 처리하기 위해 메모리에 유지되는 기간(기본적으로 48시간)과 캐시에 유지되는 기간(기본적으로 120시간)을 지정할 수 있습니다.  
  
     **메모리에 비활성 데이터베이스 유지** 는 비활성 데이터베이스가 새 요청을 처리하기 위해 메모리에 유지되는 기간을 지정합니다. 활성 데이터베이스는 쿼리하고 있는 동안에는 항상 메모리에 유지되지만 더 이상 활성 상태가 아니면 해당 데이터에 대한 추가 요청이 있을 경우를 대비해 추가 기간 동안 메모리에 유지됩니다.  
  
     [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스가 먼저 캐시된 다음 메모리에 로드되기 때문에 데이터베이스 파일은 디스크 공간을 즉시 사용합니다. 그러나 데이터베이스가 활성화되어 있는 동안(및 그 후 48시간 동안) 모든 요청은 캐시된 데이터베이스를 무시하고 먼저 메모리 내 데이터베이스로 전달됩니다. 비활성화되고 48시간 후에 파일이 메모리에서 언로드되지만 캐시에 유지되므로 로컬 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버 인스턴스가 해당 데이터에 대한 새 연결 요청을 가로채는 경우 파일이 신속하게 다시 로드될 수 있습니다. 비활성 데이터베이스에 대한 연결 요청은 콘텐츠 라이브러리보다는 캐시에서 처리되므로 콘텐츠 데이터베이스에 대한 영향이 최소화됩니다.  
  
     콘텐츠 라이브러리가 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스의 유일한 영구 위치임을 명심해야 합니다. 캐시된 복사본은 라이브러리의 데이터베이스가 디스크의 복사본과 동일한 경우에만 사용됩니다.  
  
     **캐시에 비활성 데이터베이스 유지** 는 비활성 데이터베이스가 메모리에서 언로드된 후 파일 시스템에 유지되는 기간을 지정합니다. 정리 작업에서는 이 설정을 사용하여 삭제할 파일을 결정합니다. 168시간(메모리에서 48시간 및 캐시에서 120시간) 동안 비활성 상태인 모든 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스는 정리 작업에 의해 디스크에서 삭제됩니다.  
  
5.  **확인** 을 클릭하여 변경 내용을 저장합니다.  
  
## <a name="next-steps"></a>다음 단계  
 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치에서는 서버 상태, 구성 또는 가용성에서 문제가 발견되면 수정 동작을 수행할 수 있도록 상태 규칙을 제공합니다. 이러한 규칙 중 일부는 구성 설정을 사용하여 상태 규칙이 트리거되는 조건을 확인합니다. 서버 성능을 적극적으로 조정하는 경우 이러한 설정을 검토하여 시스템에 가장 적절한 기본값이 선택되었는지 확인할 수도 있습니다. 자세한 내용은 [파워 피벗 상태 규칙 구성](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-health-rules.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [중앙 관리에서 Power Pivot 서버 관리 및 구성](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
