---
title: "데이터베이스에 대 한 액세스를 부여 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- database access
ms.assetid: 686edfe2-3650-48a6-a2da-9d46fa211ad8
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 30de5de3d238905802e80d433c2df7deaf058929
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-2-2---granting-access-to-a-database"></a>2-2-데이터베이스에 대 한 액세스 부여 단원
현재 Mary는 이 인스턴스의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 액세스할 수 있지만 데이터베이스에 액세스할 수 있는 권한은 없습니다. Mary에게 데이터베이스 사용자의 권한을 부여할 때까지 Mary는 자신의 기본 데이터베이스인 **TestData** 에도 액세스할 수 없습니다.  
  
Mary에게 액세스 권한을 부여하려면 **TestData** 데이터베이스로 전환한 다음 CREATE USER 문을 사용하여 Mary의 로그인을 Mary라는 사용자에게 매핑합니다.  
  
### <a name="to-create-a-user-in-a-database"></a>데이터베이스에서 사용자를 만들려면  
  
1.  다음 문을 입력하고 실행하여( `computer_name` 을 컴퓨터의 이름으로 바꿈) `Mary` 데이터베이스에 대한 액세스 권한을 `TestData` 에게 부여합니다.  
  
    ```  
    USE [TestData];  
    GO  
  
    CREATE USER [Mary] FOR LOGIN [computer_name\Mary];  
    GO  
  
    ```  
  
    이제 Mary는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 `TestData` 데이터베이스에 대한 액세스 권한을 가집니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[뷰 및 저장 프로시저 만들기](../t-sql/lesson-2-3-creating-views-and-stored-procedures.md)  
  
  
  

