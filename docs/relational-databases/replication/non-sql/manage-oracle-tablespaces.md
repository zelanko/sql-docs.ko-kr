---
title: "Oracle 테이블스페이스 관리 | Microsoft Docs"
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
  - "Oracle 게시 [SQL Server 복제], 테이블스페이스 관리"
  - "테이블스페이스 [SQL Server 복제]"
ms.assetid: b8ea6c3b-01d6-4efc-bbfb-03b264530bbd
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Oracle 테이블스페이스 관리
  테이블스페이스는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 파일 그룹과 개념이 거의 동일한 데이터베이스 저장소 단위입니다. 테이블스페이스를 사용하면 개별 그룹 내에서 데이터베이스 개체를 저장하고 관리할 수 있습니다. 자세한 내용은 Oracle 설명서를 참조하십시오.  
  
 테이블을 Oracle 게시의 일부로 구성하는 경우 복제 로깅 정보를 저장할 때 기존 Oracle 테이블스페이스를 사용하도록 선택적으로 지정할 수 있습니다. 지정하지 않으면 복제 개체에 대한 테이블스페이스가 게시자를 구성할 때 구성된 복제 관리 사용자 스키마와 연결된 기본 테이블스페이스가 됩니다.  
  
 **아티클 로깅 테이블에 대해 테이블스페이스를 지정하려면**   
  
-   **아티클 속성** 대화 상자에서 테이블스페이스를 지정합니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
-   사용 하 여 [sp_changearticle (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)합니다. 사용 하 여 **sp_changearticle**, 다음을 지정 합니다.  
  
    -   **@publisher**매개 변수에 대한 Oracle 게시자의 이름  
  
    -   **@publication**매개 변수에 대한 Oracle 게시의 이름  
  
    -   **@article**매개 변수에 대한 아티클의 이름  
  
    -   **@property**매개 변수에 대한 '테이블스페이스' 값  
  
    -   **@value**매개 변수에 대한 테이블스페이스의 이름  
  
## 참고 항목  
 [Oracle 게시자 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle 게시자에 생성되는 개체](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)  
  
  