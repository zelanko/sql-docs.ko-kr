---
title: 보고서 서버 항목에 대해 Windows SharePoint Services의 기본 제공 보안 사용 | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 9577e88d-c22b-4934-936f-e0f1400cedf5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4b543c79ade78fe62b5484926d20e876c251b9ad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47817001"
---
# <a name="use-built-in-security-in-windows-sharepoint-services-for-report-server-items"></a>보고서 서버 항목에 대해 Windows SharePoint Services의 기본 제공 보안 사용
  SharePoint는 SharePoint 사이트와 라이브러리에서 보고서 서버 항목에 액세스하는 데 사용할 수 있는 기본 제공 보안 기능을 제공합니다. 이미 사용자에게 사이트 및 목록 사용 권한을 할당한 경우 SharePoint와 보고서 서버 간의 통합 설정을 구성하면 즉시 해당 사용자가 보고서 서버 항목과 작업에 액세스할 수 있습니다.  
  
## <a name="securable-items"></a>보안 개체 항목  
 사이트나 라이브러리에 정의된 사용 권한을 사용하여 보고서 서버 항목에 대한 액세스 권한을 부여할 수 있습니다. 하지만 개별 항목의 보안을 설정하려는 경우 다음 콘텐츠 형식에 사용 권한을 설정할 수 있습니다.  
  
|파일 유형|설명|  
|---------------|-----------------|  
|.rdl|데이터 검색에 사용되는 명령과 보고서 레이아웃을 정의하는 보고서 정의 파일입니다. 보고서 정의는 보고서를 처리할 때 데이터 원본 연결 정보를 사용하여 데이터를 검색합니다. 보고서 정의가 보고서 작성기에서 만든 임시 보고서인 경우 렌더링된 보고서에 데이터 탐색 범위를 설정하는 보고서 모델 파일(.smdl)과 보고서가 연결됩니다.|  
|.smdl|데이터 구조와 관계를 설명하는 보고서 모델 파일입니다. 이 파일은 보고서 작성기 보고서를 만들고 실행하는 데 사용됩니다.|  
|.rsds|외부 데이터 원본에 대한 연결 정보를 지정하는 공유 데이터 원본 파일입니다. 이 파일은 보고서 정의 파일(.rdl) 및 보고서 모델 파일(.smdl)에서 사용됩니다. 보고서 모델은 항상 .rsds 파일을 사용하여 기본 데이터 원본에 대한 연결 정보를 가져옵니다. 보고서 정의는 .rsds 파일 또는 보고서의 데이터 원본 속성에 정의된 연결 정보를 사용할 수 있습니다.|  
|.rsc|보고서 항목 또는 데이터 영역의 레이아웃과 구조를 정의하는 보고서 파트 파일입니다. 다른 보고서 만든 이가 보고서 파트 갤러리에서 항목을 다시 사용할 수 있도록 보고서 파트를 서버에 게시하는 데 사용됩니다.|  
|.rsd|데이터 집합에 대한 쿼리 구문과 속성을 정의하는 공유 데이터 집합 파일입니다. 공유 데이터 집합을 보고서 외부에서 공유, 저장, 처리 및 캐시할 수 있습니다.|  
  
 일정, 구독 및 보고서 기록은 보안 개체 항목이 아닙니다. 사용자가 일정, 구독 및 보고서 기록을 만들거나 사용할 수 있는지 결정하는 사용 권한을 사이트나 라이브러리에 설정할 수 있지만 이러한 항목의 보안을 직접 설정할 수는 없습니다.  
  
 개별 항목의 보안을 설정하려면 라이브러리에서 해당 항목을 선택하고 아래쪽 화살표를 클릭한 다음 **사용 권한 관리**를 선택합니다. **동작** 메뉴에서 **사용 권한 편집**을 선택합니다.  
  
## <a name="using-built-in-groups-and-permission-levels-to-access-report-server-items"></a>기본 제공 그룹 및 사용 권한 수준을 사용하여 보고서 서버 항목에 액세스  
 사용 권한 상속과 표준 SharePoint 그룹을 사용하는 경우 보고서 서버와 SharePoint 인스턴스에서 통합 설정을 구성한 후 즉시 보고서 서버 작업에 액세스할 수 있습니다.  
  
 SharePoint는 SharePoint 사이트의 문서와 페이지에 액세스하는 방법을 결정하는 미리 정의된 사용 권한 수준에 매핑되는 표준 그룹을 제공합니다. 표준 그룹과 기본 사용 권한 수준을 사용 중이며 사용 권한을 상속하도록 사이트가 구성된 경우 다음 방식으로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능을 사용할 수 있습니다.  
  
|**SharePoint 그룹**|**사용 권한 수준**|**요약**|**보고서 서버 액세스**|  
|---------------------------|--------------------------|-----------------|------------------------------|  
|**소유자**|모든 권한|소유자는 보고서 서버 항목 및 작업을 만들고 관리하며 보안을 설정할 수 있는 모든 권한을 갖습니다.|사이트 전체 라이브러리에 저장된 모든 보고서 서버 항목에 대한 액세스를 제어하는 사용 권한을 설정합니다. 보고서 모델 내의 사용 권한을 설정합니다(모델 항목 보안). 보고서 뷰어 웹 파트를 사용자 지정합니다. 라이브러리에 보고서 및 기타 항목을 추가합니다. 보고서 및 기타 문서에 대한 항목 속성을 편집합니다. 보고서 및 기타 항목을 삭제합니다. 데이터 탐색을 위해 보고서 모델을 사용하는 보고서 등 보고서를 봅니다. 보고서의 매개 변수를 설정합니다. 보고서의 처리 옵션을 설정합니다. 보고서 모델을 생성합니다. 보고서 작성기에서 보고서를 만듭니다. 공유 데이터 원본을 만들고 관리합니다. 모든 사용자가 소유하는 구독을 만들고 변경 및 삭제합니다. 사이트 전체에서 사용되는 공유 일정을 만들고 관리합니다. 보고서 기록을 포함하여 문서 버전을 만들고 관리합니다. 보고서 정의나 보고서 모델의 원본 파일을 다운로드합니다. 보고서 정의, 보고서 모델, 공유 데이터 원본 또는 리소스를 바꿉니다(항목 속성 및 사용 권한 유지).|  
|**멤버**|참가|멤버는 새 항목을 만들고 디자인 도구에서 SharePoint 라이브러리로 항목 보고서와 모델을 게시할 수 있습니다.|라이브러리에 보고서 및 기타 항목을 추가합니다. 보고서 및 기타 문서에 대한 항목 속성을 편집합니다. 보고서 및 기타 항목을 삭제합니다. 데이터 탐색을 위해 보고서 모델을 사용하는 보고서 등 보고서를 봅니다. 보고서 기록 스냅숏을 비롯한 문서의 이전 버전을 봅니다. 이 경우 보고서 기록이 생성된 보고서를 열 권한이 사용자에게 있어야 합니다. 보고서의 매개 변수를 설정합니다. 보고서의 처리 옵션을 설정합니다. 보고서 모델을 생성합니다. 보고서 작성기에서 보고서를 만듭니다. 공유 데이터 원본을 만들고 관리합니다. 해당 사용자가 소유하는 구독을 만들고 변경 및 삭제합니다. 구독에 공유 일정을 사용합니다. 보고서 기록을 포함하여 문서 버전을 만들고 관리합니다. 보고서 정의나 보고서 모델의 원본 파일을 다운로드합니다. 보고서 정의, 보고서 모델, 공유 데이터 원본 또는 리소스를 바꿉니다(항목 속성 및 사용 권한 유지).|  
|**방문자** 및 **뷰어**|읽기|방문자는 보고서를 볼 수 있습니다.|데이터 탐색을 위해 보고서 모델을 사용하는 보고서 등 보고서를 봅니다.|  
  
 기본 제공 그룹과 사용 권한 수준을 사용하지 않는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능에 액세스하려면 특정 사용 권한을 포함해야 합니다. 자세한 내용은 [SharePoint 웹 응용 프로그램에서 보고서 서버 작업에 대한 사용 권한 설정](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 부여](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Reporting Services의 역할 및 태스크와 SharePoint 그룹 및 사용 권한 비교](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [SharePoint 웹 응용 프로그램에서 보고서 서버 작업에 대한 사용 권한 설정](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 부여](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
