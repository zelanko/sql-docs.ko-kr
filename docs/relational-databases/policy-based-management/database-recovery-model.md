---
title: 데이터베이스 복구 모델
description: 사용자 데이터베이스의 데이터 손실을 줄이기 위해 정책을 사용하도록 설정하여 백업 복구 모델을 검사하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 08/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 048fa8d28e32ad73aa9e2a85e217f268fa865a3c
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89285254"
---
# <a name="database-recovery-model"></a>데이터베이스 복구 모델
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  SQL Server Enterprise 및 Standard 버전의 경우 이 규칙은 읽기 전용이 아닌 사용자 데이터베이스의 복구가 단순 복구로 설정되어 있는지 검사합니다. 프로덕션 데이터베이스의 경우 단순 복구 모델보다 전체 복구 모델을 사용하는 것이 좋습니다. 전체 복구 모델은 지정 시간 복구를 지원합니다. 이 기능은 재해 복구를 수행할 때 데이터 손실을 줄이는 데 도움을 줍니다.
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 프로덕션 데이터베이스는 전체 복구 모드로 설정해야 하며, 데이터 손실을 최소화할 수 있도록 트랜잭션 로그를 자주 백업해야 합니다.
  
## <a name="see-also"></a>참고 항목 
  
 [복원 및 복구 개요](../backup-restore/restore-and-recovery-overview-sql-server.md)   
  
 [전체 데이터베이스 복원(전체 복구 모델)](../backup-restore/complete-database-restores-full-recovery-model.md)  

 [트랜잭션 로그 백업](../backup-restore/transaction-log-backups-sql-server.md)   
  
