---
title: "원격 데이터 보관 서버 구성 옵션 구성 | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b5817b5a-f39a-4faf-b11e-a47b54fd9f32
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# 원격 데이터 보관 서버 구성 옵션 구성
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **remote data archive** 옵션을 사용하여 서버의 데이터베이스 및 테이블을 Stretch에 사용할 수 있는지 여부를 지정합니다. 자세한 내용은 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)를 참조하십시오.  
  
 **remote data archive** 옵션에는 다음과 같은 값이 올 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|0|서버의 데이터베이스 및 테이블을 Stretch에 사용할 수 없습니다.|  
|1|서버의 데이터베이스 및 테이블을 Stretch에 사용할 수 있습니다.|  
  
 **remote data archive** 옵션의 값을 설정하도록 **sp_configure**를 실행하려면 sysadmin 또는 serveradmin 권한이 필요합니다.  
  
## 예제  
 다음 예제에서는 먼저 **remote data archive** 옵션의 현재 설정을 표시합니다. 그런 다음 예에서는 값을 1로 설정하여 **remote data archive** 옵션을 활성화합니다.  
  
```  
EXEC sp_configure 'remote data archive';  
GO  
EXEC sp_configure 'remote data archive' , '1';  
GO  
RECONFIGURE;  
GO  
```  
  
 옵션을 해제하려면 값을 0으로 설정합니다.  
  
## 참고 항목  
 [데이터베이스에서 스트레치 데이터베이스 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [스트레치 데이터베이스](../../sql-server/stretch-database/stretch-database.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  