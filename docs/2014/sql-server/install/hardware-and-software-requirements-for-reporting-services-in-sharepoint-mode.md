---
title: SharePoint 모드의 Reporting Services에 대 한 하드웨어 및 소프트웨어 요구 사항 | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ed91877d-4f74-4266-a932-b824b4810c99
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 56ddfce4fc1812e99870c22eeb0e15be64c5decb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75245631"
---
# <a name="hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode"></a>SharePoint 모드의 Reporting Services에 대한 하드웨어 및 소프트웨어 요구 사항

  이 항목에서는 SharePoint 모드에서 실행 하기 위한 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 필수 구성 요소, 하드웨어 요구 사항 및 설치 고려 사항에 대해 설명 합니다. 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드에는 SharePoint 서버가 필요하기 때문에 대부분의 요구 사항은 SharePoint 환경을 기반으로 합니다. 기본 모드 보고서 서버의 경우 하드웨어가 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]실행에 필요한 최소 하드웨어 및 소프트웨어 요구 사항을 충족해야 합니다. 자세한 내용은 [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)을 참조하세요.  
  
-   [필수 구성 요소](#bkmk_prereq)  
  
-   [보고서 서버 데이터베이스 요구 사항](#bkmk_report_server_database)  
  
-   [파워 뷰 요구 사항](#bkmk_powerview)  
  
-   [추가 정보](#bkmk_more_information)  
  
##  <a name="bkmk_prereq"></a> 필수 조건  
  
-   로컬 설치의 경우 SharePoint 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치 중 로그인된 계정은 로컬 운영 체제의 administrators 그룹의 구성원이어야 합니다. 설치 계정이 SharePoint 팜 관리자 그룹의 구성원이 될 필요는 없습니다.  
  
     자세한 내용은 [SharePoint 2013에서의 계정 권한 및 보안 설정](https://technet.microsoft.com/library/cc678863.aspx)을 참조하세요.  
  
-   SharePoint 모드로 실행 중인 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에는 SharePoint Server가 필요합니다. SharePoint 요구 사항 및 구성에 대한 자세한 내용은 다음을 참조하세요.  
  
    -   [하드웨어 및 소프트웨어 요구 사항 (SharePoint 2013)](https://go.microsoft.com/fwlink/p/?LinkId=256365) (https://go.microsoft.com/fwlink/p/?LinkId=256365)  
  
    -   [SharePoint Server 2013의 용량 관리 및 크기 조정](https://technet.microsoft.com/library/cc261700.aspx)  
  
    -   [비즈니스 인텔리전스에 대 한 소프트웨어 요구 사항 (SharePoint 2013)](https://go.microsoft.com/fwlink/p/?LinkId=256367)  
  
    -   [하드웨어 및 소프트웨어 요구 사항 (SharePoint Server 2010)](https://technet.microsoft.com/library/cc262485\(v=office.14\))  
  
    -   [SharePoint Server 2010의 용량 관리 및 크기 조정](https://technet.microsoft.com/library/cc261700.aspx\(v=office.14\))  
  
-   기존 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 설치를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]으로 업그레이드하거나 업데이트하려는 경우 [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)실행에 필요한 최소 하드웨어 및 소프트웨어 요구 사항을 충족해야 합니다.  
  
-   
  **SharePoint 2013 관리** 서비스를 Windows Server Manager에서 시작했는지 확인합니다.  
  
###  <a name="bkmk_report_server_database"></a>보고서 서버 데이터베이스 요구 사항  
  
-   
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 와 SharePoint 제품 및 기술은 모두 SQL Server 관계형 데이터베이스를 사용하여 애플리케이션 데이터를 저장합니다.  
  
-   
  [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]를 사용하려면 호환되는 SQL Server 버전의 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스가 필요합니다. 하드웨어 및 소프트웨어 요구 사항에 대한 자세한 내용은 [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)을 참조하십시오.  
  
-   SharePoint 제품에서는 기존 데이터베이스 인스턴스를 사용할 수 있습니다. 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스가 설치되지 않은 경우 SharePoint 제품 설치 프로그램은 SharePoint 애플리케이션 데이터베이스에 대해 SQL Server Express Edition을 설치합니다.  
  
-   보고서 서버 인스턴스는 SQL Server Express Edition을 데이터베이스로 사용할 수 없습니다. 그러나 SharePoint 제품에 의해 설치된 SQL Server Express Edition 인스턴스는 다른 데이터베이스 엔진 버전과 함께 있을 수 있습니다.  
  
##  <a name="bkmk_powerview"></a>[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 요구 사항

 Office.Microsoft.com에서 최신 [Power View 설명서](https://office.microsoft.com/excel-help/power-view-explore-visualize-and-present-your-data-HA102835634.aspx) 를 참조하세요. 
  [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]는 Microsoft Excel 2013의 기능이며, Microsoft SharePoint Server 2010 및 2013 Enterprise Edition용 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Reporting Services 추가 기능의 일부입니다.  
  
##  <a name="bkmk_more_information"></a> 자세한 정보

 SharePoint 변경 내용에 대 한 자세한 내용은 [sharepoint 2010에서 sharepoint 2013로 변경](https://technet.microsoft.com/library/ff607742\(office.15\).aspx) ()https://technet.microsoft.com/library/ff607742(office.15).aspx)을 참조 하세요.  
  
 [SQL Server 2014 릴리스 정보](https://go.microsoft.com/fwlink/?LinkID=296445)  
  
