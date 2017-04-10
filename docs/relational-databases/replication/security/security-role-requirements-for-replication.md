---
title: "복제용 보안 역할 요구 사항 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "보안 [SQL Server 복제], 역할"
  - "역할 [SQL Server], 복제"
ms.assetid: b324a80f-4319-4cb2-847b-1910c49d90e0
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 복제용 보안 역할 요구 사항
  복제는 사용자의 로그인이 매핑된 역할에 따라 해당 사용자가 수행할 수 있는 동작을 제한합니다. 복제에는 특정 한 사용 권한을 부여한는 **sysadmin** 고정 서버 역할의 **db_owner** 게시 액세스 목록 (PAL)에 고정 데이터베이스 역할 및 로그인 합니다.  
  
## 복제 설정에 대한 보안 역할 요구 사항  
 다음 표에서는 일반적인 복제 설정 태스크에 필요한 인증 수준을 요약하여 보여 줍니다.  
  
|설정 태스크|멤버 요구 사항|  
|----------------|----------------------------|  
|배포자, 게시자 또는 구독자 설정|게시자에 대한**sysadmin** 서버 역할|  
|데이터베이스 복제 설정|게시자에 대한**sysadmin** 서버 역할|  
|게시 생성|**db_owner** 게시자에서 게시 데이터베이스의 데이터베이스 역할 또는 **sysadmin** 게시자에 대 한 서버 역할입니다.|  
|게시 속성 보기|게시자의 PAL의 멤버 **db_owner** 게시자의 게시 데이터베이스의 데이터베이스 역할 또는 **sysadmin** 게시자에 대 한 서버 역할입니다.|  
|구독 생성|**db_owner** 게시자에서 게시 데이터베이스의 데이터베이스 역할 또는 **sysadmin** 게시자에 대 한 서버 역할입니다.<br /><br /> **db_owner** 구독자에서 구독 데이터베이스의 데이터베이스 역할 또는 **sysadmin** 구독자에서 서버 역할입니다.|  
|에이전트 프로필 구성|배포자에 대한**sysadmin** 서버 역할|  
  
## 복제 유지 관리에 대한 보안 역할 요구 사항  
 다음 표에서는 일반적인 복제 유지 관리 태스크에 필요한 인증 수준을 요약하여 보여 줍니다.  
  
|유지 관리 태스크|멤버 요구 사항|  
|----------------------|----------------------------|  
|배포자, 게시자 또는 구독자 수정 또는 삭제|해당 서버에 대한**sysadmin** 서버 역할|  
|게시 수정 또는 삭제|**db_owner** 게시자에서 게시 데이터베이스의 데이터베이스 역할 또는 **sysadmin** 게시자에 대 한 서버 역할입니다.|  
|게시자에서 구독 수정 또는 삭제|**db_owner** 게시자에서 게시 데이터베이스의 데이터베이스 역할 또는 **sysadmin** 게시자에 대 한 서버 역할입니다.|  
|구독자에서 구독 수정 또는 삭제|**db_owner** 구독자에서 구독 데이터베이스의 데이터베이스 역할 또는 **sysadmin** 구독자에서 서버 역할입니다.|  
|구독을 다시 초기화로 표시|밀어넣기 구독: **db_owner** 게시자에서 게시 데이터베이스의 데이터베이스 역할 또는 **sysadmin** 게시자에 대 한 서버 역할입니다.<br /><br /> 끌어오기 구독: **db_owner** 구독자에서 구독 데이터베이스의 데이터베이스 역할 또는 **sysadmin** 구독자에서 서버 역할입니다.|  
|복제 모니터를 사용하여 복제 작업, 오류 및 기록 보기. **sysadmin** 서버 역할의 멤버가 아닌 사용자는 에이전트 프로필, 일정 등을 수정할 수 없음|배포자의 배포 데이터베이스에 대한**replmonitor** 데이터베이스 역할 또는 배포자에 대한 **sysadmin** 서버 역할|  
|복제 에이전트 유지 관리|**db_owner** 적절 한 데이터베이스의 데이터베이스 역할 또는 **sysadmin** 해당 서버에서 서버 역할입니다.<br /><br /> 에이전트가 **sysadmin** 역할의 사용자에 의해 생성되고 에이전트에 대해 프록시 계정을 지정하지 않은 경우 에이전트는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 계정의 컨텍스트에서 실행됩니다. 이 경우 사용자에는 **db_owner** 역할 에이전트에 연결 된 작업을 수정할 수 없습니다.|  
|복제 에이전트 시작 또는 중지|에이전트 작업의 소유자 또는 해당 서버에 대한 **sysadmin** 서버 역할|  
  
## 참고 항목  
 [복제 보안을 위한 최선의 구현 방법](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [보안 및 보호 & #40입니다. 복제 및 #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  