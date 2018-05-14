---
title: Security Audit Data Columns | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 06bb8b1c6906ebbced1ed7cf52d254564c77d084
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="security-audit-data-columns"></a>Security Audit 데이터 열
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Security Audit 이벤트 범주에는 다음과 같은 이벤트 클래스가 있습니다.  
  
||||  
|-|-|-|  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|1.|Audit Login|클라이언트가 SQL Server의 인스턴스를 실행하는 서버에 대한 연결을 요청하는 경우와 같이 추적이 시작된 이후의 새 연결 이벤트를 모두 수집합니다.|  
|2|Audit Logout|클라이언트가 연결 끊기 명령을 보내는 등 추적이 시작된 이후의 새 연결 끊기 이벤트를 모두 수집합니다.|  
|4|Audit Server Starts And Stops|서비스 종료, 시작 및 일시 중지 동작을 기록합니다.|  
|18|Audit Object Permission Event|개체 사용 권한의 변경 내용을 기록합니다.|  
|19|Audit Admin Operations Event|서버 백업, 복원, 동기화, 연결, 분리, 이미지 로드 및 이미지 저장을 기록합니다.|  
  
 다음 표에서는 이러한 각 이벤트 클래스에 대한 데이터 열을 나열합니다.  
  
## <a name="audit-login"></a>Audit Login  
  
|||||  
|-|-|-|-|  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|Severity|22|1.|예외적인 심각도입니다.|  
|성공|23|1.|1 = 성공, 0 = 실패. 예를 들어 1은 사용 권한 확인에 성공했음을 의미하며 0은 확인에 실패했음을 의미합니다.|  
|오류|24|1.|지정된 이벤트의 오류 번호입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|NTUserName|32|8|Windows 사용자 이름입니다.|  
|NTDomainName|33|8|사용자가 속한 Windows 도메인입니다.|  
|ClientHostName|35|8|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID입니다.|  
|ApplicationName|37|8|서버 연결을 만든 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="audit-logout"></a>Audit Logout  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|  
|성공|23|1.|1 = 성공, 0 = 실패. 예를 들어 1은 사용 권한 확인에 성공했음을 의미하며 0은 확인에 실패했음을 의미합니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|NTUserName|32|8|Windows 사용자 이름입니다.|  
|NTDomainName|33|8|사용자가 속한 Windows 도메인입니다.|  
|ClientHostName|35|8|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID입니다.|  
|ApplicationName|37|8|서버 연결을 만든 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="audit-server-starts-and-stops"></a>Audit Server Starts And Stops  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 1: 인스턴스 종료<br /><br /> 2: 인스턴스 시작<br /><br /> 3: 인스턴스 일시 중지<br /><br /> 4: 인스턴스 계속|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|Severity|22|1.|예외적인 심각도입니다.|  
|성공|23|1.|1 = 성공, 0 = 실패. 예를 들어 1은 사용 권한 확인에 성공했음을 의미하며 0은 확인에 실패했음을 의미합니다.|  
|오류|24|1.|지정된 이벤트의 오류 번호입니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="audit-object-permission-event"></a>Audit Object Permission Event  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|ObjectID|11|8|개체 ID(문자열)입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectName|13|8|개체 이름입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ObjectReference|15|8|개체 참조로, 개체를 설명하는 태그를 사용하여 모든 부모에 대한 XML로 인코딩됩니다.|  
|Severity|22|1.|예외적인 심각도입니다.|  
|성공|23|1.|1 = 성공, 0 = 실패. 예를 들어 1은 사용 권한 확인에 성공했음을 의미하며 0은 확인에 실패했음을 의미합니다.|  
|오류|24|1.|지정된 이벤트의 오류 번호입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
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
  
## <a name="audit-admin-operations-event"></a>Audit Admin Operations Event  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 1: **백업**<br /><br /> 2: **복원**<br /><br /> 3: **동기화**<br /><br /> 4: **분리**<br /><br /> 5: **연결**<br /><br /> 6: **ImageLoad**<br /><br /> 7: **ImageSave**|  
|Severity|22|1.|예외적인 심각도입니다.|  
|성공|23|1.|1 = 성공, 0 = 실패. 예를 들어 1은 사용 권한 확인에 성공했음을 의미하며 0은 확인에 실패했음을 의미합니다.|  
|오류|24|1.|지정된 이벤트의 오류 번호입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
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
 [Security Audit 이벤트 범주](../../analysis-services/trace-events/security-audit-event-category.md)  
  
  
