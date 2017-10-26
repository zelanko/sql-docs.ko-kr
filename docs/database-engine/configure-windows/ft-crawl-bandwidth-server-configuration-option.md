---
title: "ft crawl bandwidth 서버 구성 옵션 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- large memory buffers
- memory [SQL Server], buffers
- ft crawl bandwidth option
ms.assetid: e5864ad9-92f5-43b5-95de-46d68ded8694
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e582c59680c19f052ae10130d3673568b5eb60d6
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="ft-crawl-bandwidth-server-configuration-option"></a>ft crawl bandwidth 서버 구성 옵션
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **ft crawl bandwidth** 옵션을 사용하여 대용량 메모리 버퍼 풀이 증가할 수 있는 크기를 지정할 수 있습니다. 대용량 메모리 버퍼의 크기는 4MB입니다. **max** 매개 변수 값은 전체 텍스트 메모리 관리자가 대용량 버퍼 풀에서 유지 관리해야 하는 버퍼의 최대 수를 지정합니다. **max** 값이 0이면 대용량 버퍼 풀에 가능한 버퍼 수에 제한이 없어집니다.  
  
 **min** 매개 변수 값은 대용량 메모리 버퍼에서 유지 관리해야 하는 메모리 버퍼의 최소 수를 지정합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 관리자의 요청이 있을 경우 모든 여분의 버퍼 풀이 해제되지만 이 최소 버퍼 수는 유지됩니다. 하지만 지정된 **min** 값이 0일 경우 모든 메모리 버퍼가 해제됩니다.  
  
 특정 환경에서는 현재 할당된 버퍼 수가 **min** 매개 변수에 지정된 값보다 작을 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ft notify bandwidth 서버 구성 옵션](../../database-engine/configure-windows/ft-notify-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

