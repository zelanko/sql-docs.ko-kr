---
title: "최대 작업자 스레드 수 설정 검사 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "최선의 방법 [데이터베이스 엔진]"
ms.assetid: 2d94adfd-3ba1-493a-b29a-b436f9d583df
caps.latest.revision: 17
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 17
---
# 최대 작업자 스레드 수 설정 검사
  이 규칙은 최대 작업자 스레드 수 서버 옵션에서 발생할 수 있는 잘못된 설정을 검사합니다. 최대 작업자 스레드 수 옵션을 작은 값으로 설정하면 들어오는 클라이언트 요청을 적절한 시간 내에 처리하기 위한 스레드의 수가 부족하게 되어 “스레드 고갈” 상태가 발생할 수 있습니다. 옵션을 큰 값으로 설정하면 주소 공간이 낭비될 수 있습니다. 각 활성 스레드의 소비 공간이 64비트 서버의 경우 최대 4MB에 이르기 때문입니다.  
  
## 최선의 구현 방법 권장 사항  
 최대 작업자 스레드 수 옵션을 0으로 설정합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 사용자 요청에 따라 활성 작업자 스레드의 적정 수를 자동으로 결정합니다.  
  
## 참조 항목  
 [max worker threads 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)  
  
## 참고 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  