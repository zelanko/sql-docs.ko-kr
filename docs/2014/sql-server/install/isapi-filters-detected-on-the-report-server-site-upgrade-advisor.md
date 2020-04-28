---
title: 보고서 서버 사이트에서 ISAPI 필터가 검색 됨 (업그레이드 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- ISAPI filters
- report servers [Reporting Services], upgrade issues
ms.assetid: dd30560d-9e16-47c7-ba68-a9743a657e4e
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: a2b811955839eb22e3325d64c55454b92a6b1b8c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952440"
---
# <a name="isapi-filters-detected-on-the-report-server-site-upgrade-advisor"></a>ISAPI 필터가 보고서 서버 사이트에서 검색됨(업그레이드 관리자)
  업그레이드 관리자가 보고서 서버와 보고서 관리자 가상 디렉터리를 호스팅하는 웹 사이트에서 하나 이상의 ISAPI 필터를 발견했습니다. ISAPI 필터는에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]지원 되지 않습니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]전용.|  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 업그레이드하기 전에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 애플리케이션이 웹 사이트에 대한 ISAPI 필터를 사용하는지 여부를 확인합니다. ISAPI 필터가 필요하지 않으면 보고서 서버를 업그레이드할 수 있습니다. 설치 프로그램은 IIS에서 실행되는 ISAPI 필터에 대한 지원 없이 기본 URL을 만듭니다. ISAPI 필터가 필요하면 ISAPI 필터를 호스팅하는 다른 방법(예: ISA Server를 사용하거나 IIS에서 ISAPI 필터를 계속 호스팅하는 방법)을 찾을 때까지 업그레이드하지 마십시오. 보고서 서버는 특정 시나리오에서 ISAPI 필터의 대체로 ASP.NET HTTPModules를 지원합니다. 자세한 내용은 MSDN에서 ASP.NET 설명서를 참조하십시오.  
  
## <a name="corrective-action"></a>수정 동작  
 배포에 필요한 ISAPI 필터를 호스팅하는 별도의 솔루션을 평가하고 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 관리자를 &#40;업그레이드 문제를 Reporting Services&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
