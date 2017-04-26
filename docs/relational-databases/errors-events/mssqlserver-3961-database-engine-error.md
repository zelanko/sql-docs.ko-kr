---
title: "MSSQLSERVER_3961 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3961 (Database Engine error)
ms.assetid: 3bbc6965-6445-400c-940a-2d85b037513f
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4bee6f2a3420267cca465ef81adb25436f105166
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver3961"></a>MSSQLSERVER_3961
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|3961|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|XACT_METADATA_INVALID|  
|메시지 텍스트|"문에서 액세스한 개체가 이 트랜잭션이 시작된 후 다른 동시 트랜잭션의 DDL 문에 의해 수정되어 데이터베이스 '%.*ls'에서 스냅숏 격리 트랜잭션이 실패했습니다.  메타데이터에 버전이 지정되지 않았으므로 이 트랜잭션은 허용되지 않습니다. 스냅숏 격리를 함께 사용하여 메타데이터에 대해 동시 업데이트를 수행하면 일관되지 않은 결과가 발생할 수 있습니다."|  
  
## <a name="explanation"></a>설명  
스냅숏 격리에서 메타데이터를 쿼리 중이고 스냅숏 격리에서 액세스하는 메타데이터를 업데이트하는 동시 DDL 문이 있을 경우 이 오류가 발생할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 메타데이터의 버전 관리를 지원하지 않습니다. 따라서 스냅숏 격리에서 실행하는 명시적 트랜잭션에서 수행할 수 있는 DDL 작업에 대한 제한 사항이 있습니다. 기본적으로 암시적 트랜잭션은 DDL 문에서도 스냅숏 격리의 의미 체계를 적용할 수 있게 하는 단일 문입니다. ALTER TABLE, CREATE INDEX, CREATE XML INDEX, ALTER INDEX, DROP INDEX, DBCC REINDEX, ALTER PARTITION FUNCTION, ALTER PARTITION SCHEME 또는 CLR(공용 언어 런타임) DDL 문과 같은 DDL 문은 BEGIN TRANSACTION 문 다음에 스냅숏 격리에서 허용되지 않습니다. 이러한 문은 암시적 트랜잭션 내에서 스냅숏 격리를 사용할 때 허용됩니다. 기본적으로 암시적 트랜잭션은 DDL 문에서도 스냅숏 격리의 의미 체계를 적용할 수 있게 하는 단일 문입니다.  
  
## <a name="user-action"></a>사용자 동작  
메타데이터를 쿼리하기 전에 스냅숏 격리 수준을 커밋된 읽기와 같은 비스냅숏 격리 수준으로 변경합니다.  
  

