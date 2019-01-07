---
title: 보고서 파트 관리 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 41947b4c-8ecf-4e4f-b30e-66e1d6692b74
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fabed689d832cc71bcfe14a7f017d91b33244d84
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52394067"
---
# <a name="managing-report-parts"></a>보고서 파트 관리
  보고서 파트는 여러 사용자가 다시 사용하고 페이지가 매겨진 보고서 및 여러 보고서에서 다시 사용할 수 있습니다. 사용자는 서버에서 보고서 파트를 검색하여 보고서에 추가할 수 있습니다.  또한 사용자에게 서버의 보고서 파트에 대한 업데이트를 알리고 보고서 파트의 새 버전을 다시 게시할 수 있습니다. 이러한 보고서 제작 동작은 Reporting Services 보안 권한에 의해 제어되고 이의 영향을 받습니다.  이 항목에서는 서버에 게시된 보고서 파트 속성 및 동작을 검토합니다.  
  
## <a name="managing-report-parts"></a>보고서 파트 관리  
 보고서 파트를 관리하려면 기본 모드로 보고서 서버의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 사용하거나 SharePoint 통합 모드로 보고서 서버의 애플리케이션 페이지를 사용합니다.  
  
### <a name="server-side-interaction-and-search"></a>서버 쪽 상호 작용 및 검색  
 보고서 파트는 기본 모드 또는 SharePoint 통합 모드에서 보고서 서버에 게시할 수 있습니다. 사용자는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보고서 작성기와 같은 보고서 제작 응용 프로그램의 보고서 파트 갤러리 기능을 사용하여 보고서 파트를 찾고 이를 보고서에 추가할 수 있습니다. 사용자가 보고서 파트를 검색할 경우 서버가 설치된 모드와 상관없이 보고서 서버 카탈로그에서 검색이 수행됩니다.  
  
 보고서 작성기와 같은 보고서 제작 애플리케이션에서 SharePoint 통합 모드의 보고서 서버로 보고서 파트를 게시하면 보고서 서버 카탈로그도 업데이트되므로 갤러리 검색에도 새 보고서 파트나 업데이트 보고서 파트가 정확히 반영됩니다.  
  
#### <a name="directly-uploading-report-parts-to-a-sharepoint-folder"></a>SharePoint 폴더로 보고서 파트 직접 업로드  
 보고서 파트가 보고서 제작 애플리케이션에서 게시되지 않고 대신에 SharePoint 문서 폴더로 직접 업로드되는 경우 보고서 서버 카탈로그가 업데이트되지 않습니다. 따라서 보고서 파트 갤러리를 검색할 때 업로드된 보고서 파트를 찾을 수 없습니다. SharePoint 폴더와 보고서 서버 카탈로그의 동기화 상태를 유지하기 위해 SharePoint 서버에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 파일 동기화 기능을 활성화할 수 있습니다. 자세한 내용은 [SharePoint 중앙 관리에서 보고서 서버 파일 동기화 기능을 활성화](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)을 참조하세요.  
  
 GetProperties 및 SetProperties와 같은 일부 Reporting Services 관리 API를 호출하여 파일을 동기화할 수도 있습니다.  
  
### <a name="organizing-and-moving-report-parts"></a>보고서 파트 구성 및 이동  
 팀에서 보고서 파트 및 공유 데이터 세트와 공유 데이터 원본을 사용하고 구성할 방법을 미리 생각하고 계획하는 것이 좋습니다. 나중에 이를 이동할 수 있지만 문제가 있을 수 있습니다.  
  
#### <a name="native-mode-report-server"></a>기본 모드 보고서 서버  
 기본 모드 보고서 서버에서 동일한 서버의 다른 폴더로 보고서 파트를 이동하는 경우 보고서 제작 애플리케이션에서 보고서 파트에 대한 업데이트를 검색하거나 다운로드하는 기능에는 아무런 영향이 없습니다. 이는 서버가 고유 ComponentID에 의존하기 때문입니다. 그러나 보고서 파트가 사용자에게 사용 권한이 없는 폴더로 이동되는 경우 검색 시 보고서 파트를 찾을 수 없고 보고서 파트에 대한 업데이트가 있는 경우에도 보고서에서 알림을 받지 못합니다.  
  
#### <a name="report-server-in-sharepoint-integrated-mode"></a>SharePoint 통합 모드의 보고서 서버  
 보고서 파트를 다른 문서 라이브러리나 폴더로 이동하면 SharePoint 서버로 직접 업로드하는 것과 같은 결과를 가져옵니다. 즉, 보고서 서버 카탈로그가 동기화되지 않습니다. 이 문제를 방지하려면 SharePoint 서버의 보고서 서버 파일 동기화 기능을 활성화합니다.  
  
 그러나 하위 폴더는 예외입니다. 검색 시 항상 하위 폴더를 검색하므로 보고서 파트를 하위 폴더로 수동으로 이동해도 보고서 갤러리에서 검색 시 해당 보고서 파트를 찾을 수 있으며, 보고서 파트 갤러리에서 검색할 때도 해당 보고서 파트를 찾을 수 있습니다.  
  
### <a name="report-server-catalog-properties"></a>보고서 서버 카탈로그 속성  
 다음 표에서는 기존 보고서 서버 카탈로그 필드를 보고서 파트에 연결하는 방법과 보고서 파트의 카탈로그에 추가되는 새 필드에 연결하는 방법에 대해 설명합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 SharePoint 라이브러리와 보고서 작성기 등의 보고서 제작 응용 프로그램에서 사용할 수 있습니다.  
  
 별표(*)는 이번 릴리스에 새로 추가된 것임을 나타냅니다.  
  
|속성|설명|보고서 파트<br /><br /> 갤러리 검색 조건|  
|--------------|-----------------|---------------------------------------------|  
|속성|사용자가 보고서 파트 갤러리에서 검색할 수 있는 조건 중 하나입니다.|예|  
|설명|사용자가 갤러리에서 쉽게 찾을 수 있도록 보고서 파트 이름을 구성할 수 있습니다. 예를 들어 판매 관련 데이터 및 프레젠테이션이 포함되는 모든 보고서 파트를 찾을 때 "판매>>"로 시작하는 설명을 검색할 수 있습니다.|예|  
|CreatedBy|보고서 파트를 보고서 서버 데이터베이스에 추가한 사용자의 ID입니다. 정확한 형식은 인증 방식에 따라 다릅니다. 예를 들어 일부 인증 방법은 CreatedBy 및 ModifiedBy 필드에 전체 도메인\사용자 이름이 표시됩니다.|예|  
|CreationDate|보고서 파트가 처음 생성된 날짜입니다.<br /><br /> 사용자가 보고서 파트 갤러리에서 검색할 수 있는 조건 중 하나입니다.|예|  
|ModifiedBy|ModifiedBy는 보고서 파트를 마지막으로 수정한 사람의 ID입니다.|예|  
|ModifiedDate|서버에서 보고서 파트가 마지막으로 수정된 날짜입니다.<br /><br /> 이 필드는 보고서 파트에 대해 서버 쪽 업데이트가 이루어진 시점을 확인하는 논리의 일부로 사용됩니다. 자세한 내용은 이 표의 뒷부분에 나오는 ComponentID에 대한 설명을 참조하십시오.|예|  
|SubType (*)|SubType은 "테이블릭스" 또는 "차트"와 같이 검색할 보고서 파트의 종류를 나타내는 문자열입니다.|예|  
|ComponentID (*)|ComponentID는 보고서 파트의 고유 식별자입니다. 카탈로그에 추가되는 새 필드로, 서버 쪽뿐만 아니라 보고서 작성기와 같은 보고서 제작 애플리케이션에서도 표시됩니다.<br /><br /> 클라이언트 애플리케이션이 서버에서 보고서 파트의 업데이트를 확인할 때도 이 필드가 사용됩니다. 클라이언트 애플리케이션은 서버에서 현재 클라이언트 쪽 보고서에 있는 ComponentID를 검색합니다. 일치하는 ComponentID가 있으면, ModifiedDate를 보고서 항목의 클라이언트 쪽 SyncDate와 비교합니다.|지원 안 함|  
  
## <a name="controlling-access-to-report-parts"></a>보고서 파트에 대한 액세스 제어  
 다음 표에서는 기본 역할 할당 및 이를 사용하여 다양한 작업을 수행하는 방법에 대해 설명합니다. 역할 할당 이름은 사용되는 보고서 서버의 유형에 따라 다릅니다.  
  
### <a name="server-in-native-mode"></a>기본 모드의 서버  
  
|동작|역할|  
|-------------|-----------|  
|보고서 파트 추가, 삭제, 항목 속성 편집, 보안 관리 및 다운로드|내용 관리자<br /><br /> 내 보고서|  
|보고서 파트 추가, 삭제 및 다운로드|게시자|  
|검색 및 다시 사용|브라우저<br /><br /> 보고서 작성기|  
  
### <a name="server-in-sharepoint-integrated-mode"></a>SharePoint 통합 모드의 서버  
  
|동작|역할|  
|-------------|----------|  
|보고서 파트 추가, 삭제, 항목 속성 편집, 보안 관리 및 다운로드|모든 권한|  
|보고서 파트 추가, 삭제, 항목 속성 편집 및 다운로드|디자인<br /><br /> 참가|  
|검색 및 다시 사용|읽기<br /><br /> 보기만|  
  
### <a name="security-considerations"></a>보안 고려 사항  
  
-   보고서에 다시 사용되는 보고서 파트 정의는 식별 ComponentID와 함께 보고서 정의로 모두 복사됩니다. 보고서 파트가 서버에서 업데이트되면 사용자는 업데이트된 보고서 파트를 보고서로 다운로드할 수 있습니다. 업데이트 역시 보고서 정의에 대한 보고서 파트의 완전한 복사본이며 보고서에 있는 기존 보고서 파트 버전을 대체합니다.  
  
    > [!IMPORTANT]  
    >  이러한 각 단계에서 신뢰할 수 있는 위치와 사용자의 보고서에서 보고서 파트가 다시 사용되는지 확인해야 합니다.  
  
-   보고서 파트는 기존 "리소스" 항목 유형과 동일한 사용 권한 정책을 사용합니다. 보안 상속 관점에서 폴더 내의 기존 리소스 항목과 보고서 파트는 차이가 없습니다. 보고서 파트는 같은 폴더에 있는 이미지와 동일한 사용 권한 정책을 상속합니다. 구별해야 하는 경우에는 원하는 보고서 파트에 대해 항목 수준 보안을 구성할 수 있습니다. 또는 올바른 사용 권한이 구성된 별도의 폴더에 보고서 파트를 넣을 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 작성기의 보고서 파트 및 데이터 집합](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [보고서 서버 콘텐츠 관리&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [보고서 파트 문제 해결(보고서 작성기 및 SSRS)](https://msdn.microsoft.com/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [보고서 디자이너의 보고서 파트&#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md)  
  
  
