---
title: Windows 응용 프로그램 로그 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Windows application logs [Reporting Services]
- logs [Reporting Services], Windows application logs
- application logs [Reporting Services]
ms.assetid: 742fd00e-aa6c-4c8a-b58f-c03c489b1699
caps.latest.revision: 31
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5cc0848226b80c2c77345ed737f8acff68eba5bc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150064"
---
# <a name="windows-application-log"></a>Windows 응용 프로그램 로그
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 이벤트 메시지를 Windows 응용 프로그램 로그에 기록합니다. 응용 프로그램 로그에 기록된 메시지 정보를 사용하여 로컬 시스템에서 실행되는 보고서 서버 응용 프로그램에서 생성된 이벤트를 확인할 수 있습니다.  
  
## <a name="viewing-report-server-events"></a>보고서 서버 이벤트 보기  
 이벤트 뷰어를 사용하여 로그 파일을 보고 로그 파일에 들어 있는 메시지를 필터링할 수 있습니다. 이벤트 메시지에 대 한 자세한 내용은 참조 하세요. [오류 및 이벤트 참조 &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)합니다. Windows 응용 프로그램 로그나 이벤트 뷰어에 대한 자세한 내용은 Windows 제품 설명서를 참고하십시오.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 다음과 같은 세 가지 이벤트 원본을 제공합니다.  
  
-   보고서 서버(보고서 서버 Windows 서비스)  
  
-   보고서 관리자  
  
-   일정 예약 및 배달 프로세서  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 보고서 서버의 응용 프로그램 이벤트 로깅을 해제하거나 기록 대상 이벤트를 변경할 수 없습니다. 보고서 서버 이벤트 로깅을 설명하는 스키마는 고정되어 있습니다. 사용자 지정 이벤트를 지원하도록 스키마를 확장할 수 없습니다.  
  
 다음 표에서는 보고서 서버에서 응용 프로그램 이벤트 로그에 기록하는 이벤트 유형을 설명합니다.  
  
|이벤트 유형|Description|  
|----------------|-----------------|  
|정보|성공한 작업을 보여 주는 이벤트(예: 보고서 서버 서비스 시작 시간)|  
|경고|잠재적인 문제를 나타내는 이벤트(예: 디스크 공간 부족)|  
|Error|중요한 문제점을 보여 주는 이벤트(예: 서비스가 시작되지 않았음)|  
|성공 감사|성공적인 로그온을 보여 주는 보안 이벤트|  
|실패 감사|로그온 시도가 실패할 때 기록되는 이벤트|  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 로그 파일 및 소스](../report-server/reporting-services-log-files-and-sources.md)   
 [오류 및 이벤트 참조 &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
