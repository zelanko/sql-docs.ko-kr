---
title: "SharePoint 페이지에 SQL Server Reporting Services 보고서 뷰어 웹 파트 추가 | Microsoft Docs"
ms.custom: Display a report, from SQL Server Reporting Services or Power BI Report Server, by adding a Report Viewer web part to a SharePoint page.
ms.date: 09/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: fbc68b6ff9f1edf5cf6ee13f6e93a3d2d1a8f834
ms.contentlocale: ko-kr
ms.lasthandoff: 10/06/2017

---

# <a name="add-sql-server-reporting-services-report-viewer-web-part-to-a-sharepoint-page"></a>SharePoint 페이지에 SQL Server Reporting Services 보고서 뷰어 웹 파트 추가

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

SharePoint 페이지에는 보고서 뷰어 웹 파트를 추가 하 여 SQL Server Reporting Services 또는 Power BI 보고서 서버에서 보고서를 표시 합니다.

![SharePoint 페이지에서 보고서 뷰어 웹 파트](media/sharepoint-report-viewer-web-part-on-page.png)

## <a name="prerequisites"></a>필수 구성 요소

* 성공적으로 로드 하려면 보고서에 대 한 Kerberos에 대해 구성 해야 하는 Windows 토큰 서비스 (C2WTS)에 대 한 클레임이 제한 된 위임 합니다. C2WTS를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Windows 토큰 서비스 (C2WTS) 및 Reporting Services에 대 한 클레임](../install-windows/claims-to-windows-token-service-c2wts-and-reporting-services.md)합니다.

* 보고서 뷰어 웹 파트를 SharePoint 팜에 배포 되어야 합니다. 보고서 뷰어 웹 파트 솔루션 프로젝트를 배포 하는 방법에 대 한 정보를 참조 하십시오. [SharePoint 사이트에서 보고서 뷰어 웹 파트 배포](deploy-report-viewer-web-part.md)합니다.

* 웹 페이지에 웹 파트를 추가 하려면 사이트 수준에서 페이지를 사용자 지정 및 추가 권한이 있어야 합니다. 기본 보안 설정을 사용하는 경우 이 권한은 모든 권한 수준의 사용 권한이 있는 **소유자** 그룹의 멤버에게 부여됩니다.

## <a name="add-web-part"></a>웹 파트 추가

1. SharePoint 사이트에서 선택 된 **기어** 왼쪽 위에 하 고 선택 아이콘 **페이지를 추가**합니다.

    ![기어 아이콘에서 sharepoint 사이트에는 페이지를 추가 합니다.](media/sharepoint-add-a-page.png)

2. 이름과 선택 페이지를 지정 **만들기**합니다.

3. 페이지 디자이너에서 선택 하 고 **삽입** 리본 메뉴에 탭 합니다. 다음 선택 **웹 파트** 내에서 **부분** 섹션.

    ![Office 리본 메뉴에서 웹 파트를 삽입 합니다.](media/sharepoint-insert-web-part.png)

4. 아래 **범주**선택, **SQL Server Reporting Services (기본 모드). 아래 **부분**선택, **보고서 뷰어**합니다. 그런 다음 선택 **추가**합니다.

    ![보고서 뷰어 웹 파트를 추가 합니다.](media/sharepoint-report-viewer-web-part.png)

    이 오류가 발생 하 여 처음에 나타날 수 있습니다. 오류는 기본 보고서 서버 URL로 설정 되어 있으므로 *http://localhost* 해당 위치에서 사용할 수 있는 되지 않을 수 있습니다.

## <a name="configure-the-report-viewer-web-part"></a>보고서 뷰어 웹 파트를 구성 합니다.

특정 보고서를 가리키도록 웹 파트를 구성 하려면 다음을 수행 합니다.

1. SharePoint 페이지를 편집할 때 웹 파트의 오른쪽 위에 있는 아래쪽 화살표를 선택 하 고 선택 **웹 파트 편집**합니다.

    ![웹 파트 드롭다운 목록에서 웹 페이지를 편집 합니다.](media/sharepoint-edit-web-part.png)

2. 입력은 **보고서 서버 URL** 보고서를 호스팅하는 보고서 서버에 대 한 합니다. 이것은 비슷합니다 *http://myrsserver/reportserver*합니다.

3. 웹 파트 내에서 표시할 보고서의 이름과 경로 입력 합니다. 이것은 유사 *AdventureWorks Sample Reports/Company Sales*합니다. 이 예제에서는 보고서 *Company Sales* 라고 하는 폴더에 *AdventureWorks 예제 보고서*합니다.

4. 보고서가 필요한 경우 매개 변수를 보고서 서버 URL과 보고서의 이름을 지정한 후 선택 **매개 변수 로드** 내는 **매개 변수** 섹션.

5. 선택 **확인** 에 웹 파트 구성에 변경 내용을 저장 합니다.

6. 선택 **저장**, SharePoint 페이지에 변경 내용을 저장 하는 Office 리본 메뉴 내에서.

![SharePoint 페이지에서 보고서 뷰어 웹 파트](media/sharepoint-report-viewer-web-part-on-page.png)

## <a name="considerations-and-limitations"></a>고려 사항 및 제한 사항

* SharePoint에 있는 최신 페이지에는 보고서 뷰어 웹 파트를 사용할 수 없습니다.
* 보고서 뷰어 웹 파트와 power BI 보고서를 사용할 수 없습니다.
* 보고서 뷰어 웹 파트를 페이지에 추가 하려면 표시 되지 않으면 했는지 확인 [보고서 뷰어 웹 파트 배포](deploy-report-viewer-web-part.md)합니다.

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)

