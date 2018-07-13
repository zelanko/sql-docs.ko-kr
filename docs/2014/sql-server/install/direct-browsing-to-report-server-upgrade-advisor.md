---
title: (업그레이드 관리자) 보고서 서버로 직접 이동 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3d2814a4-318a-45ed-b093-1e852fab561f
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 482fc74e08a60ed7f4d81a450a680c43a9815d5a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196683"
---
# <a name="direct-browsing-to-report-server-upgrade-advisor"></a>보고서 서버로 직접 이동(업그레이드 관리자)
  업그레이드 관리자가 현재 설치를 검색 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버 가상 디렉터리를 직접 검색 됩니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드입니다.|  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 업그레이드 관리자가 현재 설치를 검색 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 예를 들어 보고서 서버 가상 디렉터리에 직접 검색 **http://\<서버 이름 > / ReportServer**합니다. 이는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 현재 버전에서 지원되지 않습니다.  
  
> [!NOTE]  
>  이 규칙은 경고이며 업그레이드가 차단되지 않습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 문서 라이브러리에 대 한 SharePoint 사용자 인터페이스를 사용 하 여 찾아보기 사용할지 **http://\<서버 이름 > / sharepoint 사이트 >/_vti_bin/reportserver**합니다.  
  
  
