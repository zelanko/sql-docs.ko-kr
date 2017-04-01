---
title: "SharePoint용 파워 피벗 설치 문제 해결 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# SharePoint용 파워 피벗 설치 문제 해결
  예상한 페이지 및 기능 대신 오류가 발생할 경우 다음을 수행합니다.  
  
-   알려진 설치 문제에 대한 해결 방법은 SharePoint 및 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 에 대한 릴리스 정보를 참조하십시오. 릴리스 정보는 소프트웨어를 다운로드한 Microsoft 사이트나 설치 미디어에 제공됩니다.  
  
    -   [SQL Server 2016 릴리스 정보](../sql-server/sql-server-2016-release-notes.md)  
  
-   TechNet wiki 항목, [Troubleshooting Installations of Power Pivot (and other add-ins)](http://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx)(파워 피벗 및 기타 추가 기능의 설치 문제 해결)을 참조하세요.  
  
## 문제  
  
### Power Pivot 갤러리 축소판 이미지가 빨간색 X로 표시됨  
 한 가지 가능한 원인은 **[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 기능 통합** 이 활성 상태가 아닌 것입니다. 다음을 완료합니다.  
  
1.  [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 갤러리 라이브러리의 기어 아이콘 ![SharePoint 설정](../analysis-services/media/as-sharepoint2013-settings-gear.png "SharePoint 설정") 또는 **홈** 목록에서 **사이트 설정**을 클릭합니다.  
  
2.  **사이트 모음 관리** 섹션에서 **사이트 모음 기능**을 클릭합니다.  
  
3.  **사이트 모음 기능**을 클릭합니다.  
  
4.  **[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 기능 통합** 이 **활성**상태인지 확인합니다.  
  
 이 문제의 추가 원인은 [Power Pivot Gallery shows Red X's for Icons](http://support.microsoft.com/kb/2361559)(파워 피벗 갤러리의 아이콘에 빨간색 X가 표시됨)(http://support.microsoft.com/kb/2361559)를 참조하세요.  
  
  