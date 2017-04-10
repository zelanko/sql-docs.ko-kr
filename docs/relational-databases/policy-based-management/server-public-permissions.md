---
title: "서버 public 사용 권한 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "최선의 방법 [데이터베이스 엔진]"
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# 서버 public 사용 권한
  이 규칙은 public 서버 역할에 서버 사용 권한이 있는지 확인합니다. 서버에 만들어진 모든 로그인은 public 서버 역할의 멤버입니다. 이 조건이 충족될 경우 서버의 모든 로그인은 서버 사용 권한을 갖습니다.  
  
## 최선의 구현 방법 권장 사항  
 서버 public 역할에 서버 사용 권한을 부여하지 마십시오.  
  
> [!IMPORTANT]  
>  설치가 완료되면 **PUBLIC** 역할은 모든 끝점에 대한 **CONNECT** 권한( **관리자 전용 연결**제외)을 갖습니다. 이것은 정상이며 일반적으로 변경할 수 없습니다. 새 로그인을 만들 때 자동으로 부여되는 **CONNECT SQL** 권한으로 액세스가 제어됩니다.  
  
### 참조 항목  
 [SQL Server 보안 설정](../../relational-databases/security/securing-sql-server.md)  
  
  