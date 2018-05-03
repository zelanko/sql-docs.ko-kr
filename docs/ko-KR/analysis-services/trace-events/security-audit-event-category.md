---
title: Security Audit 이벤트 범주 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [Analysis Services], security audit
- security events [Analysis Services]
ms.assetid: 9686a495-68d7-4137-8e30-2655aa519f6c
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1d4136c84692e1e2a171a11c867598a7b2c51c34
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="security-audit-event-category"></a>Security Audit 이벤트 범주
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Security Audit 이벤트 범주에는 다음 표에 설명된 이벤트 클래스가 있습니다.  
  
|Event Class|이벤트 ID|Description|  
|-----------------|--------------|-----------------|  
|Audit Login|1.|클라이언트가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 인스턴스를 실행하는 서버에 대한 연결을 요청하는 경우와 같이 추적이 시작된 이후의 새 연결 이벤트를 모두 기록합니다.|  
|Audit Logout|2|클라이언트가 연결 끊기 명령을 보내는 등 추적이 시작된 이후의 새 연결 끊기 이벤트를 모두 기록합니다.|  
|Audit Server Starts and Stops|4|서비스의 종료, 시작 및 일시 중지 동작을 기록합니다.|  
|Audit Object Permission Event|18|개체 사용 권한의 변경 내용을 모두 기록합니다.|  
|Audit Admin Operations Event|19|백업, 복원, 동기화, 연결, 분리, 이미지 로드 및 이미지 저장에 대한 서버 작업을 기록합니다.|  
  
 각각의 Security Audit 이벤트 클래스와 연관된 열에 대한 자세한 내용은 [Security Audit Data Columns](../../analysis-services/trace-events/security-audit-data-columns.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 추적 이벤트](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
