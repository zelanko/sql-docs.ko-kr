---
title: "병합 구독자의 파티션 정보 유효성 검사 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "병합 복제 데이터 유효성 검사 [SQL Server 복제], 파티션"
  - "매개 변수가 있는 필터 [SQL Server 복제], 파티션 정보 유효성 검사"
  - "파티션 정보 유효성 검사"
ms.assetid: c059553e-df2c-4333-ba79-e8d6e2890c34
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 병합 구독자의 파티션 정보 유효성 검사
  병합 게시에 대해 매개 변수가 있는 행 필터를 정의할 때는 구독자의 로그인 이름과 같이 구독자 정보를 참조하는 기능을 사용합니다. 기본적으로 복제는 각 동기화 전과 스냅숏이 구독자에 적용될 때마다 이러한 기능에 기반하여 구독자 정보의 유효성을 검사합니다. 유효성 검사 프로세스는 데이터가 각 구독자에 대해 올바르게 분할되었는지 확인합니다. 유효성 검사 동작에 의해 제어 되는 **validate_subscriber_info** 게시 속성을 사용 하 여 변경 될 수 있는 [sp_changemergepublication (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) 에 **구독 옵션** 의 페이지는 **게시 속성** 대화 상자입니다. 게시 속성 변경 방법은 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하십시오.  
  
## 파티션 유효성 검사 작동 방법  
 게시를 필터링 할 때, 예를 들어 함수를 사용 하 여 **suser_sname ()**, 병합 에이전트에 유효한 데이터를 기반으로 하는 각 구독자에 초기 스냅숏을 적용는 **suser_sname ()** 식입니다.  
  
 유효성 검사를 활성화하면 구독자가 다음 동기화를 위해 게시자에 다시 연결할 때 병합 에이전트가 구독자에서 정보의 유효성을 검사하고 각 구독자의 파티션이 초기 스냅숏에서 수신한 파티션과 동일한지 확인합니다. 각 후속 병합 또는 스냅숏 응용 프로그램의 경우에는 병합 에이전트가 각 구독자 파티션의 유효성을 검사합니다.  
  
 필터링 식에 사용된 함수에서 반환된 값이 초기 스냅숏에 반환된 값과 다른 것을 병합 에이전트가 감지하면 병합 또는 스냅숏 응용 프로그램이 실패하고 해당 구독자의 구독을 다시 초기화해야 할 수 있습니다. 구독자의 병합 설정을 변경할 때 문제가 발생하지 않도록 하기 위해 재초기화가 필요할 수 있지만 로그인 이름과 같은 구독자의 정보를 원래 스냅숏에서 사용된 값으로 다시 변경만 해도 됩니다.  
  
 병합 에이전트가 파티션의 유효성을 검사할 때 필터링 식에 사용된 함수에서 반환한 값에 대해 파티션의 유효성을 검사하는 것 외에도 에이전트는 메타데이터 정리 작업 또는 스키마 변경과 같이 스냅숏을 무효화한 변경 작업 이전에 스냅숏이 생성되었는지 여부도 확인합니다. 분할된 스냅숏이 너무 오래된 경우 병합 에이전트는 오류를 표시하고 이로 인해 현재 일반 스냅숏에 기반하여 해당 구독자에 대해 분할된 스냅숏을 다시 생성해야 합니다.  
  
## 참고 항목  
 [관리 및 #40입니다. 복제 및 #41;](../../relational-databases/replication/administration/administration-replication.md)   
 [최선의 복제 관리 방법](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [복제된 데이터의 유효성 검사](../../relational-databases/replication/validate-replicated-data.md)  
  
  