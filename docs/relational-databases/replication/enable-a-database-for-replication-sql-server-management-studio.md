---
title: "데이터베이스 복제 설정(SQL Server Management Studio) | Microsoft Docs"
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
  - "데이터베이스 [SQL Server 복제]"
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# 데이터베이스 복제 설정(SQL Server Management Studio)
  **sysadmin** 고정 서버 역할의 멤버가 새 게시 마법사로 게시를 만들면 데이터베이스가 복제를 사용할 수 있도록 암시적으로 설정됩니다. 멤버는 **sysadmin** 고정된 서버 역할 데이터베이스 복제에 대해 명시적으로 사용할 수도 있도록의 멤버는 **db_owner** 고정된 데이터베이스 역할 해당 데이터베이스에 하나 이상의 게시를 만들 수 있습니다. 데이터베이스를 명시적으로 사용 하려면 사용 된 **게시 데이터베이스** 의 페이지는 **게시자 속성-\< 게시자>** 대화 상자입니다. 이 대화 상자에 액세스하는 방법은 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)을 참조하십시오.  
  
### 데이터베이스 복제를 설정하려면  
  
1.  에 **게시 데이터베이스** 의 페이지는 **게시자 속성-\< 게시자>** 대화 상자는 **트랜잭션** 및/또는 **병합** 복제할 각 데이터베이스에 대 한 확인란입니다. 데이터베이스에서 스냅숏 복제를 설정하려면 **트랜잭션** 을 선택합니다.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  