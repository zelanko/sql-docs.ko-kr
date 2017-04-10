---
title: "MSSQL_ENG018456 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG018456 오류"
ms.assetid: 3daa8144-d81f-445a-b6c3-4bb3e9fd1526
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_ENG018456
    
## 메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|18456|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|사용자가 로그인 하지 못했습니다 ' %. * ls'.%.\*ls|  
  
## 설명  
 로그인 시도가 실패할 때마다 MSSQL_ENG018456 오류가 발생합니다. 오류 메시지는 계정을 포함 하는 경우 **distributor_admin** (로그인 하지 못했습니다 메시지가 나타납니다.), 복제에 사용 된 계정에 문제가 있습니다. 복제는 원격 서버에 만듭니다 **repl_distributor**, 배포자 및 게시자 간 통신을 허용 합니다. 로그인 **distributor_admin** 이 원격 서버에 연결 되며 유효한 암호가 있어야 합니다.  
  
## 사용자 동작  
 이 계정의 암호를 지정했는지 확인하십시오. 자세한 내용은 참조 [배포자 보안 설정](../../relational-databases/replication/security/secure-the-distributor.md)합니다.  
  
## 참고 항목  
 [오류 및 이벤트 참조 & #40입니다. 복제 및 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  