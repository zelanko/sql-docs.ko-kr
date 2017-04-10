---
title: "저장 프로시저 실행을 트랜잭션 게시로 게시(SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "게시 [SQL Server 복제], 저장 프로시저 실행"
  - "저장 프로시저 [SQL Server 복제], 게시"
ms.assetid: 1d3a3525-0bc5-466f-b097-5359dc74432d
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 저장 프로시저 실행을 트랜잭션 게시로 게시(SQL Server Management Studio)
  저장된 프로시저 (해당 정의 아님)의 실행에 게시 되어야 합니다 지정는 **아티클 속성-\< 문서>** 대화 상자입니다. 이 대화 상자는 새 게시 마법사에서 사용할 수 있는 고 **게시 속성-\< 게시>** 대화 상자입니다. 마법사를 사용 하 고 대화 상자에 액세스 하는 방법에 대 한 자세한 내용은 참조 [게시를 만들](../../../relational-databases/replication/publish/create-a-publication.md) 및 [보기 및 게시 속성을 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)합니다.  
  
 프로시저 정의(CREATE PROCEDURE 문)는 구독이 초기화될 때 구독자로 복제되고 게시자에서 프로시저가 실행되면 복제가 구독자에서 해당하는 프로시저를 실행합니다.  
  
### 저장 프로시저의 실행을 게시하려면  
  
1.  에 **문서** 새 게시 마법사의 페이지 또는 **게시 속성-\< 게시>** 대화 상자에서 저장된 프로시저를 선택 합니다.  
  
2.  **아티클 속성**을 클릭한 다음 **선택한 저장 프로시저 아티클 속성 설정**을 클릭합니다.  
  
3.  에 **아티클 속성-\< 아티클>** 대화 상자에 다음 값 중 하나를 지정 합니다는 **복제** 옵션:  
  
    -   **저장 프로시저 실행**  
  
    -   **SP의 직렬화된 트랜잭션에서 실행**  
  
         이 옵션은 프로시저가 직렬화할 수 있는 트랜잭션의 컨텍스트 내에서 실행될 때만 프로시저 실행을 복제하기 때문에 권장됩니다. 저장 프로시저가 직렬화할 수 있는 트랜잭션 외부에서 실행되면 게시된 테이블의 데이터 변경 내용이 일련의 DML(데이터 조작 언어) 문으로 복제됩니다.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  있는 경우는 **게시 속성-\< 게시>** 대화 상자를 클릭 하 여 **확인** 저장 하 고 대화 상자를 닫습니다.  
  
## 참고 항목  
 [트랜잭션 복제에서 저장 프로시저 실행 게시](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)  
  
  