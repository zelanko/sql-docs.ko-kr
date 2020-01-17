---
title: 디스크 IO 하위 시스템에서 IO 지연 문제 확인
description: 이벤트 로그에서 SQL Server 정책 기반 관리의 오류 메시지 833을 확인하여 디스크 IO 하위 시스템에서 IO 지연 문제를 확인하는 정책을 사용하도록 설정하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 23863340-d8e0-48d6-928b-462745885d37
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0cf1dc8196ef8e248da485b01efc4bf192d4248c
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558178"
---
# <a name="check-disk-input-and-output-subsystem-for-io-delay-problems"></a>Check Disk Input and Output Subsystem for IO Delay Problems
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 규칙은 이벤트 로그에서 오류 메시지 833을 검사합니다. 이 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 디스크에서 읽기 또는 쓰기 요청을 실행하여 해당 요청이 반환되는 데 15초 이상 소요되었음을 나타냅니다. 이 오류는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 보고하며 디스크 I/O 하위 시스템에 문제가 있음을 나타냅니다. 이렇게 긴 시간의 지연이 발생하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경의 성능이 심각하게 저하될 수 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 하드웨어 관련 오류 메시지에 대한 시스템 이벤트 로그를 검사하여 이 오류의 문제를 해결합니다. 또한 사용 가능한 경우 하드웨어 관련 로그를 검사합니다.  
  
 성능 모니터를 사용하여 다음 카운터를 검사합니다.  
  
-   Average Disk Sec/Transfer  
  
-   Average Disk Queue Length  
  
-   Current Disk Queue Length  
  
 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 실행하는 컴퓨터의 Average Disk Sec/Transfer는 일반적으로 15밀리초 미만입니다. Average Disk Sec/Transfer 값이 증가하는 경우 이는 디스크 I/O 하위 시스템이 I/O 요구를 최적으로 따라가고 있지 못함을 나타냅니다.  
  
## <a name="for-more-information"></a>참조 항목  
   
  
 [Microsoft 기술 자료 문서 897284](https://go.microsoft.com/fwlink/?linkid=117743)  
  
 [SQL Server I/O 기본 사항, 2장(SQL Server I/O Basics, Chapter 2)](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))
