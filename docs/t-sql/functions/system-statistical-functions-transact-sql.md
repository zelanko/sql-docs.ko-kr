---
description: 시스템 통계 함수(Transact-SQL)
title: 시스템 통계 함수(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- statistical functions [SQL Server]
- system statistical functions [SQL Server]
- functions [SQL Server], statistical
ms.assetid: 45828c67-1b9a-4653-bb24-86246084d8ba
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 7368e6bdb14dfdabfe44b79ef68d764dceb40149
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459565"
---
# <a name="system-statistical-functions-transact-sql"></a>시스템 통계 함수(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  다음 스칼라 함수는 시스템에 대한 통계 정보를 반환합니다.  

:::row:::
    :::column:::
        [@@CONNECTIONS](../../t-sql/functions/connections-transact-sql.md)
    :::column-end:::
    :::column:::
        [@@PACK_RECEIVED](../../t-sql/functions/pack-received-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [@@CPU_BUSY](../../t-sql/functions/cpu-busy-transact-sql.md)
    :::column-end:::
    :::column:::
        [@@PACK_SENT](../../t-sql/functions/pack-sent-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [fn_virtualfilestats](../../relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql.md)
    :::column-end:::
    :::column:::
        [@@TIMETICKS](../../t-sql/functions/timeticks-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [@@IDLE](../../t-sql/functions/idle-transact-sql.md)
    :::column-end:::
    :::column:::
        [@@TOTAL_ERRORS](../../t-sql/functions/total-errors-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [@@IO_BUSY](../../t-sql/functions/io-busy-transact-sql.md)
    :::column-end:::
    :::column:::
        [@@TOTAL_READ](../../t-sql/functions/total-read-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [@@PACKET_ERRORS](../../t-sql/functions/packet-errors-transact-sql.md)
    :::column-end:::
    :::column:::
        [@@TOTAL_WRITE](../../t-sql/functions/total-write-transact-sql.md)
    :::column-end:::
:::row-end:::
  
  
 모든 시스템 통계 함수는 비 결정적입니다. 이는 이러한 함수를 호출할 때마다 동일한 입력 값 집합을 사용하더라도 항상 동일한 결과가 반환되지는 않는다는 것을 의미합니다. 함수 결정성에 대한 자세한 내용은 [결정적 함수 및 비결정적 함수](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  
