---
title: 가상 디렉터리에 지원 되지 않는 인증 방법 있음 (업그레이드 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- virtual directories [Reporting Services]
ms.assetid: 216eca6f-9a66-42e1-aa54-dcf99cec9f7d
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 26420df466860677f22d39d57133568a2f02bc68
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952014"
---
# <a name="virtual-directory-has-unsupported-authentication-method-upgrade-advisor"></a>가상 디렉터리에 지원되지 않는 인증 방법이 있음(업그레이드 관리자)
  업그레이드 관리자가 보고서 관리자 또는 보고서 서버 가상 디렉터리에서 지원되지 않는 인증 방법을 검색했습니다. 업그레이드를 지원하지 않는 인증 방법에는 익명, 다이제스트 및 .NET Passport가 있습니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.|  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>설명  
 설치 프로그램은 다음 인증 방법 중 하나를 사용하는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설치를 업그레이드할 수 없습니다.  
  
-   익명  
  
-   다이제스트  
  
-   .NET Passport  
  
 계속하려면 인터넷 정보 서비스(IIS)의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 가상 디렉터리에 지정된 인증 방법을 수정하거나 설치를 마이그레이션하면 됩니다. 설치를 마이그레이션하는 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서를 참조하십시오.  
  
## <a name="corrective-action"></a>수정 동작  
 업그레이드를 계속하려면 ReportServer 및 Reports 가상 디렉터리에 대한 IIS의 인증 방법을 수정합니다. 인증 방법 수정은 IIS 설명서를 참조하십시오. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 가상 디렉터리의 인증 방법을 수정한 후에는 업그레이드 관리자를 다시 실행하여 다른 업그레이드 문제가 없는지 확인합니다.  
  
## <a name="see-also"></a>관련 항목  
 [업그레이드 문제 &#40;Reporting Services 업그레이드 관리자&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
