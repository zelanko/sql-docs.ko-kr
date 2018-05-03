---
title: File Load and Save 데이터 열 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 0101e809-d6ea-4d0c-95ec-65dd77acf665
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b5fb352769c94efd9d65933df8ac60900cc6970b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="file-load-and-save-data-columns"></a>File Load and Save 데이터 열
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  File Load and Save 이벤트 범주에는 다음 이벤트 클래스가 있습니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|90|파일 로드를 시작합니다.|파일 로드를 시작합니다.|  
|91|파일 로드를 종료합니다.|파일 로드를 종료합니다.|  
|92|파일 저장을 시작합니다.|파일 저장을 시작합니다.|  
|93|파일 저장을 종료합니다.|파일 저장을 종료합니다.|  
|94|PageOut을 시작합니다.|PageOut을 시작합니다.|  
|95|PageOut을 종료합니다.|PageOut을 종료합니다.|  
|96|PageIn을 시작합니다.|PageIn을 시작합니다.|  
|97|PageIn을 종료합니다.|PageIn을 종료합니다.|  
  
 다음 표에서는 이 이벤트 클래스에 대한 데이터 열을 나열합니다.  
  
## <a name="file-load-begin"></a>파일 로드를 시작합니다.  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|JobID|7|1.|진행할 작업 ID입니다.|  
|SessionType|8|8|세션 유형(작업을 유발한 엔터티)입니다.|  
|ObjectID|11|8|개체 ID(문자열)입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectName|13|8|개체 이름입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="file-load-end"></a>파일 로드를 종료합니다.  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|JobID|7|1.|진행할 작업 ID입니다.|  
|SessionType|8|8|세션 유형(작업을 유발한 엔터티)입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectID|11|8|개체 ID(문자열)입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectName|13|8|개체 이름입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|Severity|22|1.|예외적인 심각도입니다.|  
|성공|23|1.|1 = 성공, 0 = 실패. 예를 들어 1은 사용 권한 확인에 성공했음을 의미하며 0은 확인에 실패했음을 의미합니다.|  
|오류|24|1.|지정된 이벤트의 오류 번호입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="file-save-begin"></a>파일 저장을 시작합니다.  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|JobID|7|1.|진행할 작업 ID입니다.|  
|SessionType|8|8|세션 유형(작업을 유발한 엔터티)입니다.|  
|ObjectID|11|8|개체 ID(문자열)입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectName|13|8|개체 이름입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="file-save-end"></a>파일 저장을 종료합니다.  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|JobID|7|1.|진행할 작업 ID입니다.|  
|SessionType|8|8|세션 유형(작업을 유발한 엔터티)입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectID|11|8|개체 ID(문자열)입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectName|13|8|개체 이름입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|Severity|22|1.|예외적인 심각도입니다.|  
|성공|23|1.|1 = 성공, 0 = 실패. 예를 들어 1은 사용 권한 확인에 성공했음을 의미하며 0은 확인에 실패했음을 의미합니다.|  
|오류|24|1.|지정된 이벤트의 오류 번호입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="pageout-begin"></a>PageOut을 시작합니다.  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|JobID|7|1.|진행할 작업 ID입니다.|  
|SessionType|8|8|세션 유형(작업을 유발한 엔터티)입니다.|  
|ObjectID|11|8|개체 ID(문자열)입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectName|13|8|개체 이름입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="pageout-end"></a>PageOut을 종료합니다.  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|JobID|7|1.|진행할 작업 ID입니다.|  
|SessionType|8|8|세션 유형(작업을 유발한 엔터티)입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectID|11|8|개체 ID(문자열)입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectName|13|8|개체 이름입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|Severity|22|1.|예외적인 심각도입니다.|  
|성공|23|1.|1 = 성공, 0 = 실패. 예를 들어 1은 사용 권한 확인에 성공했음을 의미하며 0은 확인에 실패했음을 의미합니다.|  
|오류|24|1.|지정된 이벤트의 오류 번호입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="pagein-begin"></a>PageIn을 시작합니다.  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|JobID|7|1.|진행할 작업 ID입니다.|  
|SessionType|8|8|세션 유형(작업을 유발한 엔터티)입니다.|  
|ObjectID|11|8|개체 ID(문자열)입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectName|13|8|개체 이름입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="pagein-end"></a>PageIn을 종료합니다.  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|CurrentTime|2|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|사용 가능한 경우 이벤트가 시작된 시간입니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간입니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)입니다.|  
|JobID|7|1.|진행할 작업 ID입니다.|  
|SessionType|8|8|세션 유형(작업을 유발한 엔터티)입니다.|  
|IntegerData|10|1.|정수 데이터입니다.|  
|ObjectID|11|8|개체 ID(문자열)입니다.|  
|ObjectType|12|1.|개체 유형입니다.|  
|ObjectName|13|8|개체 이름입니다.|  
|ObjectPath|14|8|개체 경로입니다. 개체의 부모로 시작하는 쉼표로 구분된 부모 목록입니다.|  
|Severity|22|1.|예외적인 심각도입니다.|  
|성공|23|1.|1 = 성공, 0 = 실패. 예를 들어 1은 사용 권한 확인에 성공했음을 의미하며 0은 확인에 실패했음을 의미합니다.|  
|오류|24|1.|지정된 이벤트의 오류 번호입니다.|  
|ConnectionID|25|1.|고유 연결 ID입니다.|  
|DatabaseName|28|8|사용자 문이 실행되는 데이터베이스의 이름입니다.|  
|ClientProcessID|36|1.|클라이언트 응용 프로그램의 프로세스 ID입니다.|  
|SessionID|39|8|세션 GUID입니다.|  
|TextData|42|9|이벤트와 연결된 텍스트 데이터입니다.|  
|ServerName|43|8|이벤트를 생성하는 서버의 이름입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [File Load and Save 이벤트 범주](../../analysis-services/trace-events/file-load-and-save-event-category.md)  
  
  
