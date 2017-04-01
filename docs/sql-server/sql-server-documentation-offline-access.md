---
title: "SQL Server 설명서 오프라인 액세스 | Microsoft Docs"
ms.custom: ""
ms.date: "08/22/2016"
ms.prod: "sql-non-specified"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 257ed357-8cbb-43bd-b042-254be5fbb977
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# SQL Server 설명서 오프라인 액세스

오프라인에서 SQL Server 2016 기술 설명서를 확인합니다.
  
## 필수 구성 요소
오프라인에서 SQL Server 2016 기술 설명서를 보려면 다음과 함께 설치되는 HelpViewer 2.2가 필요합니다. 
- [Visual Studio 2015(Community를 포함하는 임의 버전)](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) 또는
- [SQL Server Management Studio(SSMS) April 2016 Preview(13.0.12500.29) 이상](https://msdn.microsoft.com/library/mt238290.aspx)

아래 단계를 진행하기 전에 이러한 프로그램 중 하나를 설치합니다.
  
## SQL Server 오프라인 기술 설명서 설치 

1. 임의 버전의 Visual Studio 2015 또는 SSMS April 2016 Preview 빌드 이상을 설치합니다. 
2. SSMS 또는 Visual Studio를 시작합니다.
3. 위쪽 탐색 모음의 **도움말** 메뉴에서 **도움말 콘텐츠 추가 및 제거**를 선택합니다. 

#### 이 작업은 HelpViewer를 시작합니다.

4. HelpViewer에서 기본 설치 원본인 **온라인**을 선택합니다. 
5. 설치할 모든 설명서 옆에 있는 **추가**를 클릭합니다.
6. 화면의 오른쪽 아래에 있는 **업데이트** 단추를 클릭하여 선택한 설명서를 다운로드하고 설치합니다.
![오프라인 콘텐츠 로드](../sql-server/media/load-offline-content.png) 

 >** 중요!!** 업데이트를 클릭하면 HelpViewer가 고정/중단됩니다. 선택한 설명서는 다운로드 및 설치되었습니다. **이 문제를 해결하려면** 작업 관리자에서 HelpViewer를 종료한 다음 위의 3단계에 따라 다시 시작합니다. HelpViewer가 처음 고정/중단될 때 [이러한 단계](https://msdn.microsoft.com/library/mt654096.aspx)도 수행합니다. 이 단계는 한 번만 수행하면 되지만 콘텐츠를 업데이트할 때마다 작업 관리자에서 HelpViewer를 종료해야 합니다.  
6. 도움말/콘텐츠 추가 및 제거를 선택하여 HelpViewer를 다시 시작합니다. 이제 오프라인 설명서를 사용할 준비가 되었습니다!



   ![오프라인 사용 준비 완료](../sql-server/media/offline-ready-to-use.png)


