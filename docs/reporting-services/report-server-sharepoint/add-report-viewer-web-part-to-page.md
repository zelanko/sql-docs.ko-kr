---
title: SharePoint 페이지에 SQL Server Reporting Services 보고서 뷰어 웹 파트 추가 | Microsoft Docs
ms.custom: ''
ms.date: 09/26/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server-sharepoint
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3d63f40c62c1997be2d4944c8b67f328d2b64c2d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33024930"
---
# <a name="add-sql-server-reporting-services-report-viewer-web-part-to-a-sharepoint-page"></a>SharePoint 페이지에 SQL Server Reporting Services 보고서 뷰어 웹 파트 추가

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

SharePoint 페이지에 보고서 뷰어 웹 파트를 추가하여 SQL Server Reporting Services 또는 Power BI Report Server에서 보고서를 표시합니다.

![SharePoint 페이지의 보고서 뷰어 웹 파트](media/sharepoint-report-viewer-web-part-on-page.png)

## <a name="prerequisites"></a>사전 요구 사항

* 보고서를 성공적으로 로드하려면 C2WTS(Windows 토큰 서비스에 대한 클레임)가 Kerberos 제한된 위임에 대해 구성되어야 합니다. C2WTS를 구성하는 방법에 대한 자세한 내용은 [C2WTS(Windows 토큰 서비스에 대한 클레임) 및 Reporting Services](../install-windows/claims-to-windows-token-service-c2wts-and-reporting-services.md)를 참조하세요.

* 보고서 뷰어 웹 파트는 SharePoint 팜에 배포되어야 합니다. 보고서 뷰어 웹 파트 솔루션 프로젝트를 배포하는 방법에 대한 내용은 [SharePoint 사이트의 보고서 뷰어 웹 파트 배포](deploy-report-viewer-web-part.md)를 참조하세요.

* 웹 페이지에 웹 파트를 추가하려면 사이트 수준에서 페이지 추가 및 사용자 지정 권한이 있어야 합니다. 기본 보안 설정을 사용하는 경우 이 권한은 모든 권한 수준의 사용 권한이 있는 **소유자** 그룹의 멤버에게 부여됩니다.

## <a name="add-web-part"></a>웹 파트 추가

1. SharePoint 사이트의 왼쪽 위에서 **기어** 아이콘을 선택하고 **페이지 추가**를 선택합니다.

    ![기어 아이콘에서 sharepoint 사이트에 페이지를 추가합니다.](media/sharepoint-add-a-page.png)

2. 페이지에 이름을 지정하고 **만들기**를 선택합니다.

3. 페이지 디자이너 내의 리본에서 **삽입** 탭을 선택합니다. 그런 다음 **파트** 섹션 내의 **웹 파트**를 선택합니다.

    ![사무실 리본에서 웹 파트를 삽입합니다.](media/sharepoint-insert-web-part.png)

4. **범주** 아래에서 **SQL Server Reporting Services(기본 모드)를 선택합니다. **파트** 아래에서 **보고서 뷰어**를 선택합니다. 그런 다음 **추가**를 선택합니다.

    ![보고서 뷰어 웹 파트를 추가합니다.](media/sharepoint-report-viewer-web-part.png)

    이는 처음에 오류와 함께 나타날 수 있습니다. 오류는 기본 보고서 서버 URL이 *http://localhost*로 설정되어 있으며 해당 위치에서 사용할 수 없기 때문입니다.

## <a name="configure-the-report-viewer-web-part"></a>보고서 뷰어 웹 파트 구성

특정 보고서를 가리키도록 웹 파트를 구성하려면 다음을 수행합니다.

1. SharePoint 페이지를 편집할 때 웹 파트의 오른쪽 위에 있는 아래쪽 화살표를 선택하고 **웹 파트 편집**을 선택합니다.

    ![웹 파트 드롭다운 목록에서 웹 페이지를 편집합니다.](media/sharepoint-edit-web-part.png)

2. 보고서를 호스팅하는 보고서 서버에 대한 **보고서 서버 URL**을 입력합니다. 이는 *http://myrsserver/reportserver*과 같이 표시됩니다.

3. 웹 파트 내에서 표시하려는 보고서의 경로 및 이름을 입력합니다. 이는 */AdventureWorks Sample Reports/Company Sales*와 유사합니다. 이 예제에서는 보고서 *Company Sales*는 *AdventureWorks Sample Reports*라는 폴더에 있습니다.

4. 보고서에 매개 변수가 필요한 경우 보고서 서버 URL 및 보고서의 이름을 제공한 후 **매개 변수** 섹션 내에서 **매개 변수 로드**를 선택합니다.

5. **확인**을 선택하여 웹 파트 구성에 변경 내용을 저장합니다.

6. 사무실 리본 내에서 **저장**을 선택하여 SharePoint 페이지에 변경 내용을 저장합니다.

![SharePoint 페이지의 보고서 뷰어 웹 파트](media/sharepoint-report-viewer-web-part-on-page.png)

## <a name="considerations-and-limitations"></a>고려 사항 및 제한 사항

* SharePoint 내의 최신 페이지에는 보고서 뷰어 웹 파트를 사용할 수 없습니다.
* Power BI 보고서는 보고서 뷰어 웹 파트와 함께 사용할 수 없습니다.
* 보고서 뷰어 웹 파트가 표시되지 않는 경우 페이지에 추가하려면 [보고서 뷰어 웹 파트를 배포](deploy-report-viewer-web-part.md)했는지 확인합니다.

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
