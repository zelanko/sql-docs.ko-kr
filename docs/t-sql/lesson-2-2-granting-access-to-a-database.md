---
title: 데이터베이스에 대한 액세스 권한 부여 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: t-sql
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
helpviewer_keywords:
- database access
ms.assetid: 686edfe2-3650-48a6-a2da-9d46fa211ad8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 75d4f048573ce60b0be6704196b376c8136aa213
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424092"
---
# <a name="lesson-2-2---granting-access-to-a-database"></a>2-2단원 - 데이터베이스에 대한 액세스 권한 부여
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
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
  
  
  
