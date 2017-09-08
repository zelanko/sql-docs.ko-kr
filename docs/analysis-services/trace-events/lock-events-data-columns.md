---
title: "Events Data Columns 잠금 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c223157f-41a0-405c-bc1a-41c999506936
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9a211ed540b3bddb11c5d84cf0db65ef3dade1ad
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="lock-events-data-columns"></a>Lock 이벤트 데이터 열
  Lock 이벤트 범주에는 다음과 같은 이벤트 클래스가 있습니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|50|Deadlock|교착 상태에 있는 현재 잠금에 대한 정보입니다.|  
|51|Lock Timeout|최근에 시간 초과된 잠금에 대한 정보입니다.|  
|52|Lock Acquired|최근에 획득된 잠금에 대한 정보입니다.|  
|53|Lock Released|최근에 해제된 잠금에 대한 정보입니다.|  
|54|Lock Waiting|다른 잠금을 기다리고 있는 잠금에 대한 정보입니다.|  
  
 다음 표에서는 이 이벤트 클래스에 대한 데이터 열을 나열합니다.  
  
## <a name="deadlock"></a>Deadlock  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="lock-timeout"></a>Lock Timeout  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|NTUserName|32|8|Windows 사용자 이름입니다.|  
|NTDomainName|33|8|사용자가 속한 Windows 도메인입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="lock-acquired"></a>Lock Acquired  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|NTUserName|32|8|Windows 사용자 이름입니다.|  
|NTDomainName|33|8|사용자가 속한 Windows 도메인입니다.|  
|ClientHostName|35|8|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID입니다.|  
|ApplicationName|37|8|서버 연결을 만든 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="lock-released"></a>Lock Released  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|NTUserName|32|8|Windows 사용자 이름입니다.|  
|NTDomainName|33|8|사용자가 속한 Windows 도메인입니다.|  
|ClientHostName|35|8|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID입니다.|  
|ApplicationName|37|8|서버 연결을 만든 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="lock-waiting"></a>Lock Waiting  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|NTUserName|32|8|Windows 사용자 이름입니다.|  
|NTDomainName|33|8|사용자가 속한 Windows 도메인입니다.|  
|ClientHostName|35|8|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID입니다.|  
|ApplicationName|37|8|서버 연결을 만든 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1.|서버 프로세스 ID로, 사용자 세션을 고유하게 식별합니다. 이 SPI는 XML/A에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [잠금 이벤트 범주](../../analysis-services/trace-events/lock-events-category.md)  
  
  
