---
title: "명명된 파이프 속성 | Microsoft Docs"
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
  - "파이프 [SQL Server]"
  - "수신 대기 [SQL Server], 파이프"
  - "파이프 [SQL Server], 파이프에 수신 대기"
  - "명명된 파이프 [SQL Server], 파이프에 수신 대기"
ms.assetid: a5fd5b8e-f889-485b-89e3-d4010ec4c6ec
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 32
---
# 명명된 파이프 속성
  명명된 파이프 프로토콜을 사용하는 경우 **명명된 파이프 속성** 대화 상자의 **프로토콜** 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 수신 대기하는 명명된 파이프를 보거나 변경할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 시작해야 합니다.  
  
## 옵션  
 **Enabled**  
 가능한 값은 **예** 및 **아니요**입니다.  
  
 **파이프 이름**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 수신 대기하는 명명된 파이프를 지정합니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은 기본 인스턴스의 경우 `\\.\pipe\sql\query` 에서 수신하고, 명명된 인스턴스의 경우 `\\.\pipe\MSSQL$<instancename>\sql\query` 에서 수신합니다. 이 필드는 2047자로 제한됩니다.  
  
## 대체 명명된 파이프 만들기  
 명명된 파이프를 변경하려면 **파이프 이름** 입력란에 새 파이프 이름을 입력한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 중지하고 다시 시작하십시오. **sql\query**는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 명명된 파이프로 많이 알려졌으므로 파이프를 변경하면 악의적인 프로그램의 공격 위험을 줄일 수 있습니다.  
  
### 예제  
 **\\\\.\pipe\unit\app**을 입력하여 **unit\app** 파이프를 수신 대기합니다.  
  
 **\\\\.\pipe\acct**를 입력하여 **acct** 파이프를 수신 대기합니다.  
  
## 관련 항목:  
 [서버 네트워크 프로토콜 설정 또는 해제](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [네트워크 프로토콜 선택](../Topic/Choosing%20a%20Network%20Protocol.md)   
 [명명된 파이프를 사용하여 유효한 연결 문자열 만들기](../Topic/Creating%20a%20Valid%20Connection%20String%20Using%20Named%20Pipes.md)  
  
  