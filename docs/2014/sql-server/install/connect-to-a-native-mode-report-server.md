---
title: 기본 모드 보고서 서버에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.connectiondialog.F1
helpviewer_keywords:
- report servers [Reporting Services], configuring
ms.assetid: 8b9ea8d3-827c-4011-9e02-be2eac3bb364
caps.latest.revision: 10
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 27b2d2d93d83057fd2de408b4a0cb61dd1cd0771
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321783"
---
# <a name="connect-to-a-native-mode-report-server"></a>기본 모드 보고서 서버에 연결
  이 대화 상자를 사용 하 여 로컬 또는 원격으로 연결할 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버 인스턴스. 이 도구를 사용 하 여 이전 버전의에 연결할 수 없습니다 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버. 한 번에 하나의 인스턴스에만 연결할 수 있습니다.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.  
  
> [!NOTE]  
>  합니다 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager를 구성 및 관리 하지는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드. SharePoint 중앙 관리 및 PowerShell 스크립트를 사용하여 SharePoint 모드에서 보고서 서버를 구성합니다. 자세한 내용은 참조 하세요. [Reporting Services SharePoint 모드 설치 SharePoint 2010 용](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
> [!TIP]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자 (RSConfigTool.exe)는 "highestAvailable"의 권한 수준으로 설치 됩니다. 이 동작은 의도된 것입니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI API와의 통신이 필요합니다. 일부 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] WMI 통신에는 더 높은 수준 또는 관리자 권한이 필요합니다.  
  
-   로컬 보고서 서버 인스턴스에 연결하려면 기본값을 사용하고 **연결**을 클릭합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자가 로컬 서버 이름을 제공하여 기본 인스턴스를 검색합니다. 대부분의 경우 값을 변경할 필요 없이 **연결** 을 클릭할 수 있습니다. 인스턴스를 여러 개 설치한 경우 사용할 인스턴스를 선택합니다.,  
  
-   원격 보고서 서버 인스턴스에 연결하려면 서버 이름을 입력하고 **찾기**를 클릭한 다음 인스턴스를 선택하고 **연결**을 클릭합니다.  
  
 이 대화 상자를 열려면 시작을 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager입니다. 이 대화 상자는 구성 도구를 시작하면 바로 표시됩니다. 자세한 내용은 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **서버 이름**  
 컴퓨터의 네트워크 이름을 입력 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치 됩니다. 이때 컴퓨터 이름만 입력하고 접두사나 슬래시를 포함시키지 마십시오.  
  
 **찾기**  
 **서버 이름**에 지정된 컴퓨터를 찾습니다.  
  
 **보고서 서버 인스턴스**  
 보고서 서버 인스턴스가 여러 개 설치된 경우 연결할 구성 요소를 선택합니다. 유효한 인스턴스만 선택할 수 있습니다. 이전 버전의을 실행 하는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] side-by-side-는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스, 인스턴스 목록에 나타나지 것입니다.  
  
 **연결**  
 지정된 서버와 인스턴스에 연결합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 구성 관리자&#40;기본 모드&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
