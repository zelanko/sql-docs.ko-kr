---
title: server trigger recursion 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- recursive triggers [SQL Server]
- triggers [SQL Server], recursive
- server trigger recursion option
ms.assetid: da4c25f5-d04c-4951-a3db-409e71a1b468
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f1fc67db5d7d62c9257f6d66359b0166b6ed8c0b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62808884"
---
# <a name="server-trigger-recursion-server-configuration-option"></a>server trigger recursion 서버 구성 옵션
  **server trigger recursion** 옵션을 사용하여 서버 수준 트리거가 재귀적으로 발생할 수 있는지 여부를 지정할 수 있습니다. 이 옵션을 1(ON)로 설정하면 서버 수준 트리거가 재귀적으로 발생할 수 있으며 0(OFF)으로 설정하면 재귀적으로 발생할 수 없습니다. server trigger recursion 옵션이 0(OFF)일 때는 직접 재귀만 차단되며 간접 재귀를 막으려면 **nested triggers** 옵션을 0으로 설정해야 합니다. 이 옵션의 기본값은 1(ON)이며 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
 자세한 내용은 [중첩 트리거 만들기](../../relational-databases/triggers/create-nested-triggers.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
