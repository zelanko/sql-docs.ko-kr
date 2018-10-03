---
title: 디스크 입/출력 하위 시스템에서 IO 지연 문제 확인 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 23863340-d8e0-48d6-928b-462745885d37
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 59c6c98a9b401b220e912617e9c5693b5d782a2b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48110453"
---
# <a name="check-disk-input-and-output-subsystem-for-io-delay-problems"></a>디스크 입/출력 하위 시스템에서 IO 지연 문제 확인
  이 규칙은 이벤트 로그에서 오류 메시지 833을 검사합니다. 이 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 디스크에서 읽기 또는 쓰기 요청을 실행하여 해당 요청이 반환되는 데 15초 이상 소요되었음을 나타냅니다. 이 오류는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 보고하며 디스크 I/O 하위 시스템에 문제가 있음을 나타냅니다. 이렇게 긴 시간의 지연이 발생하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경의 성능이 심각하게 저하될 수 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 하드웨어 관련 오류 메시지에 대한 시스템 이벤트 로그를 검사하여 이 오류의 문제를 해결합니다. 또한 사용 가능한 경우 하드웨어 관련 로그를 검사합니다.  
  
 성능 모니터를 사용하여 다음 카운터를 검사합니다.  
  
-   Average Disk Sec/Transfer  
  
-   Average Disk Queue Length  
  
-   Current Disk Queue Length  
  
 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 실행하는 컴퓨터의 Average Disk Sec/Transfer는 일반적으로 15밀리초 미만입니다. Average Disk Sec/Transfer 값이 증가하는 경우 이는 디스크 I/O 하위 시스템이 I/O 요구를 최적으로 따라가고 있지 못함을 나타냅니다.  
  
## <a name="for-more-information"></a>참조 항목  
 [MSSQLSERVER_833](../errors-events/mssqlserver-833-database-engine-error.md)  
  
 [Microsoft 기술 자료 문서 897284](http://go.microsoft.com/fwlink/?linkid=117743)  
  
 [SQL Server I/O 기본 사항, 2장(SQL Server I/O Basics, Chapter 2)](http://go.microsoft.com/fwlink/?LinkId=69370)  
  
  
