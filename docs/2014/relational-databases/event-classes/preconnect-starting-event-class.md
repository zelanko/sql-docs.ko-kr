---
title: PreConnect:Starting 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- PreConnect:Starting Event Class
ms.assetid: d43ed0ad-3dbd-42e0-9cef-8320b8d87497
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0986e654430a47cc494bf1646c222b4888fc105b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63033515"
---
# <a name="preconnectstarting-event-class"></a>PreConnect:Starting 이벤트 클래스
  PreConnect:Starting 이벤트 클래스는 LOGON 트리거나 리소스 관리자 분류자 함수가 언제 실행을 시작하는지 표시합니다.  
  
## <a name="preconnectstarting-event-class-data-columns"></a>PreConnect:Starting 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|`int`|215|27|아니요|  
|SPID|`int`|이 이벤트를 발생시키는 서버 프로세스의 ID입니다.|12|사용자 계정 컨트롤|  
|EventSubClass|`int`|사용자 정의 분류자 함수의 경우 1입니다.|21|사용자 계정 컨트롤|  
|StartTime|`datetime`|사용자 정의 분류자 함수가 시작되는 시간입니다.|14|사용자 계정 컨트롤|  
|ObjectID|`int`|사용자 정의 분류자 개체의 ID입니다.|22|사용자 계정 컨트롤|  
|ObjectName|`nvarchar(256)`|분류자 사용자 정의 함수의 두 부분으로 이루어진 이름입니다(예: dbo.classifier).|34|사용자 계정 컨트롤|  
  
## <a name="see-also"></a>관련 항목  
 [확장 이벤트](../extended-events/extended-events.md)   
 [PreConnect:Completed 이벤트 클래스](preconnect-completed-event-class.md)   
 [리소스 관리자](../resource-governor/resource-governor.md)  
  
  
