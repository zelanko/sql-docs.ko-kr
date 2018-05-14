---
title: 데이터 컬렉션 매개 변수 구성(Transact-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data collection [SQL Server]
ms.assetid: 850905b6-35d2-4ed1-ab51-de64daa832b2
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 25acc3d0b5f9c29476e0041e38fc62f04d646b27
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="configure-data-collection-parameters-transact-sql"></a>데이터 컬렉션 매개 변수 구성(Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  사용자 지정 컬렉션 집합을 만들기 전에 먼저 데이터 컬렉션 매개 변수를 구성해야 합니다. 데이터 수집기에서 제공하는 저장 프로시저를 사용하여 이를 구성할 수 있습니다. 이 태스크를 수행하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 쿼리 편집기를 사용하여 다음 절차를 수행해야 합니다.  
  
> [!NOTE]  
>  데이터 컬렉션 매개 변수는 한 번만 구성합니다. 구성 후 이러한 매개 변수는 생성된 추가 컬렉션 집합에 사용됩니다.  
  
### <a name="configure-data-collection-parameters"></a>데이터 컬렉션 매개 변수 구성  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 사용자 지정 컬렉션 집합을 만들 데이터베이스에 연결합니다.  
  
2.  쿼리 편집기에서 다음 문을 실행합니다.  
  
    ```sql  
    USE msdb;  
    EXEC sp_syscollector_set_warehouse_instance_name N'INSTANCE_NAME';-- where instance name is the name of the SQL Server instance  
    EXEC sp_syscollector_set_warehouse_database_name N'MDW';  
    EXEC sp_syscollector_set_cache_directory N'D:\tempdata';  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)   
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
