---
title: Microsoft SQL Server Reporting Services SharePoint 공유 서비스가 함께 설치 됨 (업그레이드 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6ae1017e-129b-4702-9ea7-00ac9b024062
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 529e07dc7beed8dc37741f6c9dab0b0b080d4898
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952689"
---
# <a name="microsoft-sql-server-reporting-services-sharepoint-shared-service-is-installed-side-by-side-upgrade-advisor"></a>Microsoft SQL Server Reporting Services SharePoint 공유 서비스가 병렬로 설치됨(업그레이드 관리자)
  업그레이드 관리자가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 공유 서비스가 이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]와 나란히 설치 되었음을 발견 했습니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 모드.|  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 업그레이드 관리자가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sharepoint 공유 서비스 아키텍처를 기반으로 하지 않는 이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 와 나란히 설치 되어 있음을 발견 했습니다. 컴퓨터에 이전 및 최신 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 관련 기술이 함께 설치되어 있기 때문에 업그레이드가 차단됩니다.  
  
## <a name="corrective-action"></a>수정 동작  
 업그레이드를 계속하려면 기존 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치 중 하나를 제거해야 합니다. 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치 중 하나를 제거한 후 업그레이드 관리자를 다시 실행하여 다른 업그레이드 문제가 없는지 확인합니다.  
  
  
