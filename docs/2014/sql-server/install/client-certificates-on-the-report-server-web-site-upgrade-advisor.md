---
title: 보고서 서버 웹 사이트 (업그레이드 관리자)에서 클라이언트 인증서 | Microsoft Docs
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
- report servers [Reporting Services], upgrade issues
ms.assetid: 5ecce26b-99df-4109-8e51-d150d369dff7
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 4d08cf58e6908aa8aba187e1e192a05b85b95c96
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082408"
---
# <a name="client-certificates-on-the-report-server-web-site-upgrade-advisor"></a>보고서 서버 웹 사이트의 클라이언트 인증서(업그레이드 관리자)
  업그레이드 관리자가 보고서 서버 또는 보고서 관리자 가상 디렉터리를 호스팅하는 IIS 웹 사이트에서 하나 이상의 클라이언트 인증서를 검색했습니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.|  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서는 사용자를 인증하는 데 클라이언트 인증서를 사용하도록 지원하지 않습니다. 업그레이드를 계속 진행할 수는 있지만 클라이언트 인증서는 업그레이드된 보고서 서버에서 사용되지 않습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 ISA Server와 같은 별도의 솔루션을 사용하여 클라이언트 인증서 인증 요구 사항을 해결합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 업그레이드 문제 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  