---
title: "여러 Integration Services 버전을 병렬로 설치 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "상호 운용성 및 공존성 [Integration Services]"
  - "Integration Services, 상호 운용성 및 공존성"
ms.assetid: edfbcd56-012f-462e-a542-95491394fda9
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 41
---
# 여러 Integration Services 버전을 병렬로 설치
  SSIS의 이전 버전과   
      [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services(SSIS)를 병렬로 설치할 수 있습니다. 이 항목에서는 병렬 설치의 몇 가지 제한에 대해 설명합니다.  
  
## 패키지 디자인 및 유지 관리  
 SQL Server 2016, SQL Server 2014 또는 SQL Server 2012를 대상으로 하는 패키지를 디자인하고 유지 관리하려면 Visual Studio 2015dyd SSDT(SQL Server Data Tools)를 사용합니다. SSDT를 다운로드하려면 [최신 SQL Server Data Tools 다운로드](https://msdn.microsoft.com/library/mt204009.aspx)를 참조하세요.  
  
 Integration Services 프로젝트의 속성 페이지에 있는 **구성 속성** 의 **일반**탭에서 **TargetServerVersion** 속성을 선택하고 SQL Server 2016, SQL Server 2014 또는 SQL Server 2012를 선택합니다.  
  
|SQL Server의 대상 버전|SSIS 패키지용 개발 환경|  
|----------------------------------|-----------------------------------------------|  
|2016|Visual Studio 2015용 SQL Server Data Tools|  
|2014|Visual Studio 2015용 SQL Server Data Tools<br /><br /> 또는<br /><br /> SQL Server Data Tools - Visual Studio 2013용 Business Intelligence|  
|2012|Visual Studio 2015용 SQL Server Data Tools<br /><br /> 또는<br /><br /> SQL Server Data Tools - Visual Studio 2012용 Business Intelligence|  
|2008|SQL Server 2008의 Business Intelligence Development Studio|  
  
 기존 프로젝트에 추가하는 기존 패키지는 프로젝트의 대상 형식으로 변환됩니다.  
  
## 패키지 실행  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 **dtexec** 유틸리티 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 이전 버전의 개발 도구에서 만든 Integration Services 패키지를 실행할 수 있습니다. 이러한 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 도구는 이전 버전의 개발 도구에서 개발한 패키지를 로드할 때 일시적으로 메모리 내의 패키지를 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 에서 사용하는 패키지 형식으로 변환합니다. 패키지에 문제가 있어 정상적으로 변환할 수 없는 경우 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 도구는 해당 문제를 해결할 때까지 패키지를 실행할 수 없습니다. 자세한 내용은 [Integration Services 패키지 업그레이드](../../integration-services/install-windows/upgrade-integration-services-packages.md)를 참조하세요.  
  
  