---
title: 추적 모니터링 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, traces
- XMLA, traces
- monitoring traces [XMLA]
- traces [Analysis Services]
ms.assetid: cdbfb984-18bd-4c4e-8fb7-d64ce298ed35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 678c6d2312261475f4b970b1535ce1faa1f00930
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60156416"
---
# <a name="monitoring-traces-xmla"></a>추적 모니터링(XMLA)
  사용할 수는 [Subscribe](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/subscribe-element-xmla) XMLA (XML for Analysis)의 인스턴스에 정의 된 기존 추적을 모니터링 하려면 명령을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다. `Subscribe` 명령에서는 추적 결과를 행 집합으로 반환합니다.  
  
## <a name="specifying-a-trace"></a>추적 지정  
 [개체](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) 의 속성을 `Subscribe` 명령 중 하나에 대 한 개체 참조를 포함 해야 합니다는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스나에 대 한 추적은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스. `Object` 속성을 지정하지 않거나 `Object` 속성에 추적 식별자를 지정하지 않은 경우 `Subscribe` 명령에서는 명령의 SOAP 헤더에 지정된 명시적 세션에 대한 기본 세션 추적을 모니터링합니다.  
  
## <a name="returning-results"></a>결과 반환  
 `Subscribe` 명령에서는 지정된 추적에 의해 캡처된 추적 이벤트가 포함되어 있는 행 집합을 반환합니다. `Subscribe` 명령을 명령에서 취소 되기 전까지 추적 결과 반환 합니다 [취소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla) 명령입니다.  
  
 행 집합에는 다음 표에 나열된 열이 들어 있습니다.  
  
|Column|데이터 형식|Description|  
|------------|---------------|-----------------|  
|EventClass|정수|추적에 의해 수신된 이벤트의 이벤트 클래스입니다.|  
|EventSubclass|정수(Long)|추적에 의해 수신된 이벤트의 이벤트 하위 클래스입니다.|  
|CurrentTime|DATETIME|이벤트가 시작된 시간입니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|DATETIME|이벤트가 시작된 시간입니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|DATETIME|이벤트가 종료된 시간입니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.<br /><br /> 프로세스 또는 동작의 시작을 설명하는 이벤트 클래스의 경우 이 열은 채워지지 않습니다.|  
|Duration|정수(Long)|이벤트에 소요된 경과 시간(밀리초)입니다.|  
|CPUTime|정수(Long)|이벤트에 소요된 프로세서 시간(밀리초)입니다.|  
|JobID|정수(Long)|프로세스에 대한 작업 식별자입니다.|  
|SessionID|문자열|이벤트가 발생한 세션의 식별자입니다.|  
|SessionType|문자열|이벤트가 발생한 세션의 유형입니다.|  
|ProgressTotal|정수(Long)|이벤트에 의해 보고된 총 진행률입니다.|  
|IntegerData|정수(Long)|이벤트와 연결된 정수 데이터입니다. 이 열의 내용은 이벤트의 이벤트 클래스 및 하위 클래스에 따라 달라집니다.|  
|ObjectID|문자열|이벤트가 발생한 개체의 식별자입니다.|  
|ObjectType|문자열|ObjectName에 지정된 개체의 형식입니다.|  
|ObjectName|문자열|이벤트가 발생한 개체의 이름입니다.|  
|ObjectPath|문자열|이벤트가 발생한 개체의 계층 구조 경로입니다. 이 경로는 ObjectName에 지정된 개체의 부모에 대한 개체 식별자로 구성된 쉼표로 구분된 문자열로 표시됩니다.|  
|ObjectReference|문자열|ObjectName에 지정된 개체에 대한 개체 참조의 XML 표현입니다.|  
|NestLevel|정수|이벤트가 발생한 트랜잭션의 수준입니다.|  
|NumSegments|정수(Long)|이벤트를 발생시킨 명령에서 영향을 받거나 액세스된 데이터 세그먼트의 수입니다.|  
|Severity|정수|이벤트에 대한 예외의 심각도 수준입니다. 이 열 값은 다음 중 하나일 수 있습니다.<br /><br /> 값: 0 = 성공<br /><br /> 값: 1 = 정보<br /><br /> 값: 2 = 경고<br /><br /> 값: 3 = 오류|  
|성공|Boolean|명령의 성공 여부를 나타냅니다.|  
|Error|정수(Long)|이벤트의 오류 번호입니다(해당되는 경우).|  
|ConnectionID|문자열|이벤트가 발생한 연결의 식별자입니다.|  
|DatabaseName|문자열|이벤트가 발생한 데이터베이스의 이름입니다.|  
|NTUserName|문자열|이벤트와 연결된 사용자의 Windows 사용자 이름입니다.|  
|NTDomainName|문자열|이벤트와 연결된 사용자의 Windows 도메인입니다.|  
|ClientHostName|문자열|클라이언트 응용 프로그램을 실행 중인 컴퓨터의 이름입니다. 이 열은 클라이언트 응용 프로그램에서 전달한 값으로 채워집니다.|  
|ClientProcessID|정수(Long)|클라이언트 응용 프로그램의 프로세스 식별자입니다.|  
|ApplicationName|문자열|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 클라이언트 응용 프로그램에서 전달한 값으로 채워집니다.|  
|NTCanonicalUserName|문자열|이벤트와 연결된 사용자의 정식 Windows 사용자 이름입니다.|  
|SPID|문자열|이벤트가 발생한 세션의 SPID(서버 프로세스 ID)입니다. 이 열의 값은 이벤트가 발생한 XMLA 메시지의 SOAP 헤더에 지정된 세션 ID에 직접 해당합니다.|  
|TextData|문자열|이벤트와 연결된 텍스트 데이터입니다. 이 열의 내용은 이벤트의 이벤트 클래스 및 하위 클래스에 따라 달라집니다.|  
|데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면|문자열|이벤트가 발생한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름입니다.|  
|RequestParameters|문자열|이벤트가 발생한 매개 변수가 있는 쿼리 또는 XMLA 명령의 매개 변수입니다.|  
|RequestProperties|문자열|이벤트가 발생한 XMLA 메서드의 속성입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services에서 XMLA를 사용하여 개발](developing-with-xmla-in-analysis-services.md)  
  
  
