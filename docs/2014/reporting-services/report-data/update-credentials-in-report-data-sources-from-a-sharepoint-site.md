---
title: SharePoint 사이트의 보고서 데이터 원본에서 자격 증명 업데이트 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e0c50b6e-89e7-4b4d-8fe5-c90682c5d1b1
caps.latest.revision: 10
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 324b8730b4a61fdca6f0d1bafae27c6ca056f594
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184655"
---
# <a name="update-credentials-in-report-data-sources-from-a-sharepoint-site"></a>SharePoint 사이트의 보고서 데이터 원본에서 자격 증명 업데이트
  이 항목에서는 SharePoint 문서 라이브러리에 저장된 공유 데이터 원본 및 보고서에 포함된 데이터 원본을 업데이트하는 방법에 대해 설명합니다.  
  
 보고서 중 상당수에 데이터 원본이 포함되어 있거나 Windows 인증을 사용하도록 구성된 공유 데이터 원본이 사용되고 있을 수 있습니다. SharePoint 문서 라이브러리에 저장된 보고서에 대해 데이터 경고를 만드는 것과 같은 일부 상황에서는 데이터 원본 자격 증명을 저장된 자격 증명으로 업데이트하거나 자격 증명을 필요로 하지 않도록 업데이트해야 합니다.  
  
 보고서에서 저장된 자격 증명을 사용하기 위해 새 SQL Server 로그인을 만들어 사용할 수도 있습니다. 자세한 내용은 [로그인 만들기](../../relational-databases/security/authentication-access/create-a-login.md)를 참조하세요.  
  
### <a name="to-update-an-embedded-data-source-to-use-stored-credentials"></a>저장된 자격 증명을 사용하도록 포함된 데이터 원본을 업데이트하려면  
  
1.  보고서를 저장한 SharePoint 문서 라이브러리로 이동합니다.  
  
2.  보고서에서 확장 드롭다운 메뉴 아이콘을 클릭한 다음 **데이터 원본 관리**를 클릭합니다.  
  
     데이터 원본 관리 페이지가 열립니다.  
  
3.  **이름** 열에서 데이터 원본을 클릭합니다.  
  
4.  **연결 형식** 에 대해 **사용자 지정 데이터 원본** 옵션이 선택되어 있는지 확인합니다.  
  
     이 옵션은 데이터 원본이 보고서에 포함됨을 나타냅니다.  
  
5.  보고서를 다른 데이터 원본 유형, 다른 서버 또는 데이터 저장소에 연결하려는 것이 아닌 한 **데이터 원본 유형** 및 **연결 문자열** 옵션을 그대로 둡니다.  
  
6.  **자격 증명**에 대해 **저장된 자격 증명**을 선택합니다. 이 옵션은 데이터 원본이 자격 증명을 허용하지 않거나 사용자가 다른 방법으로 자격 증명을 전달하는 경우에만 작동합니다.  
  
     일부 상황에서는 **자격 증명 필요 없음** 옵션을 사용할 수도 있습니다.  
  
     일부 데이터 원본 유형의 경우 보고서 서버에서 무인 실행 계정을 구성해야 합니다. 자세한 내용은 [외부 데이터 원본의 데이터 추가&#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md) 및 [무인 실행 계정 구성&#40;SSRS 구성 관리자&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)의 해당하는 데이터 원본 유형에 대한 항목을 참조하세요.  
  
7.  사용자 이름 및 암호를 입력합니다.  
  
    -   계정이 Windows 도메인 사용자 계정인 경우 \<도메인>\\<계정\> 형식으로 지정한 다음 **데이터 원본에 연결할 때 Windows 자격 증명으로 사용**을 선택합니다.  
  
    -   사용자 이름과 암호가 데이터베이스 자격 증명인 경우 **데이터 원본에 연결할 때 Windows 자격 증명으로 사용**을 선택하지 않습니다. 데이터베이스 서버에서 가장 또는 위임이 지원되는 경우 **실행 컨텍스트를 이 계정으로 설정**을 선택할 수 있습니다.  
  
8.  업데이트된 자격 증명을 사용하여 데이터 원본 연결을 확인하려면 **연결 테스트**를 클릭합니다.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-update-a-shared-data-source-to-use-stored-credentials"></a>저장된 자격 증명을 사용하도록 공유 데이터 원본을 업데이트하려면  
  
1.  공유 데이터 원본을 저장한 SharePoint 문서 라이브러리로 이동합니다.  
  
2.  공유 데이터 원본에서 확장 드롭다운 메뉴 아이콘을 클릭한 다음 **데이터 원본 정의 편집**을 클릭합니다.  
  
     데이터 원본 페이지가 열립니다.  
  
3.  공유 데이터 원본을 다른 데이터 원본 유형, 다른 서버 또는 데이터 저장소에 연결하려는 것이 아닌 한 **데이터 원본 유형** 및 **연결 문자열** 옵션을 그대로 둡니다.  
  
4.  **자격 증명**에 대해 **저장된 자격 증명**을 선택합니다.  
  
     일부 상황에서는 **자격 증명 필요 없음** 옵션을 사용할 수도 있습니다. 이 옵션은 데이터 원본이 자격 증명을 허용하지 않거나 사용자가 다른 방법으로 자격 증명을 전달하는 경우에만 작동합니다.  
  
     일부 데이터 원본 유형의 경우 보고서 서버에서 무인 실행 계정을 구성해야 합니다. 자세한 내용은 [외부 데이터 원본의 데이터 추가&#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md) 및 [무인 실행 계정 구성&#40;SSRS 구성 관리자&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)의 해당하는 데이터 원본 유형에 대한 항목을 참조하세요.  
  
5.  사용자 이름 및 암호를 입력합니다.  
  
    -   계정이 Windows 도메인 사용자 계정인 경우 \<도메인>\\<계정\> 형식으로 지정한 다음 **데이터 원본에 연결할 때 Windows 자격 증명으로 사용**을 선택합니다.  
  
    -   사용자 이름과 암호가 데이터베이스 자격 증명인 경우 **데이터 원본에 연결할 때 Windows 자격 증명으로 사용**을 선택하지 않습니다. 데이터베이스 서버에서 가장 또는 위임이 지원되는 경우 **실행 컨텍스트를 이 계정으로 설정**을 선택할 수 있습니다.  
  
6.  업데이트된 자격 증명을 사용하여 데이터 원본 연결을 확인하려면 **연결 테스트**를 클릭합니다.  
  
7.  이 데이터 원본 사용이 선택되어 있는지 확인합니다.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [SharePoint 라이브러리에 문서 업로드&#40;SharePoint 모드의 Reporting Services&#41;](../upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)  
  
  