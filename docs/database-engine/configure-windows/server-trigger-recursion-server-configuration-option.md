---
title: server trigger recursion 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
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
ms.openlocfilehash: dcd67a89ea5605647d6736d9d28a6e070a483c16
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68027618"
---
# <a name="server-trigger-recursion-server-configuration-option"></a>server trigger recursion 서버 구성 옵션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **server trigger recursion** 옵션을 사용하여 서버 수준 트리거가 재귀적으로 발생할 수 있는지 여부를 지정할 수 있습니다. 이 옵션을 1(ON)로 설정하면 서버 수준 트리거가 재귀적으로 발생할 수 있으며 0(OFF)으로 설정하면 재귀적으로 발생할 수 없습니다. server trigger recursion 옵션이 0(OFF)일 때는 직접 재귀만 차단되며 간접 재귀를 막으려면 **nested triggers** 옵션을 0으로 설정해야 합니다. 이 옵션의 기본값은 1(ON)이며 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
 자세한 내용은 [중첩 트리거 만들기](../../relational-databases/triggers/create-nested-triggers.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
