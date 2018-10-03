---
title: Events Data Columns 명령 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Command Events event category
ms.assetid: 7169f1e2-c6be-4d8c-b147-25719b84bc2c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ce551de71785fb947283674771b23399bfc7417f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219913"
---
# <a name="command-events-data-columns"></a>Command Events 데이터 열
  다음 표에서는 **Command Events** 이벤트 범주의 각 이벤트 클래스에 대한 데이터 열을 나열합니다.  
  
 **Command Events** 이벤트 범주에는 다음과 같은 이벤트 클래스가 있습니다.  
  
-   [Command Begin 클래스](#bkmk_1)  
  
-   [Command End 클래스](#bkmk_2)  
  
 다음 표에서는 이러한 각 이벤트 클래스에 대한 데이터 열을 나열합니다.  
  
##  <a name="bkmk_1"></a> Command Begin 클래스 - 데이터 열  
  
|데이터 열|Description|  
|-----------------|-----------------|  
|ConnectionID|명령 이벤트와 연결된 고유 연결 ID를 포함합니다.|  
|TextData|명령 이벤트와 연결된 텍스트 데이터를 포함합니다.|  
|데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면|명령 이벤트가 발생한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 포함합니다.|  
|CurrentTime|명령 이벤트의 현재 시간을 포함합니다.|  
|DatabaseName|명령을 실행하는 데이터베이스의 이름을 포함합니다.|  
|EventSubclass|명령 이벤트 내의 이벤트 클래스를 포함합니다. 값은 다음과 같습니다.<br /><br /> 0: Create<br />1: Alter<br />2: Delete<br />3: Process<br />4: DesignAggregations<br />5: WBInsert<br />6: WBUpdate<br />7: WBDelete<br />8: Backup<br />9: Restore<br />10: MergePartitions<br />11: Subscribe<br />12: Batch<br />13: BeginTransaction<br />14: CommitTransaction<br />15: RollbackTransaction<br />16: GetTransactionState<br />17: Cancel<br />18: Synchronize<br />19: Import80MiningModels<br />20: Attach<br />21: Detach<br />22: SetAuthContext<br />23: ImageLoad<br />24: ImageSave<br />10000: Other|  
|NTUserName|명령 이벤트와 연결된 Windows 사용자 이름을 포함합니다. 이는 정식 사용자 이름으로 engineering.microsoft.com/software/user와 같습니다.|  
|RequestProperties|명령 이벤트와 연결된 XMLA(XML for Analysis) 요청 속성을 포함합니다.|  
|SPID|명령 이벤트와 연결된 사용자 세션을 고유하게 식별하는 SPID(서버 프로세스 ID)를 포함합니다. SPID는 XMLA에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|StartTime|명령 이벤트가 시작된 시간(사용 가능한 경우)을 포함합니다.|  
|SessionType|작업을 발생시킨 엔터티를 포함합니다.|  
|NTDomainName|개체 사용 권한 이벤트와 연결된 Windows 도메인 계정을 포함합니다.|  
|ClientProcessID|명령 이벤트와 연결된 고유 클라이언트 프로세스 ID를 포함합니다.|  
  
##  <a name="bkmk_2"></a> Command End 클래스 - 데이터 열  
  
|데이터 열|Description|  
|-----------------|-----------------|  
|ConnectionID|명령 이벤트와 연결된 고유 연결 ID를 포함합니다.|  
|TextData|명령 이벤트와 연결된 텍스트 데이터를 포함합니다.|  
|데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면|명령 이벤트가 발생한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 포함합니다.|  
|CurrentTime|명령 이벤트의 현재 시간을 포함합니다. 필터링 형식은 *YYYY*-*MM*-*DD* 및 *YYYY*-*MM*-*DD HH*:*MM*:*SS*입니다.|  
|DatabaseName|명령을 실행하는 데이터베이스의 이름을 포함합니다.|  
|Duration|명령 시작 이벤트와 명령 종료 이벤트 간의 추정 시간을 포함합니다.|  
|EndTime|명령 이벤트가 종료된 시간을 포함합니다. 필터링 형식은 *YYYY*-*MM*-*DD* 및 *YYYY*-*MM*-*DD HH*:*MM*:*SS*입니다.|  
|EventSubclass|명령 이벤트 내의 이벤트 클래스를 포함합니다. 값은 다음과 같습니다.<br /><br /> 0: Create<br />1: Alter<br />2: Delete<br />3: Process<br />4: DesignAggregations<br />5: WBInsert<br />6: WBUpdate<br />7: WBDelete<br />8: Backup<br />9: Restore<br />10: MergePartitions<br />11: Subscribe<br />12: Batch<br />13: BeginTransaction<br />14: CommitTransaction<br />15: RollbackTransaction<br />16: GetTransactionState<br />17: Cancel<br />18: Synchronize<br />19: Import80MiningModels<br />20: Attach<br />21: Detach<br />22: SetAuthContext<br />23: ImageLoad<br />24: ImageSave<br />10000: Other|  
|NTCanonicalUserName|명령 이벤트와 연결된 Windows 사용자 이름을 포함합니다. 이는 정식 사용자 이름으로 engineering.microsoft.com/software/user와 같습니다.|  
|NTUserName|명령 이벤트와 연결된 Windows 사용자 계정을 포함합니다.|  
|SPID|명령 이벤트와 연결된 사용자 세션을 고유하게 식별하는 SPID(서버 프로세스 ID)를 포함합니다. SPID는 XMLA에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|StartTime|명령 종료 이벤트가 시작된 시간(사용 가능한 경우)을 포함합니다.|  
|CPUTime|명령 시작 이벤트와 명령 종료 이벤트의 시간 사이에 프로세스에 사용된 CPU 시간(밀리초)을 포함합니다.|  
|Error|명령 이벤트와 연결된 모든 오류의 오류 번호를 포함합니다.|  
|Severity|명령 이벤트와 연결된 예외의 심각도 수준을 포함합니다. 값은 다음과 같습니다.<br /><br /> 0 = 성공<br /><br /> 1 = 알림<br /><br /> 2 = 경고<br /><br /> 3 = 오류|  
|성공|명령 이벤트의 성공 또는 실패 여부를 포함합니다. 값은 다음과 같습니다.<br /><br /> 0 = 실패<br /><br /> 1 = 성공|  
|SessionType|명령 종료 이벤트와 연결된 작업을 발생시킨 엔터티를 포함합니다.|  
|NTDomainName|명령 이벤트와 연결된 Windows 도메인 계정을 포함합니다.|  
|ClientProcessID|명령 이벤트와 연결된 고유 클라이언트 프로세스 ID를 포함합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Command Events 이벤트 범주](command-events-event-category.md)  
  
  
