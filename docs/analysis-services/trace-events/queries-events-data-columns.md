---
title: "이벤트 데이터 열을 쿼리하여 | Microsoft Docs"
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
- Queries Events event category
ms.assetid: 28aa7df5-3e1f-4f4f-8a1c-8bbd29d5da13
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 48f2e8dec1939bedda904845dd2e56a237ddc10c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="queries-events-data-columns"></a>Queries Events 데이터 열
  Queries Events 이벤트 범주에는 다음과 같은 이벤트 클래스가 있습니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|9|Query Begin|쿼리 시작입니다.|  
|10|쿼리 끝|쿼리를 종료합니다.|  
  
 다음 표에서는 이러한 각 이벤트 클래스에 대한 데이터 열을 나열합니다.  
  
## <a name="query-begin-classdata-columns"></a>Query Begin 클래스 - 데이터 열  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 0: MDXQuery<br /><br /> 1: DMXQuery<br /><br /> 2: SQLQuery<br /><br /> 3: DAXQuery|  
|CurrentTime|2|5|이벤트의 현재 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|이벤트가 시작된 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|ConnectionID|25|1.|쿼리 이벤트와 연결된 고유 연결 ID를 포함합니다.|  
|DatabaseName|28|8|쿼리를 실행하는 데이터베이스의 이름을 포함합니다.|  
|NTUserName|32|8|쿼리 이벤트와 연결된 Windows 사용자 이름을 포함합니다.|  
|NTDomainName|33|8|쿼리 이벤트와 연결된 Windows 도메인 계정을 포함합니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID를 포함합니다.|  
|ApplicationName|37|8|서버 연결을 만든 클라이언트 응용 프로그램의 이름을 포함합니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|  
|SessionID|39|8|XMLA 요청의 세션 고유 ID를 포함합니다.|  
|NTCanonicalUserName|40|8|쿼리 이벤트와 연결된 Windows 사용자 이름을 포함합니다. 이는 정식 사용자 이름으로 engineering.microsoft.com/software/user와 같습니다.|  
|SPID|41|1.|쿼리 이벤트와 연결된 사용자 세션을 고유하게 식별하는 SPID(서버 프로세스 ID)를 포함합니다. SPID는 XMLA에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|쿼리 이벤트와 연결된 텍스트 데이터를 포함합니다.|  
|ServerName|43|8|쿼리 이벤트가 발생한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 포함합니다.|  
|RequestParameters|44|9|쿼리 이벤트와 연결된 매개 변수가 있는 쿼리 및 명령의 매개 변수를 포함합니다.|  
|RequestProperties|45|9|XMLA 요청의 속성을 포함합니다.|  
  
## <a name="query-end-classdata-columns"></a>Query End 클래스 - 데이터 열  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 0: MDXQuery<br /><br /> 1: DMXQuery<br /><br /> 2: SQLQuery<br /><br /> 3: DAXQuery|  
|CurrentTime|2|5|이벤트의 현재 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|이벤트가 시작된 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간을 포함합니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 경과 시간(밀리초)을 포함합니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)을 포함합니다.|  
|Severity|22|1.|쿼리 이벤트와 연결된 예외의 심각도를 포함합니다. 값은 다음과 같습니다.<br /><br /> 0 = 성공<br /><br /> 1 = 알림<br /><br /> 2 = 경고<br /><br /> 3 = 오류|  
|성공|23|1.|쿼리 이벤트의 성공 또는 실패를 포함합니다. 값은 다음과 같습니다.<br /><br /> 0 = 실패<br /><br /> 1 = 성공|  
|오류|24|1.|쿼리 이벤트와 연결된 모든 오류의 오류 번호를 포함합니다.|  
|ConnectionID|25|1.|쿼리 이벤트와 연결된 고유 연결 ID를 포함합니다.|  
|DatabaseName|28|8|쿼리를 실행하는 데이터베이스의 이름을 포함합니다.|  
|NTUserName|32|8|쿼리 이벤트와 연결된 Windows 사용자 이름을 포함합니다.|  
|NTDomainName|33|8|쿼리 이벤트와 연결된 Windows 도메인 계정을 포함합니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID를 포함합니다.|  
|ApplicationName|37|8|서버 연결을 만든 클라이언트 응용 프로그램의 이름을 포함합니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|  
|SessionID|39|8|XMLA 요청의 세션 고유 ID를 포함합니다.|  
|NTCanonicalUserName|40|8|쿼리 이벤트와 연결된 Windows 사용자 이름을 포함합니다. 이는 정식 사용자 이름으로 engineering.microsoft.com/software/user와 같습니다.|  
|SPID|41|1.|쿼리 이벤트와 연결된 사용자 세션을 고유하게 식별하는 SPID(서버 프로세스 ID)를 포함합니다. SPID는 XMLA에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|쿼리 이벤트와 연결된 텍스트 데이터를 포함합니다.|  
|ServerName|43|8|쿼리 이벤트가 발생한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 포함합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Queries Events 범주](../../analysis-services/trace-events/queries-events-category.md)  
  
  

