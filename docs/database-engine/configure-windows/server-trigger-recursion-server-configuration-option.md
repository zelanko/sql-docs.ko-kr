---
title: server trigger recursion 서버 구성 옵션 | Microsoft Docs
description: "\"server trigger recursion\" 옵션이 SQL Server 서버 수준 트리거에서의 재귀에 어떻게 영향을 주는지 알아봅니다. 직접 및 간접 재귀를 설정 또는 해제하는 방법을 확인합니다."
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7dc2dcd132ef32ba4f026a1a9b76d4e67df28b26
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715561"
---
# <a name="server-trigger-recursion-server-configuration-option"></a>server trigger recursion 서버 구성 옵션
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **server trigger recursion** 옵션을 사용하여 서버 수준 트리거가 재귀적으로 발생할 수 있는지 여부를 지정할 수 있습니다. 이 옵션을 1(ON)로 설정하면 서버 수준 트리거가 재귀적으로 발생할 수 있으며 0(OFF)으로 설정하면 재귀적으로 발생할 수 없습니다. server trigger recursion 옵션이 0(OFF)일 때는 직접 재귀만 차단되며 간접 재귀를 막으려면 **nested triggers** 옵션을 0으로 설정해야 합니다. 이 옵션의 기본값은 1(ON)이며 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
 자세한 내용은 [중첩 트리거 만들기](../../relational-databases/triggers/create-nested-triggers.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
