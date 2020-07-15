---
title: ft crawl bandwidth 서버 구성 옵션 | Microsoft Docs
description: "\"ft crawl bandwidth 옵션\"에 대해 알아봅니다. 이 옵션이 대량 메모리 버퍼의 풀에서 SQL Server가 유지 관리하는 버퍼 수에 어떻게 영향을 주는지 확인합니다."
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- large memory buffers
- memory [SQL Server], buffers
- ft crawl bandwidth option
ms.assetid: e5864ad9-92f5-43b5-95de-46d68ded8694
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 59caa1e868c4caab24afd17909c34f57c96f0005
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789794"
---
# <a name="ft-crawl-bandwidth-server-configuration-option"></a>ft crawl bandwidth 서버 구성 옵션
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **ft crawl bandwidth** 옵션을 사용하여 대용량 메모리 버퍼 풀이 증가할 수 있는 크기를 지정할 수 있습니다. 대용량 메모리 버퍼의 크기는 4MB입니다. **max** 매개 변수 값은 전체 텍스트 메모리 관리자가 대용량 버퍼 풀에서 유지 관리해야 하는 버퍼의 최대 수를 지정합니다. **max** 값이 0이면 대용량 버퍼 풀에 가능한 버퍼 수에 제한이 없어집니다.  
  
 **min** 매개 변수 값은 대용량 메모리 버퍼에서 유지 관리해야 하는 메모리 버퍼의 최소 수를 지정합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 관리자의 요청이 있으면 모든 여분의 버퍼 풀이 해제되지만, 이 최소 버퍼 수는 유지됩니다. 하지만 지정된 **min** 값이 0일 경우 모든 메모리 버퍼가 해제됩니다.  
  
 특정 환경에서는 현재 할당된 버퍼 수가 **min** 매개 변수에 지정된 값보다 작을 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ft notify bandwidth 서버 구성 옵션](../../database-engine/configure-windows/ft-notify-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
