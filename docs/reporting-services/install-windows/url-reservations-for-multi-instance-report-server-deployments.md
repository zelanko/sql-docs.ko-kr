---
title: "다중 인스턴스 보고서 서버 배포를 위한 URL 예약 | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: URL reservations
ms.assetid: f67c83c0-1f74-42bb-bfc1-e50c38152d3d
caps.latest.revision: "7"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 811e58edf8d0b50e83826c94c5f8f5a54b80c17d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="url-reservations-for-multi-instance-report-server-deployments"></a>다중 인스턴스 보고서 서버 배포를 위한 URL 예약
  같은 컴퓨터에 여러 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스를 설치하는 경우 각 인스턴스의 URL 예약을 어떻게 정의할지 고려해야 합니다. 각 인스턴스 내에서 보고서 서버 웹 서비스와 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 에는 각각 한 개 이상의 URL 예약이 있어야 합니다. 전체 예약 집합은 HTTP.SYS에서 고유해야 합니다.  
  
 중복된 URL은 서비스가 시작할 때 URL을 등록하는 동안 검색됩니다. 고유하지 않은 URL 예약을 만든 경우 서비스를 시작하기 전까지는 이름 충돌이 검색되지 않을 수 있습니다. 따라서 명명 규칙에 따라 모든 값을 고유하게 지정해야 합니다.  
  
## <a name="default-naming-conventions"></a>기본 명명 규칙  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 명명된 인스턴스 내에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치할 수 있습니다. 명명된 인스턴스 내에 보고서 서버를 설치하거나 구성하면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 가 제공하는 기본 URL 예약의 가상 디렉터리에 인스턴스 이름이 자동으로 포함됩니다. 다음 표에서는 기본 인스턴스 및 명명된 인스턴스에 대한 URL 예약을 보여 줍니다.  
  
|SQL Server 인스턴스|기본 URL 예약|  
|-------------------------|-----------------------------|  
|기본 인스턴스(MSSQLServer)|`http://+:80/reportserver`|  
|명명된 인스턴스(MynamedInstance)|`http://+:80/reportserver_MyNamedInstance`|  
  
 명명된 인스턴스의 경우 가상 디렉터리에 해당 인스턴스 이름이 포함됩니다. 기본 인스턴스 및 명명된 인스턴스는 모두 같은 포트에서 수신하지만 고유한 가상 디렉터리 이름에 따라 요청을 수신할 보고서 서버가 결정됩니다.  
  
 보고서 서버 인스턴스를 구별할 수 있는 가상 디렉터리 이름을 사용하는 것이 가장 좋습니다. 이렇게 하면 URL과 대상 인스턴스 간의 관계가 명확해지고 응용 프로그램 이름이 전체 시스템에서 고유하게 됩니다.  
  
## <a name="custom-naming-conventions"></a>사용자 지정 명명 규칙  
 인스턴스 이름을 사용하는 것이 좋지만 URL 구문 및 사용자 지정 명명 규칙을 사용하여 URL 예약의 고유한 이름 제약 조건을 충족할 수도 있습니다. 다음 예에서는 각 인스턴스의 고유한 URL을 만드는 두 가지 방법을 보여 줍니다.  
  
|보고서 서버 기본 인스턴스(MSSQLSERVER)|ReportServer_MyNamedInstance|고유성|  
|----------------------------------------------------|-----------------------------------|----------------|  
|`http://+:80/reportserver`|`http://+:8888/reportserver`|각 인스턴스가 다른 포트에서 수신합니다.|  
|`http://www.contoso.com/reportserver`|`http://SRVR-46/reportserver`|각 인스턴스가 다른 서버 이름(정규화된 도메인 이름 및 컴퓨터 이름)에 응답합니다.|  
  
## <a name="uniqueness-requirements"></a>고유성 요구 사항  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 사용되는 기본 기술에는 고유 이름 관련 요구 사항이 적용됩니다. HTTP.SYS의 리포지토리 내에서 모든 URL이 고유해야 합니다. 포트, 호스트 이름 또는 가상 디렉터리 이름을 변경하여 고유한 URL을 만들 수 있습니다. [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]을 사용하려면 응용 프로그램 ID가 동일한 프로세스 내에서 고유해야 합니다. 이러한 요구 사항은 가상 디렉터리 이름에 영향을 줍니다. 따라서 동일한 보고서 서버 인스턴스 내에서 중복되는 가상 디렉터리 이름을 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 서버 URL 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [URL 구성&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
  
