---
title: 보고서 서버로 직접 탐색 (업그레이드 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3d2814a4-318a-45ed-b093-1e852fab561f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9a12f39bc399e2c46e61fc290bb20ad2c43e4de9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012546"
---
# <a name="direct-browsing-to-report-server-upgrade-advisor"></a>보고서 서버로 직접 이동(업그레이드 관리자)
  업그레이드 관리자가 현재 설치 된에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버 가상 디렉터리로 직접 검색 하 고 있음을 발견 했습니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]SharePoint 모드.|  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 업그레이드 관리자가 현재 설치 된에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버 가상 디렉터리 (예: **http:// \<server name> /reportserver**)로 직접 검색 하 고 있음을 발견 했습니다. 이는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 현재 버전에서 지원되지 않습니다.  
  
> [!NOTE]  
>  이 규칙은 경고이며 업그레이드가 차단되지 않습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 문서 라이브러리에 대 한 SharePoint 사용자 인터페이스를 사용 하 여 찾아보거나 **http:// \<server name> /sharepoint site>/_vti_bin/sharepoint**를 사용 합니다.  
  
  
