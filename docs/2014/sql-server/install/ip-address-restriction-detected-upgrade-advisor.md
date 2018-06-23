---
title: IP 주소 제한이 검색 됨 (업그레이드 관리자) | Microsoft Docs
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
ms.assetid: 9a154455-c68f-4403-a3a7-b90f4d35eecb
caps.latest.revision: 10
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: b3ab784e15737a08b9bf928d6d15e08a27636b88
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089452"
---
# <a name="ip-address-restriction-detected-upgrade-advisor"></a>IP 주소 제한이 검색됨(업그레이드 관리자)
  업그레이드 관리자가 보고서 서버 또는 보고서 관리자 가상 디렉터리를 호스팅하는 IIS 웹 사이트에서 하나 이상의 IP 주소 제한을 검색했습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]는 IP 주소 제한에 대한 기본 지원을 제공하지 않습니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 네이티브 합니다.|  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 설치 프로그램이 업그레이드된 보고서 서버용으로 생성된 URL에 대한 IP 주소 제한을 정의할 수 없습니다. 업그레이드를 계속 진행할 수는 있지만 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL에 대한 IP 주소 제한은 정의되지 않습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 업그레이드 후 ISA Server, 방화벽 소프트웨어 또는 다른 솔루션을 사용하여 특정 IP 주소에서 보고서 서버로의 요청을 허용하거나 실행합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 업그레이드 문제 &#40;업그레이드 관리자&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  