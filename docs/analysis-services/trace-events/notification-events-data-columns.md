---
title: Notification Events Data Columns | Microsoft Docs
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
- Notification Events event category
ms.assetid: 0ecf06da-1586-415a-9da8-60d4c634f030
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f671eb89295049c09da1f037fdb4544db84b7280
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="notification-events-data-columns"></a>Notification Events 데이터 열
  알림 이벤트는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]사용자가 직접 발생시키지 않는 이벤트입니다. 예를 들어 사용자가 자동 관리 캐싱을 위해 기본 테이블을 업데이트할 때 알림이 발생합니다.  
  
 Notification Events 이벤트 범주에는 다음과 같은 이벤트 클래스가 있습니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|39|알림|알림 이벤트입니다.|  
|40|사용자 정의|사용자 정의 이벤트입니다.|  
  
 다음 표에서는 이 이벤트 클래스에 대한 데이터 열을 나열합니다.  
  
## <a name="notification"></a>알림  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 다음 **하위 클래스 ID**:<br />                      **하위 클래스 이름** 쌍이 정의됩니다.<br /><br /> 0: 자동 관리 캐싱 시작<br /><br /> 1: 자동 관리 캐싱 끝<br /><br /> 2: 비행 레코더 시작<br /><br /> 3: 비행 레코더 중지<br /><br /> 4: 구성 속성 업데이트<br /><br /> 5:SQL 추적<br /><br /> 6: 개체 생성됨<br /><br /> 7: 개체 삭제됨<br /><br /> 8: 개체 변경됨<br /><br /> 9: 자동 관리 캐싱 폴링 시작<br /><br /> 10: 자동 관리 캐싱 폴링 끝<br /><br /> 11: 비행 레코더 스냅숏 시작<br /><br /> 12: 비행 레코더 스냅숏 끝<br /><br /> 13: 자동 관리 캐싱: 알려야 할 개체 업데이트됨<br /><br /> 14: 지연 처리: 처리 시작<br /><br /> 15: 지연 처리: 처리 완료<br /><br /> 16: SessionOpened 이벤트 시작<br /><br /> 17: SessionOpened 이벤트 끝<br /><br /> 18: SessionClosing 이벤트 시작<br /><br /> 19: SessionClosing 이벤트 끝<br /><br /> 20: CubeOpened 이벤트 시작<br /><br /> 21: CubeOpened 이벤트 끝<br /><br /> 22: CubeClosing 이벤트 시작<br /><br /> 23: CubeClosing 이벤트 끝<br /><br /> 24: 트랜잭션 중단 요청|  
|CurrentTime|2|5|알림 이벤트의 현재 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|이벤트가 시작된 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간을 포함합니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|기간|5|2|이벤트에 의해 사용된 시간(밀리초)을 포함합니다.|  
|IntegerData|10|1.|알림 이벤트와 연결된 정수 데이터를 포함합니다. EventSubclass 열이 8일 때 값은 다음과 같습니다.<br /><br /> 1 = 생성됨<br /><br /> 2 = 삭제됨<br /><br /> 3 = 개체 속성이 변경됨<br /><br /> 4 = 개체 자식의 속성이 변경됨<br /><br /> 6 = 자식이 추가됨<br /><br /> 7 = 자식이 삭제됨<br /><br /> 8 = 개체가 완전히 처리됨<br /><br /> 9 = 개체가 부분적으로 처리됨<br /><br /> 10 = 개체가 처리되지 않음<br /><br /> 11 = 개체가 완전히 최적화됨<br /><br /> 12 = 개체가 부분적으로 최적화됨<br /><br /> 13 = 개체가 최적화되지 않음|  
|ObjectID|11|8|이 알림이 실행된 개체 ID를 포함하며 문자열 값입니다.|  
|ObjectType|12|1.|알림 이벤트와 연결된 개체 유형을 포함합니다.|  
|ObjectName|13|8|알림 이벤트와 연결된 개체 이름을 포함합니다.|  
|ObjectPath|14|8|알림 이벤트와 연결된 개체 경로를 포함합니다. 경로는 개체의 부모로 시작하는 쉼표로 구분된 부모 목록으로 반환됩니다.|  
|ObjectReference|15|8|진행률 보고서 종료 이벤트에 대한 개체 참조를 포함합니다. 개체 참조는 개체를 설명하는 태그를 통해 모든 부모에 의해 XML로 인코딩됩니다.|  
|ConnectionID|25|1.|알림 이벤트와 연결된 고유 연결 ID를 포함합니다.|  
|DatabaseName|28|8|알림 이벤트가 발생한 데이터베이스의 이름을 포함합니다.|  
|NTUserName|32|8|알림 이벤트와 연결된 Windows 사용자 이름을 포함합니다.|  
|NTDomainName|33|8|사용자가 속한 Windows 도메인입니다.|  
|SessionID|39|8|알림 이벤트와 연결된 세션 ID를 포함합니다.|  
|NTCanonicalUserName|40|8|알림 이벤트와 연결된 Windows 사용자 이름을 포함합니다. 이는 정식 사용자 이름으로 engineering.microsoft.com/software/user와 같습니다.|  
|SPID|41|1.|알림 이벤트와 연결된 사용자 세션을 고유하게 식별하는 SPID(서버 프로세스 ID)를 포함합니다. SPID는 XMLA에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|알림 이벤트와 연결된 텍스트 데이터를 포함합니다.|  
|ServerName|43|8|알림 이벤트가 발생한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 포함합니다.|  
|RequestProperties|45|9|XMLA 요청의 속성을 포함합니다.|  
  
## <a name="user-defined"></a>사용자 정의  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1.|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1.|1.|각 이벤트 클래스에 대한 추가 정보를 제공하는 특정 사용자 이벤트 하위 클래스입니다.|  
|CurrentTime|2|5|알림 이벤트의 현재 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|IntegerData|10|1.|특정 사용자 정의 이벤트 정보입니다.|  
|ConnectionID|25|1.|알림 이벤트와 연결된 고유 연결 ID를 포함합니다.|  
|DatabaseName|28|8|알림 이벤트가 발생한 데이터베이스의 이름을 포함합니다.|  
|NTUserName|32|8|알림 이벤트와 연결된 Windows 사용자 이름을 포함합니다.|  
|NTDomainName|33|8|사용자가 속한 Windows 도메인입니다.|  
|SessionID|39|8|알림 이벤트와 연결된 세션 ID를 포함합니다.|  
|NTCanonicalUserName|40|8|알림 이벤트와 연결된 Windows 사용자 이름을 포함합니다. 이는 정식 사용자 이름으로 engineering.microsoft.com/software/user와 같습니다.|  
|SPID|41|1.|알림 이벤트와 연결된 사용자 세션을 고유하게 식별하는 SPID(서버 프로세스 ID)를 포함합니다. SPID는 XMLA에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|알림 이벤트와 연결된 텍스트 데이터를 포함합니다.|  
|ServerName|43|8|알림 이벤트가 발생한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 포함합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Notification Events Event Category](../../analysis-services/trace-events/notification-events-event-category.md)  
  
  
