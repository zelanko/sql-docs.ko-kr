---
title: MSSQLSERVER_3961 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3961 (Database Engine error)
ms.assetid: 3bbc6965-6445-400c-940a-2d85b037513f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f12e70423905a78eddecb93a8b4623c96a6f0322
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62914085"
---
# <a name="mssqlserver_3961"></a>MSSQLSERVER_3961
    
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|3961|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|XACT_METADATA_INVALID|  
|메시지 텍스트|"문에서 액세스한 개체가 이 트랜잭션이 시작된 후 다른 동시 트랜잭션의 DDL 문에 의해 수정되어 데이터베이스 '%.*ls'에서 스냅샷 격리 트랜잭션이 실패했습니다.  메타데이터 버전이 관리되지 않기 때문에 허용되지 않습니다. 메타데이터에 대한 동시 업데이트로 인해 스냅샷 격리와 혼합된 경우 불일치가 발생할 수 있습니다.|  
  
## <a name="explanation"></a>설명  
 이 오류는 스냅샷 격리에서 메타데이터를 쿼리하는 경우 스냅샷 격리 하에 액세스되는 메타데이터를 업데이트하는 동시 DDL 문이 있으면 발생할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 메타데이터의 버전 관리를 지원하지 않습니다. 따라서, 스냅샷 격리 하에 실행되는 명시적 트랜잭션 내에서 수행할 수 있는 DDL 작업에 대한 제한 사항이 있습니다. 암시적 트랜잭션은, 정의상, DDL 문과 함께 스냅샷 격리의 의미 체계를 적용할 수 있는 단일 명령문입니다. ALTER TABLE, CREATE INDEX, CREATE XML INDEX, ALTER INDEX, DROP INDEX, DBCC REINDEX, ALTER PARTITION FUNCTION, ALTER PARTITION SCHEME 또는 CLR(공용 언어 런타임) DDL 문과 같은 DDL 문은 BEGIN TRANSACTION 문 다음에 스냅샷 격리에서 허용되지 않습니다. 다음 명령문은 암시적 트랜잭션 내에서 스냅샷 격리를 사용하는 경우 허용됩니다. 암시적 트랜잭션은, 정의상, DDL 문과 함께 스냅샷 격리의 의미 체계를 적용할 수 있는 단일 명령문입니다.  
  
## <a name="user-action"></a>사용자 동작  
 메타데이터를 쿼리하기 전에 스냅샷 격리 수준을 커밋된 읽기와 같은 비스냅샷 격리 수준으로 변경합니다.  
  
  
