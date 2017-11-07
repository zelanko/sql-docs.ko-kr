---
title: "Discover Server State Events 데이터 열 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Discover Server State event category
ms.assetid: fbacb187-a4d1-4aa4-be3b-3ddd175f9e19
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c71c32614ee4be7fdbe198530d5ce228452d2276
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="discover-server-state-events-data-columns"></a>Discover Server State Events 데이터 열
  Discover Server State 이벤트 범주에는 다음과 같은 이벤트 클래스가 있습니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|33|Server State Discover Begin|서버 상태 검색이 시작되었습니다.|  
|34|Server State Discover Data|서버 상태 검색 응답의 내용입니다.|  
|35|Server State Discover End|서버 상태 검색이 종료되었습니다.|  
  
 다음 표에서는 이러한 각 이벤트 클래스에 대한 데이터 열을 나열합니다.  
  
## <a name="server-state-discover-begin-classdata-columns"></a>Server State Discover Begin 클래스 - 데이터 열  
  
|||||  
|-|-|-|-|  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 1: **DISCOVER_CONNECTIONS**<br /><br /> 2: **DISCOVER_SESSIONS**<br /><br /> 3: **DISCOVER_TRANSACTIONS**<br /><br /> 6: **DISCOVER_DB_CONNECTIONS**<br /><br /> 7: **DISCOVER_JOBS**<br /><br /> 8: **DISCOVER_LOCKS**<br /><br /> 12: **DISCOVER_PERFORMANCE_COUNTERS**<br /><br /> 13: **DISCOVER_MEMORYUSAGE**<br /><br /> 14: **DISCOVER_JOB_PROGRESS**<br /><br /> 15: **DISCOVER_MEMORYGRANT**|  
|CurrentTime|2|5|서버 상태 검색 이벤트의 현재 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|이벤트가 시작된 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|ConnectionID|25|1.|서버 상태 검색 이벤트와 연결된 고유 연결 ID를 포함합니다.|  
|NTUserName|32|8|서버 상태 검색 이벤트와 연결된 Windows 사용자 계정을 포함합니다.|  
|NTDomainName|33|8|서버 상태 검색 이벤트와 연결된 Windows 도메인 계정을 포함합니다.|  
|ClientProcessID|36|1.|서버 연결을 만든 클라이언트 응용 프로그램의 프로세스 ID를 포함합니다.|  
|ApplicationName|37|8|서버 연결을 만든 클라이언트 응용 프로그램의 이름을 포함합니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|  
|SessionID|39|8|서버 상태 검색 이벤트와 연결된 세션 ID를 포함합니다.|  
|NTCanonicalUserName|40|8|서버 상태 검색 이벤트와 연결된 Windows 사용자 이름을 포함합니다. 이는 정식 사용자 이름으로 engineering.microsoft.com/software/user와 같습니다.|  
|SPID|41|1.|서버 상태 검색 이벤트와 연결된 사용자 세션을 고유하게 식별하는 SPID(서버 프로세스 ID)를 포함합니다. SPID는 XMLA에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터를 포함합니다.|  
|ServerName|43|8|서버 상태 검색 이벤트가 발생한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 포함합니다.|  
|RequestProperties|45|9|현재 XMLA 요청의 속성을 포함합니다.|  
  
## <a name="server-state-discover-data-classdata-columns"></a>Server State Discover Data 클래스 - 데이터 열  
  
|||||  
|-|-|-|-|  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 1: **DISCOVER_CONNECTIONS**<br /><br /> 2: **DISCOVER_SESSIONS**<br /><br /> 3: **DISCOVER_TRANSACTIONS**<br /><br /> 6: **DISCOVER_DB_CONNECTIONS**<br /><br /> 7: **DISCOVER_JOBS**<br /><br /> 8: **DISCOVER_LOCKS**<br /><br /> 12: **DISCOVER_PERFORMANCE_COUNTERS**<br /><br /> 13: **DISCOVER_MEMORYUSAGE**<br /><br /> 14: **DISCOVER_JOB_PROGRESS**<br /><br /> 15: **DISCOVER_MEMORYGRANT**|  
|CurrentTime|2|5|서버 상태 검색 이벤트의 현재 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|이벤트가 시작된 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|ConnectionID|25|1.|서버 상태 검색 이벤트와 연결된 고유 연결 ID를 포함합니다.|  
|SessionID|39|8|서버 상태 검색 이벤트와 연결된 세션 ID를 포함합니다.|  
|SPID|41|1.|서버 상태 검색 이벤트와 연결된 사용자 세션을 고유하게 식별하는 SPID(서버 프로세스 ID)를 포함합니다. SPID는 XMLA에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|검색 요청에 대한 서버 응답과 연결된 텍스트 데이터를 포함합니다.|  
|ServerName|43|8|서버 상태 검색 이벤트가 발생한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 포함합니다.|  
  
## <a name="server-state-discover-end-classdata-columns"></a>Server State Discover End 클래스 - 데이터 열  
  
|||||  
|-|-|-|-|  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 1: **DISCOVER_CONNECTIONS**<br /><br /> 2: **DISCOVER_SESSIONS**<br /><br /> 3: **DISCOVER_TRANSACTIONS**<br /><br /> 6: **DISCOVER_DB_CONNECTIONS**<br /><br /> 7: **DISCOVER_JOBS**<br /><br /> 8: **DISCOVER_LOCKS**<br /><br /> 12: **DISCOVER_PERFORMANCE_COUNTERS**<br /><br /> 13: **DISCOVER_MEMORYUSAGE**<br /><br /> 14: **DISCOVER_JOB_PROGRESS**<br /><br /> 15: **DISCOVER_MEMORYGRANT**|  
|CurrentTime|2|5|서버 상태 검색 이벤트의 현재 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|이벤트가 시작된 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간을 포함합니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)을 포함합니다.|  
|CPUTime|6|2|서버 상태 검색 이벤트에 사용된 CPU 시간(밀리초)을 포함합니다.|  
|ConnectionID|25|1.|서버 상태 검색 이벤트와 연결된 고유 연결 ID를 포함합니다.|  
|NTUserName|32|8|서버 상태 검색 이벤트와 연결된 Windows 사용자 계정을 포함합니다.|  
|NTDomainName|33|8|서버 상태 검색 이벤트와 연결된 Windows 도메인 계정을 포함합니다.|  
|ClientProcessID|36|1.|XMLA 요청을 시작한 클라이언트 응용 프로그램의 프로세스 ID를 포함합니다.|  
|ApplicationName|37|8|서버 연결을 만든 클라이언트 응용 프로그램의 이름을 포함합니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|  
|SessionID|39|8|서버 상태 검색 이벤트와 연결된 Windows 도메인 계정을 포함합니다.|  
|NTCanonicalUserName|40|8|서버 상태 검색 이벤트와 연결된 Windows 사용자 이름을 포함합니다. 이는 정식 사용자 이름으로 engineering.microsoft.com/software/user와 같습니다.|  
|SPID|41|1.|서버 상태 검색 이벤트와 연결된 사용자 세션을 고유하게 식별하는 SPID(서버 프로세스 ID)를 포함합니다. SPID는 XMLA에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|검색 요청에 대한 서버 응답과 연결된 텍스트 데이터를 포함합니다.|  
|ServerName|43|8|서버 상태 검색 이벤트가 발생한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 포함합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Discover Server State Event Category](../../analysis-services/trace-events/discover-server-state-event-category.md)  
  
  

