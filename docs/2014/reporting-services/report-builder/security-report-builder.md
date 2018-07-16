---
title: 보안(보고서 작성기) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ed38291a-6afe-449f-9f32-3ae04502bd6f
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: b2f11120fcc98bde39800ad75f94499b0b5f5081
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37309375"
---
# <a name="security-report-builder"></a>보안 (보고서 작성기)
  보고서 작성기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버에서 작동하도록 디자인된 보고서 제작 클라이언트 응용 프로그램입니다. 보고서 서버는 기본 모드에서 독립 실행형 서버로 작동하거나 SharePoint 사이트의 보고서를 지원하는 SharePoint 통합 모드에서 작동하도록 구성할 수 있습니다.  
  
 보고서 작성기에서는 보고서, 공유 데이터 집합 및 다시 사용 가능한 보고서 파트를 작성할 수 있습니다. 보고서 서버 또는 SharePoint 사이트에서 보고서를 편집하고 공유 데이터 원본, 공유 데이터 집합 및 공유 보고서 파트를 추가할 수 있습니다.  
  
 보고서 및 보고서 관련 항목을 작성, 게시 및 사용하려면 보안 기능이 다음 영역과 관련되는 방식을 이해해야 합니다.  
  
-   **보고서를 게시하는 보고서 서버 또는 SharePoint 사이트** 이 기능은 보고서 서버 관리자 또는 SharePoint 사이트 관리자가 관리합니다.  
  
-   **게시된 보고서 및 보고서 관련 항목** 보고서 관련 항목에는 포함된 데이터 원본 및 공유 데이터 원본과 자격 증명, 공유 데이터 집합, 매개 변수, 보고서 파트 및 보고서 모델이 포함됩니다. 이러한 항목에 적용되는 보안 기능은 보고서 작성자가 관리합니다. 보고서 서버 관리자 또는 SharePoint 사이트 관리자는 항목을 게시하거나 공유할 수 있는 권한을 보고서 작성자에게 부여해야 합니다.  
  
-   **보고서에 사용되는 외부 데이터 원본** 이 기능은 외부 데이터 원본 소유자가 관리합니다.  
  
-   **외부 데이터 원본을 기반으로 하는 보고서 모델** 이 기능은 모델 디자이너가 관리합니다.  
  
-   **매개 변수와 같은 대화형 보고서 기능** 이 기능은 보고서 작성자가 관리합니다.  
  
 이 항목의 정보는 보고서 및 보고서 관련 항목을 관리하고 보안을 설정하는 방법을 이해하는 데 도움이 됩니다.  
  
##  <a name="ReportServers"></a> 보고서 서버에 대한 보안 이해  
 보고서 게시와 보고서 보기는 권한이 필요한 작업입니다. 보고서 서버 관리자는 다음 형식의 보고서 서버 중 하나에서 권한이 있는 사용자만 보고서를 게시하고 볼 수 있도록 권한을 부여합니다.  
  
-   기본 모드에서 구성된 보고서 서버  
  
     보고서 서버에 연결하거나 보고서 서버를 찾으려면 해당 서버에 액세스할 수 있는 권한과 유효한 URL이 있어야 합니다.  
  
     보고서 서버에서 항목을 보거나 게시하기 위해 보고서 관련 항목 및 작업에 적용되는 권한 집합이 역할로 구성됩니다. 보고서 서버 관리자는 하나 이상의 역할에 사용자를 할당합니다. 예를 들어 미리 정의된 역할인 브라우저를 통해 보고서, 폴더, 모델 및 리소스를 볼 수 있습니다.  
  
     보고서 서버에 연결할 수 없거나 보고서 서버를 찾을 수 없는 경우 보고서 서버 관리자에게 문의하세요. 자세한 내용은 [Reporting Services Security and Protection](../security/reporting-services-security-and-protection.md) 온라인 설명서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](http://go.microsoft.com/fwlink/?linkid=121312).  
  
-   SharePoint 통합 모드에서 구성된 보고서 서버  
  
     보고서 서버와 통합된 SharePoint 사이트에 연결하려면 SharePoint 사이트나 하위 사이트에 대한 유효한 URL과 해당 사이트에 액세스할 수 있는 권한이 있어야 합니다.  
  
     보고서 관련 항목 및 작업에 대한 액세스 권한은 항목에 따라 사용자 또는 그룹 계정을 사용 권한 수준에 매핑하는 SharePoint 보안 정책을 통해 부여됩니다.  
  
     SharePoint 사이트나 하위 사이트에 연결할 수 없거나 해당 사이트를 찾을 수 없는 경우 SharePoint 사이트 관리자에게 문의하세요.  
  
=
  
##  <a name="Reports"></a> 게시된 보고서 및 보고서 관련 항목에 대한 보안 이해  
 보고서 및 보고서 관련 항목에 대한 보안은 보고서 서버 관리자가 관리합니다. 보고서 관련 항목에는 자격 증명, 공유 데이터 집합, 매개 변수, 보고서 파트 및 모델을 비롯한 포함된 데이터 원본 및 공유 데이터 원본이 포함됩니다.  
  
 보고서 서버 또는 SharePoint 사이트에서 보고서 및 보고서 관련 항목과 작업은 독립적인 보안 개체입니다. 항목 및 작업에 대한 액세스 권한은 항목에 따라 사용자 또는 그룹 계정을 사용 권한 수준에 매핑하는 SharePoint 보안 정책을 통해 부여됩니다. 많은 정책을 유지 관리할 때 발생할 수 있는 복잡성과 오버헤드를 줄이기 위해 폴더와 같은 컨테이너에 대한 사용 권한이 컨테이너의 항목별로 상속됩니다. 예를 들어 사용자가 폴더에 대한 특정 보고서 보기 권한을 가지고 있는 경우 해당 폴더의 항목에 대한 보고서 보기 권한도 가집니다.  
  
 항목 수준 보안을 사용하여 항목이나 폴더에 대한 사용 권한을 재정의할 수 있습니다. 항목 수준 보안을 적용할 경우 부모 컨테이너의 사용 권한 상속은 항목에 적용되지 않습니다. 항목 수준 보안을 폴더에 적용하면 중첩된 폴더는 같은 사용 권한을 상속합니다.  
  
 다른 사용자가 게시한 항목을 찾을 수 없는 경우 해당 항목이나 폴더에 대한 사용 권한 문제 때문일 수 있습니다.  
  
 게시한 항목을 다른 사용자가 찾아 공유할 수 있도록 하려면 보고서 서버 관리자와 작업하여 사용자에게 액세스를 제공하는 폴더 구성을 설정해야 합니다. 보고서를 제작하고 게시된 보고서를 실행하는 데 액세스를 사용할 수 있어야 합니다.  
  
 자세한 내용은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](http://go.microsoft.com/fwlink/?linkid=121312):  
  
-   [역할 및 권한&#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md)  
  
-   [공유 데이터 집합 관리](../report-data/manage-shared-datasets.md)  
  
### <a name="update-notifications-for-report-parts"></a>보고서 파트에 대한 업데이트 알림  
 보고서 파트는 다른 사용자가 공유할 수 있도록 보고서 서버에 게시됩니다. 기본적으로 보고서 파트를 게시할 위치를 지정해야 합니다.  
  
 보고서에 보고서 파트를 포함하고 있는 사용자는 업데이트 기능을 사용할 수 있습니다. 이 기능을 사용하면 보고서 서버에서 보고서 파트가 변경될 경우 사용자가 알림을 받을 수 있습니다.  
  
 원래 위치에서 보고서 파트를 제거하면 업데이트 알림에는 보고서 파트의 현재 위치와 이전 위치가 포함됩니다. 신뢰할 수 있는 위치의 업데이트만 적용하세요.  
  
 자세한 내용은 [보고서 파트&#40;보고서 작성기 및 SSRS&#41;](../report-parts-report-builder-and-ssrs.md)를 참조하세요.  
  
=  
  
##  <a name="Data"></a> 보고서 데이터 및 외부 데이터 원본에 대한 보안 이해  
 보고서의 각 외부 데이터 원본 데이터에 액세스하려면 보고서에 포함된 데이터 원본을 만들거나 공유 데이터 원본 또는 공유 데이터 집합에 대한 참조를 추가해야 합니다.  
  
 각 외부 데이터 원본에 대해 원본 및 기본 데이터에 액세스할 수 있는 자격 증명을 제공해야 합니다. 데이터 원본의 소유자는 이 액세스를 제공하는 자격 증명의 유형을 지정합니다.  
  
 자격 증명은 보고서 정의에 저장되지 않으며 보고서 서버 또는 SharePoint 사이트 및 보고서 제작 클라이언트의 보고서와는 별도로 관리됩니다.  
  
 보고서 디자인 타임에 자격 증명은 데이터 집합 쿼리를 실행하고 보고서를 미리 보는 데 사용됩니다. 런타임에 자격 증명은 보고서를 실행하고 보고서 결과를 캐시하는 데 사용됩니다. 공유 데이터 집합 쿼리 결과를 별도로 캐시할 수도 있습니다. 디자인 타임 자격 증명과 런타임 자격 증명이 다를 수 있습니다. 자세한 내용은 [보고서 작성기에 자격 증명 지정](../specify-credentials-in-report-builder.md)을 참조하세요.  
  
 데이터에 보안을 설정하는 방법은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](http://go.microsoft.com/fwlink/?linkid=121312):  
  
-   [SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대한 보안 센터](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 자세한 내용은 [보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](../data-connections-data-sources-and-connection-strings-in-report-builder.md)을 참조하세요.  
  
=
  
##  <a name="Models"></a> 모델 및 보안 필터 이해  
 외부 데이터를 기반으로 하는 보고서 모델에서 데이터를 검색할 때 모델에 보안 필터를 적용할 수 있습니다. 이것은 보고서를 실행하는 각 사용자가 사용 권한을 가진 데이터만 볼 수 있도록 데이터에 보안을 설정할 수 있는 좋은 방법입니다.  
  
 보고서 매개 변수는 행 수준 보안에는 사용되지 않으며 특정 데이터 행을 사용자나 사용자 그룹이 보지 못하도록 방지하지 않습니다. 보고서에 표시된 데이터에 보안을 적용하려면 보안 필터 또는 모델 항목 보안을 사용해야 합니다.  
  
=
  
##  <a name="Interactive"></a> 대화형 기능을 위한 보고서 제작에 대한 보안 이해  
 보고서에서는 일반적으로 매개 변수를 사용하여 사용자가 보고서 보기를 대화형으로 사용자 지정할 수 있도록 합니다. 다음 팁을 사용하면 좋은 방법으로 보고서를 디자인하는 데 도움이 됩니다.  
  
-   유효한 값을 제공한 경우에만 쿼리 매개 변수를 기반으로 하는 **텍스트** 형식의 매개 변수를 사용하세요. 사용 가능한 값 목록은 사용자가 유효한 값만 선택하는 데 도움이 됩니다. 사용 가능한 값 목록이 없으면 사용자가 입력할 수 있는 값을 제한할 수 없습니다.  
  
-   전역 [&UserID]를 사용하여 개인 데이터에 보안을 설정하지 마세요. 이 값은 URL 액세스 구문을 사용하여 보고서 URL에 보고서 매개 변수로 지정할 수 있습니다. 이 값을 공유 데이터 집합의 식에 사용하면 데이터 집합을 캐시할 수 없습니다. 자세한 내용은 [URL Access Parameter Reference](../url-access-parameter-reference.md) 온라인 설명서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](http://go.microsoft.com/fwlink/?linkid=121312).  
  
 보고서 서버에 항목을 게시한 후 보고서 서버 관리자는 역할 기반 보안이나 폴더 및 항목 수준 보안을 할당하여 항목에 보안을 설정할 수 있습니다. 자세한 내용은 [Secure Reports and Resources](../security/secure-reports-and-resources.md) 온라인 설명서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Books Online](http://go.microsoft.com/fwlink/?linkid=121312).  
  
 
  
## <a name="see-also"></a>관련 항목  
 [설치, 제거 및 보고서 작성기 지원](../install-uninstall-and-report-builder-support.md)   
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)  
  
  
