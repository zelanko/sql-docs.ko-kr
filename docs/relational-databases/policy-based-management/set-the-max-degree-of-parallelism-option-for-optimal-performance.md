---
title: 최적 성능을 위해 최대 병렬 처리 수준 옵션 설정 | Microsoft 문서
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 00123da615c420fa3d58daae9a287ce3c13b8329
ms.sourcegitcommit: 2efb0fa21ff8093384c1df21f0e8910db15ef931
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68316669"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>최적 성능을 위해 최대 병렬 처리 수준 옵션 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 규칙은 8보다 큰 값에 대한 MAXDOP(max degree of parallelism) 옵션을 결정합니다. 이 옵션을 큰 값으로 설정하면 불필요하게 리소스가 소비되고 성능이 저하될 수 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 sp_configure를 사용하여 최대 병렬 처리 수준 옵션을 8 이하로 설정합니다.  
  
## <a name="for-more-information"></a>참조 항목  
 [SQL Server의 최대 병렬 처리 수준 구성 옵션에 대한 권장 사항 및 지침](https://go.microsoft.com/fwlink/?linkid=117786)  
  
 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
