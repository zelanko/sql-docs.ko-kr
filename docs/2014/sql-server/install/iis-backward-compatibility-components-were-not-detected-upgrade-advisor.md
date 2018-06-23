---
title: IIS 이전 버전과 호환성 구성 요소가 비활성 상태인 검색 됨 (업그레이드 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- IIS [Reporting Services]
ms.assetid: e794185a-0a77-480a-9aea-d09f8760a6b8
caps.latest.revision: 10
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 4eec6ccfad4d83a8b0ec01b77048228dcb4c36b0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081478"
---
# <a name="iis-backward-compatibility-components-were-not-detected-upgrade-advisor"></a>IIS 이전 버전과의 호환성 구성 요소가 검색되지 않음(업그레이드 관리자)
  업그레이드 관리자가 설치 프로그램이 새 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL을 만들기 위해 사용하는 정보를 제공하는 IIS 구성 요소 및 설정을 검색하지 못했습니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.|  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 IIS에 보고서 서버 및 보고서 관리자 가상 디렉터리에 대한 정보를 제공하는 구성 요소가 포함되어 있지만 이러한 구성 요소가 보고서 서버 컴퓨터에 설치되어 있지 않습니다. 업그레이드를 계속 진행할 수는 있지만 업그레이드하는 동안 보고서 서버 또는 보고서 관리자의 URL이 다시 만들어지지 않습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 업그레이드 완료 후 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구를 사용하여 보고서 서버 또는 보고서 관리자의 URL을 설정합니다. IIS 관리자를 사용하여 더 이상 필요하지 않은 가상 디렉터리를 제거합니다.  
  
 자세한 내용은 참조 [URL 구성 &#40;SSRS 구성 관리자&#41; ](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 업그레이드 문제 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  