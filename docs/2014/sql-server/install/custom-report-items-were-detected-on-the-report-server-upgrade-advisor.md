---
title: 보고서 서버 (업그레이드 관리자)에서 사용자 지정 보고서 항목이 검색 됨 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- custom report items, upgrading
ms.assetid: aee32006-65b2-4dfe-9570-d85a249d17b2
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: c971c8e19c6881cdc172a4e5c29952a1f829912a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48170763"
---
# <a name="custom-report-items-were-detected-on-the-report-server-upgrade-advisor"></a>보고서 서버에서 사용자 지정 보고서 항목이 검색됨(업그레이드 관리자)
  사용자 지정 보고서 항목의 이전 버전에 대해 만들어진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 와 호환 되지 않습니다 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]합니다. 업그레이드는 계속할 수 있지만 사용자 지정 보고서 항목을 사용하는 보고서는 올바르게 실행되지 않습니다. 업그레이드 관리자에서 사용자 지정 보고서 항목이 검색되었습니다. 업그레이드를 계속할 수 있지만 업그레이드 완료 후 사용자 지정 보고서 항목 파일을 새 설치 폴더에 수동으로 이동해야 합니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드|  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 업그레이드 관리자가 구성 파일에서 사용자 지정 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 확장 프로그램 설정을 검색했으며, 이는 보고서에 대한 하나 이상의 사용자 지정 어셈블리가 사용자 설치에 포함되어 있음을 나타냅니다.  
  
## <a name="corrective-action"></a>수정 동작  
 업그레이드가 완료된 후 사용자 지정 보고서 항목 파일을 새 설치 폴더에 수동으로 이동해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 업그레이드 문제 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
