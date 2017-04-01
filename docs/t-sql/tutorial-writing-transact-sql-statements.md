---
title: "자습서: Transact-SQL 문 작성 | Microsoft Docs"
ms.custom: ""
ms.date: "08/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "Transact-SQL 문, 자습서"
  - "Transact-SQL 자습서"
  - "자습서 [Transact-SQL]"
ms.assetid: 2addc9be-67d0-423d-a457-192fe9d7d058
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# 자습서: Transact-SQL 문 작성
[!INCLUDE[tsql](../includes/tsql-md.md)] 문 작성 자습서를 시작합니다. 이 자습서는 SQL 문을 처음 작성하는 사용자를 위해 제공됩니다. 이 자습서는 새로운 사용자가 테이블을 만들고 데이터를 삽입하는 몇 가지 기본 문을 통해 작업을 시작하는 데 도움이 될 것입니다. 이 자습서에서는 [!INCLUDE[tsql](../includes/tsql-md.md)]가 구현하는 SQL 표준인 [!INCLUDE[msCoName](../includes/msconame-md.md)]을 사용합니다. 이 자습서는 [!INCLUDE[tsql](../includes/tsql-md.md)] 클래스를 대체하는 것이 아니라 [!INCLUDE[tsql](../includes/tsql-md.md)] 언어를 간략하게 소개하는 데 목적이 있습니다. 의도적으로 간단한 문을 이 자습서에서 사용하고 있으므로 일반적인 프로덕션 데이터베이스에서 볼 수 있는 복잡한 문은 다루지 않습니다.  
  
>**참고:** 초보자라면 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 작성하는 대신 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 사용하는 것이 더 쉬울 수 있습니다.  
  
## 추가 정보 찾기  
특정 문에 대한 자세한 내용을 보려면 SQL Server 온라인 설명서에 이름으로 해당 문을 검색하거나 목차를 사용하여 [Transact-SQL 참조&#40;데이터베이스 엔진&#41;](../t-sql/transact-sql-reference-database-engine.md) 아래에 사전순으로 나열된 1,800개의 언어 요소를 찾아봅니다. 또한 관심이 있는 주제와 관련된 키워드를 검색하는 것도 좋은 방법이 될 수 있습니다. 예를 들어 월과 같은 날짜의 일부를 반환하는 방법을 보려면 **dates [SQL Server]**의 색인을 검색한 다음 **dateparts**를 선택합니다. 이렇게 하면 [DATEPART&#40;Transact-SQL&#41;](../t-sql/functions/datepart-transact-sql.md) 항목이 제공됩니다. 마찬가지로 문자열을 사용하는 방법을 보려면 **문자열 함수**를 검색합니다. 이렇게 하면 [문자열 함수&#40;Transact-SQL&#41;](../t-sql/functions/string-functions-transact-sql.md) 항목이 제공됩니다.  
  
## 학습 내용  
이 자습서에서는 데이터베이스 작성, 데이터베이스에서 테이블 작성, 테이블에 데이터 삽입, 데이터 업데이트, 데이터 읽기, 데이터 삭제, 테이블 삭제 등을 수행하는 방법을 보여 줍니다. 뷰와 저장 프로시저를 만들고 데이터베이스 및 데이터에 대해 사용자를 구성합니다.  
  
이 자습서는 다음 3개의 단원으로 이루어져 있습니다.  
  
[1단원: 데이터베이스 개체 만들기](../t-sql/lesson-1-creating-database-objects.md)  
이 단원에서는 데이터베이스 작성, 데이터베이스에서 테이블 작성, 테이블에 데이터 삽입, 데이터 업데이트, 데이터 읽기 등을 수행합니다.  
  
[2단원: 데이터베이스 개체에 대한 사용 권한 구성](../t-sql/lesson-2-configuring-permissions-on-database-objects.md)  
이 단원에서는 로그인 및 사용자를 만듭니다. 또한 뷰와 저장 프로시저를 만든 다음 저장 프로시저에 대한 사용 권한을 사용자에게 부여합니다.  
  
[3단원: 데이터베이스 개체 삭제](../t-sql/lesson-3-deleting-database-objects.md)  
이 단원에서는 데이터 액세스 권한 제거, 테이블에서 데이터 삭제, 테이블 삭제, 데이터베이스 삭제 등을 수행합니다.  
  
## 요구 사항  
이 자습서를 완료하려면 SQL 언어를 알 필요가 없지만 테이블과 같은 기본 데이터베이스 개념을 이해해야 합니다. 이 자습서를 진행하는 동안 데이터베이스를 만들고 Windows 사용자를 만듭니다. 이러한 태스크를 수행하려면 높은 수준의 사용 권한이 필요하므로 컴퓨터에 관리자로 로그인해야 합니다.  
  
시스템에는 다음이 설치되어 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)](버전은 관계 없음)  
  
-  [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)  
  

 
  
  
  
