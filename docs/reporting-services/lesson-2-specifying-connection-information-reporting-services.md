---
title: "2 단원: 연결 정보 (Reporting Services)를 지정 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 05/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
caps.latest.revision: 53
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4d0667dec1b59d5560ca24176634dddc5d6d8d18
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>2단원: 연결 정보 지정(Reporting Services)
추가한 후 한 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 페이지가 매겨진 보고서로 1 단원에서에서 자습서 프로젝트를 정의 하면 이제는 *데이터 소스*, 연결 정보가 보고서에는 관계형 데이터베이스, 다차원 데이터베이스 또는 다른 원본에서 데이터에 액세스 사용 될 수 있습니다.  
  
이 단원에서는 사용 하 여는 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 데이터 원본으로 예제 데이터베이스. 이 자습서에서는이 데이터베이스의 기본 인스턴스에 위치 하 가정 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 로컬 컴퓨터에 설치 합니다.  
  
### <a name="to-set-up-a-connection"></a>연결을 설정하려면  
  
1.  에 **보고서 데이터** 창에서 클릭 **새로** 클릭 하 고 **데이터 소스**합니다.  
**보고서 데이터** 창이 표시되지 않는 경우 **보기** 메뉴에서 **보고서 데이터**를 클릭합니다.  

    ![ssrs-table-tutorial-2-new-data-source](../reporting-services/media/ssrs-table-tutorial-2-new-data-source.png)
  
   2.  **이름**에 *AdventureWorks2014*를 입력합니다.  
  
3.  **포함된 연결** 이 선택되어 있는지 확인합니다.  
  
4.  **유형**에서 **Microsoft SQL Server**를 선택합니다.  
  
5.  **연결 문자열**에서 다음과 같이 입력합니다.  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
     이 연결 문자열에서는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], 보고서 서버 및 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 데이터베이스가 모두 로컬 컴퓨터에 설치되어 있고 사용자에게 [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 데이터베이스에 로그온할 수 있는 권한이 있다고 가정합니다. AdventureWorks2014 데이터베이스는 로컬 컴퓨터에 없는 경우 연결 문자열을 변경 하 고 대체 *localhost* 와 데이터베이스 서버 인스턴스의 이름입니다.
  
     >[!NOTE]  
    >[!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services 또는 명명된 인스턴스를 사용하는 경우에는 연결 문자열에 인스턴스 정보가 포함되어야 합니다.  
    >  
    >`Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2014`  
    >  
    >연결 문자열에 대한 자세한 내용은 다음을 참조하세요. [Data Connections, Data Sources, and Connection Strings in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)을 클릭합니다.  
     
  
6.  왼쪽 창에서 **자격 증명** 을 클릭하고 **Windows 인증 사용(통합 보안)**을 클릭합니다.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)] 데이터 원본 **AdventureWorks2014** 는 **보고서 데이터** 창에 추가되었습니다.  
![ssrs_adventureworks_datasource](../reporting-services/media/ssrs-adventureworks-datasource.png)  
## <a name="next-task"></a>다음 태스크  
[!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] 샘플 데이터베이스에 대한 연결이 정의되었습니다. 다음 단원에서는 보고서를 만듭니다. [3단원: 테이블 보고서에 대한 데이터 집합 정의&#40;Reporting Services&#41;](../reporting-services/lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[Data Connections, Data Sources, and Connection Strings in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
  


