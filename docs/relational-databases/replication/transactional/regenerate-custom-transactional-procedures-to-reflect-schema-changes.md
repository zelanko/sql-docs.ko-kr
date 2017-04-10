---
title: "스키마 변경 내용을 반영하기 위해 사용자 지정 트랜잭션 프로시저 다시 생성 | Microsoft Docs"
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
  - "사용자 지정 프로시저 [SQL Server 복제]"
  - "트랜잭션 복제, 스키마 변경 내용 복제"
  - "스키마, [SQL Server 복제], 변경 내용 복제"
ms.assetid: ccf68a13-e748-4455-8168-90e6d2868098
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 스키마 변경 내용을 반영하기 위해 사용자 지정 트랜잭션 프로시저 다시 생성
  기본적으로 트랜잭션 복제는 게시의 각 테이블 아티클에 대해 내부 프로시저로 생성된 저장 프로시저를 통해 구독자에서 모든 데이터 변경 내용을 적용합니다. 3개의 프로시저(삽입, 업데이트 및 삭제에 대해 각각 하나씩)가 구독자에 복사되고 삽입, 업데이트 또는 삭제가 구독자에 복제되면 실행됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 게시자의 테이블에서 스키마를 변경하면 복제는 새 프로시저가 새 스키마와 일치하도록 동일한 내부 스크립팅 프로시저 집합을 호출하여 이러한 프로시저를 자동으로 다시 생성합니다. Oracle 게시자의 경우 스키마 변경 내용의 복제는 지원되지 않습니다.  
  
 또한 사용자 지정 프로시저를 지정하여 기본 프로시저 중 하나 이상을 바꿀 수 있습니다. 스키마 변경으로 인해 프로시저가 영향을 받는 경우에는 사용자 지정 프로시저를 변경해야 합니다. 예를 들어 프로시저가 스키마 변경에서 삭제된 열을 참조하는 경우 해당 열에 대한 참조를 프로시저에서 제거해야 합니다. 복제가 새 사용자 지정 프로시저를 구독자에 전파하는 방법에는 두 가지가 있습니다.  
  
-   첫 번째 옵션은 사용자 지정 스크립팅 프로시저를 사용하여 복제에서 사용하는 기본값을 바꾸는 것입니다.  
  
    1.  실행할 때 [sp_addarticle (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), 확인 된 **@schema_option** 0x02 비트를 **true**합니다.  
  
    2.  실행 [sp_register_custom_scripting (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md) 'insert', 'update' 또는 'delete' 매개 변수 값을 지정 하 고 **@type** 이름 사용자 지정 스크립팅 프로시저 매개 변수 및 **@value**합니다.  
  
     다음에 스키마를 변경하면 복제는 이 저장 프로시저를 호출하여 사용자가 새로 정의한 사용자 지정 저장 프로시저에 대한 정의를 스크립팅한 다음 프로시저를 각 구독자로 전파합니다.  
  
-   두 번째 옵션은 새 사용자 지정 프로시저 정의를 포함하는 스크립트를 사용하는 것입니다.  
  
    1.  실행할 때 [sp_addarticle (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), 로 설정 된 **@schema_option** 0x02 비트를 **false** 되므로 복제는 구독자에서 사용자 지정 프로시저를 자동으로 생성 하지 않습니다.  
  
    2.  각 스키마 변경 하기 전에 새 스크립트 파일을 만들고 스크립트를 실행 하 여 복제와 함께 등록 [sp_register_custom_scripting (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)합니다. 매개 변수에 대해 'custom_script' 값을 지정 **@type** 및 경로 매개 변수는 게시자에 스크립트를 **@value**합니다.  
  
     다음에 관련 스키마를 변경하면 이 스크립트는 동일한 트랜잭션 내 각 구독자에서 DDL 명령으로 실행됩니다. 스키마를 변경한 다음에는 스크립트 등록이 취소됩니다. 후속 스키마 변경 이후에 스크립트를 실행하려면 해당 스크립트를 다시 등록해야 합니다.  
  
## 참고 항목  
 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)   
 [게시 데이터베이스의 스키마 변경](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  