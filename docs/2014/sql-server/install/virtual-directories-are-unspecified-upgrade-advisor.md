---
title: 가상 디렉터리가 지정 되지 않습니다 (업그레이드 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- virtual directories [Reporting Services]
ms.assetid: 7d32b560-49d6-4558-b5d6-9127067f82d6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: cbadcd0f42f8d5ae81ea2a97625be96214df4ce2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227153"
---
# <a name="virtual-directories-are-unspecified-upgrade-advisor"></a>가상 디렉터리가 지정되지 않음(업그레이드 관리자)
  업그레이드 관리자가 보고서 서버 웹 서비스 또는 보고서 관리자에 대한 가상 디렉터리 설정을 검색하지 못했습니다. 업그레이드가 완료된 후 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 보고서 서버에 대한 URL 예약을 구성해야 합니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.|  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치를 업그레이드하는 동안에는 보고서 서버 웹 서비스 및 보고서 관리자의 새 URL이 예약됩니다. 업그레이드 관리자가 업그레이드할 인스턴스에 대한 보고서 서버 또는 보고서 관리자의 가상 디렉터리를 검색하지 못했기 때문에 업그레이드 프로세스에 업그레이드된 보고서 서버용 URL 예약을 만드는 데 필요한 정보가 충분하지 않습니다. 업그레이드를 계속 진행할 수는 있지만 업그레이드된 설치 후에 보고서 서버 또는 보고서 관리자 가상 디렉터리는 정의되지 않습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 업그레이드 완료 후 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 사용하여 보고서 서버 및 보고서 관리자의 URL을 설정합니다. IIS 관리자를 사용하여 더 이상 필요하지 않은 모든 가상 디렉터리를 제거합니다.  
  
 자세한 내용은 [URL 구성 &#40;SSRS 구성 관리자&#41; ](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl 온라인 설명서.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 업그레이드 문제 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
