---
title: "ft notify bandwidth 서버 구성 옵션 | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "ft notify bandwidth 옵션"
  - "작은 메모리 버퍼"
  - "메모리 [SQL Server], 버퍼"
ms.assetid: 9ca284c5-f3e0-4a67-a132-fff376ff0ffe
caps.latest.revision: 19
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 19
---
# ft notify bandwidth 서버 구성 옵션
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **ft notify bandwidth** 옵션을 사용하여 작은 메모리 버퍼의 풀이 증가할 수 있는 최대 크기를 지정할 수 있습니다. 작은 메모리 버퍼의 크기는 64KB입니다. 매개 변수 값은 전체 텍스트 메모리 관리자가 작은 버퍼 풀에서 유지해야 하는 *최대* 버퍼 수를 지정합니다. **max** 값이 0인 경우 작은 버퍼 풀의 버퍼 수에 대한 상한값이 없습니다.  
  
 **min** 매개 변수는 작은 메모리 버퍼의 풀에서 유지되어야 하는 최소 메모리 버퍼 수를 지정합니다.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 관리자의 요청이 있을 경우 모든 여분의 버퍼 풀이 해제되지만 이 최소 버퍼 수는 유지됩니다. 하지만 지정된 **min** 값이 0일 경우 모든 메모리 버퍼가 해제됩니다.  
  
 경우에 따라 현재 할당된 버퍼 수가 **min** 매개 변수에 지정된 값보다 낮을 수도 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## 참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [ft crawl bandwidth 서버 구성 옵션](../../database-engine/configure-windows/ft-crawl-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  