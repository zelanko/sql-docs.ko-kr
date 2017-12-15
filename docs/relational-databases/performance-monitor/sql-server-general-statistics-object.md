---
title: "SQL Server, General Statistics 개체 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLServer:General Statistics
- General Statistics object
ms.assetid: c738e549-d7e7-4211-9ec3-064ac140af7c
caps.latest.revision: "26"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1cce63071cd5e87dee3558df803da4388b2af90a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-general-statistics-object"></a>SQL Server, General Statistics 개체
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 **SQLServer:General Statistics** 개체는 현재 연결 수 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하고 연결을 끊은 초당 사용자 수와 같은 서버 차원의 일반적 동작을 모니터링하는 카운터를 제공합니다. 이 개체는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 많은 수의 클라이언트가 연결하고 해제하는 대규모의 OLTP(온라인 트랜잭션 처리) 유형의 시스템에서 작업할 때 유용합니다.  
  
 이 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **General Statistics** 카운터를 설명합니다.  
  
|SQL Server General Statistics 카운터|설명|  
|--------------------------------------------|-----------------|  
|**Active Temp Tables**|사용 중인 임시 테이블/테이블 변수의 수입니다.|  
|**Connection resets/sec**|연결 풀에서 시작된 로그인의 총 수입니다.|  
|**Event Notifications Delayed Drop**|시스템 스레드에서 삭제 대기 중인 이벤트 알림 수입니다.|  
|**HTTP Authenticated Requests**|초당 시작된 인증된 HTTP 요청 수입니다.|  
|**Logical Connections**|시스템에 대한 논리적 연결 수입니다.<br /><br /> 논리적 연결의 주 목적은 MARS(Multiple Active Result Sets) 요청을 처리하는 것입니다. MARS 요청의 경우 응용 프로그램이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결될 때마다 하나의 실제 연결에 해당하는 논리적 연결이 두 개 이상 있을 수 있습니다.<br /><br /> MARS가 사용되지 않는 경우 실제 연결과 논리적 연결의 비율은 1:1입니다. 따라서 응용 프로그램이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결될 때마다 논리적 연결은 1씩 증가합니다.|  
|**Logins/sec**|초당 시작된 총 로그인 수입니다. 풀링된 연결은 포함되지 않습니다.|  
|**Logouts/sec**|초당 시작된 총 로그아웃 작업 수입니다.|  
|**Mars Deadlocks**|발견된 MARS 교착 상태 수입니다.|  
|**Non-atomic yield rate**|초당 생성되는 비원자성 트랜잭션 수입니다.|  
|**Processes blocked**|현재 차단된 프로세스 수입니다.|  
|**SOAP Empty Requests**|초당 시작된 빈 SOAP 요청 수입니다.|  
|**SOAP Method Invocations**|초당 시작된 SOAP 메서드 호출 수입니다.|  
|**SOAP Session Initiate Requests**|초당 시작된 SOAP 세션 시작 요청 수입니다.|  
|**SOAP Session Terminate Requests**|초당 시작된 SOAP 세션 종료 요청 수입니다.|  
|**SOAP SQL Requests**|초당 시작된 SOAP SQL 요청 수입니다.|  
|**SOAP WSDL Requests**|초당 시작된 SOAP 웹 서비스 기술 요청 수입니다.|  
|**SQL Trace IO Provider Lock Waits**|파일 IO 공급자 잠금에 대한 초당 대기 작업 수입니다.| 
|**Temp Tables Creation Rate**|초당 생성된 임시 테이블/테이블 변수의 수입니다.|  
|**Temp Tables For Destruction**|정리 시스템 스레드에 의해 소멸 대기 중인 임시 테이블/테이블 변수의 수입니다.|  
|**Tempdb recovery unit id**|생성된 중복 tempdb 복구 단위 ID 수입니다.|
|**Tempdb rowset id**|생성된 중복 tempdb 행 집합 ID 수입니다.| 
|**Trace Event Notifications Queue**|내부 큐에서 Service Broker를 통해 전송 대기 중인 추적 이벤트 알림 인스턴스의 수입니다.|  
|**트랜잭션**|로컬, DTC 및 바인딩과 같은 트랜잭션 참여 수입니다.|  
|**User Connections**|현재 SQL Server에 연결한 사용자 수입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
