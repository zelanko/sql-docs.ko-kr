---
title: SharePoint용 PowerPivot 설치 문제 해결 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 797405386e8a6c0b9e62328699f3a73a6d845313
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892438"
---
# <a name="troubleshoot-a-powerpivot-for-sharepoint-installation"></a>SharePoint용 PowerPivot 설치 문제 해결
  예상한 페이지 및 기능 대신 오류가 발생할 경우 다음을 수행합니다.  
  
-   알려진 설치 문제에 대한 해결 방법은 SharePoint 및 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에 대한 릴리스 정보를 참조하십시오. 릴리스 정보는 소프트웨어를 다운로드한 Microsoft 사이트나 설치 미디어에 제공됩니다.  
  
    -   [SQL Server 2014 릴리스 정보](https://technet.microsoft.com/library/dn169381\(v=sql.15\).aspx)  
  
-   Technet wiki 항목인 [PowerPivot 및 기타 추가 기능의 설치 문제 해결](https://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx)을 참조하십시오.  
  
## <a name="issues"></a>문제  
  
### <a name="powerpivot-gallery-thumbnail-images-show-as-a-red-x"></a>PowerPivot 갤러리 축소판 이미지가 빨간색 X로 표시됨  
 한 가지 가능한 원인은 **사이트 모음에 대한 PowerPivot 기능 통합** 이 활성 상태가 아닌 것입니다. 다음을 완료합니다.  
  
1.  PowerPivot 갤러리 라이브러리의 기어 아이콘 ![Sharepoint 설정](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "Sharepoint 설정") 또는 **홈** 목록에서 **사이트 설정** 을 클릭 합니다.  
  
2.  **사이트 모음 관리** 섹션에서 **사이트 모음 기능**을 클릭합니다.  
  
3.  **사이트 모음 기능**을 클릭합니다.  
  
4.  **사이트 모음에 대한 PowerPivot 기능 통합** 이 **활성**상태인지 확인합니다.  
  
 이 문제의 추가 원인은 https://support.microsoft.com/kb/2361559) [PowerPivot 갤러리의 아이콘에 빨간색 X가 표시](https://support.microsoft.com/kb/2361559) 되는 경우를 참조 하세요.  
  
  
