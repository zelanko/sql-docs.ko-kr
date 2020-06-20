---
title: DML 트리거 내에서 inserted 및 deleted 테이블에 대 한 DDL 작업 제거 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- data definition language [SQL Server]
- DDL statements [SQL Server]
- DML triggers, removing DDL operations
ms.assetid: e49ba7d5-787f-4052-b985-b699195d982b
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 61f7ab78b5ab6251b7f27401d36423ec27141c4e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85041844"
---
# <a name="remove-ddl-operations-on-the-inserted-and-deleted-tables-inside-dml-triggers"></a>DML 트리거 내부의 inserted 및 deleted 테이블에 대한 DDL 작업을 제거합니다.
  CREATE INDEX와 같은 DDL (데이터 정의 언어) 문은 DML 트리거 내부의 inserted 및 deleted 테이블에서 수행할 수 없습니다. 그러나 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 inserted 및 deleted 테이블에 대해 일부 DDL 문이 허용됩니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "inserted 및 deleted 테이블 사용"을 참조하십시오.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 DML 트리거 내에서 inserted 및 deleted 테이블에 대해 수행되는 DDL 작업을 제거합니다.  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 문제 데이터베이스 엔진](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
