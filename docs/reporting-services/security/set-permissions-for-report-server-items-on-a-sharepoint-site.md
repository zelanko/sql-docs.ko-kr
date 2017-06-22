---
title: "SharePoint 사이트에 보고서 서버 항목에 대 한 사용 권한을 설정 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
ms.assetid: 2467c657-a3bf-4ec3-a88c-8877df19823d
caps.latest.revision: 14
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 183adf345dabb5d1abce184691ef2d59904ecaa0
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="set-permissions-for-report-server-items-on-a-sharepoint-site"></a>SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 설정
  기본 보안 설정으로 필요한 액세스 수준을 얻을 수 없는 경우 새 사용 권한 수준을 만들어 특정 보고서 서버 항목이나 작업에 대한 액세스 권한을 제공할 수 있습니다. 사용자 지정 보안 설정은 특정 보고서에 대한 액세스를 제한하려는 경우에 유용할 수 있습니다.  
  
 사용 권한 수준 및 그룹을 만들려면 사이트 소유자여야 합니다. 사용 권한 수준은 사이트 전체에서 사용됩니다. 새 사용 권한 수준을 만들면 다른 사이트 소유자도 사용할 수 있습니다.  
  
 대부분의 사용 권한은 부모 사이트로부터 상속됩니다. 특정 라이브러리나 항목에 대해 사용 권한을 할당하면 사용 권한 상속이 해제되고 사이트 계층의 해당 분기에 대해 사용 권한을 관리해야 하는 추가 오버헤드가 발생합니다.  
  
 보고서 정의 파일(.rdl), 모델 파일(.smdl) 및 공유 데이터 원본 파일(.rsds)에 대해 사용 권한을 설정할 수 있습니다. 동일한 항목에 대해 상속된 사용 권한과 관리되는 사용 권한을 함께 사용할 수는 없습니다. 직접 사용 권한을 관리하도록 선택하면 상속된 사용 권한은 현재 항목에 영향을 주지 않습니다. 나중에 사용 권한 상속을 재개하려면 **동작** 메뉴에서 **사용 권한 상속** 을 선택할 수 있습니다.  
  
 모델의 엔터티와 큐브 뷰에 대해 사용 권한을 설정하려면 모델에 대한 모든 권한 수준의 사용 권한이 있어야 합니다. 모든 권한에는 사이트 소유자 및 모든 권한 수준의 사용 권한이 있는 기타 SharePoint 그룹에 부여되는 사이트 수준의 사용 권한인 "사용 권한 관리"가 포함됩니다. 특정 사용자에게 모델 항목 보안을 설정할 수 있도록 권한을 부여하려는 경우 사용 권한 상속을 해제하고 사용자나 그룹에 모델 파일에 대한 승격된 사용 권한(예: 모든 권한)을 부여해야 합니다. 라이브러리의 항목(예: 파일)에 대한 "모든 권한"을 부여하면 사용 권한의 범위는 해당 항목이고 동일한 라이브러리 내에서 부모 또는 다른 항목으로 확장되지 않습니다. 모델에 대한 "사용 권한 관리" 권한이 부여된 사용자는 SharePoint 사이트나 모델 디자이너를 통해 모델 항목 보안을 설정할 수 있습니다.  
  
### <a name="to-set-permissions-on-an-individual-report-model-or-data-source"></a>개별 보고서, 모델 또는 데이터 원본에 대한 사용 권한을 설정하려면  
  
1.  라이브러리가 열려 있지 않으면 빠른 실행에서 해당 이름을 클릭합니다. 라이브러리 이름이 나타나지 않으면 **모든 사이트 콘텐츠 보기**를 클릭한 다음 라이브러리 이름을 클릭합니다.  
  
2.  보고서, 보고서 모델 또는 공유 데이터 원본 파일을 가리킵니다.  
  
3.  아래쪽 화살표를 클릭하고 메뉴에서 **사용 권한 관리**를 클릭합니다.  
  
4.  **동작** 메뉴에서 **사용 권한 편집**을 클릭한 다음 **확인** 을 클릭하여 동작을 확인합니다.  
  
5.  아직 파일을 사용할 권한이 없는 사용자나 그룹에 사용 권한을 부여하려면 **새로 만들기**, **사용자 추가**를 차례로 클릭합니다.  
  
6.  기존 사용자 또는 그룹의 사용 권한을 제거하거나 수정하려면 사용자나 그룹 옆의 확인란을 클릭하고 **동작**을 클릭한 다음 **사용자의 사용 권한 제거** 또는 **사용자의 사용 권한 편집**을 클릭합니다.  
  
### <a name="to-set-permissions-that-enable-model-item-security"></a>모델 항목 보안을 설정하는 사용 권한을 지정하려면  
  
1.  사이트에 대한 "사용 권한 관리" 권한이 있는 계정을 사용하여 SharePoint 사이트에 로그인합니다.  
  
2.  모델이 포함된 라이브러리를 엽니다.  
  
3.  모델을 가리킵니다.  
  
4.  모델 옆의 아래쪽 화살표를 클릭하고 **사용 권한 관리**를 클릭합니다.  
  
5.  **동작**을 클릭합니다.  
  
6.  **사용 권한 편집**을 클릭합니다. **확인**을 클릭합니다.  
  
7.  **새로 만들기**를 클릭합니다.  
  
8.  **사용자 추가**를 클릭합니다.  
  
9. 사용자/그룹에 사용자 계정을 입력합니다.  
  
10. **사용자에게 사용 권한 직접 부여**를 선택합니다.  
  
11. **모든 권한**을 클릭합니다.  
  
12. **확인**을 클릭합니다. 특정 모델에 대한 사용 권한 관리 권한이 있는 사용자는 모델을 열어 모델 내에서 사용 권한을 편집할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 서버 항목에 대해 Windows SharePoint Services의 기본 제공 보안 사용](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)   
 [SharePoint 웹 응용 프로그램에서 보고서 서버 작업에 대한 사용 권한 설정](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [Reporting Services의 역할 및 태스크와 SharePoint 그룹 및 사용 권한 비교](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [보고서 서버 항목에 대한 SharePoint 사이트 및 목록 사용 권한 참조](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)   
 [SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 부여](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
