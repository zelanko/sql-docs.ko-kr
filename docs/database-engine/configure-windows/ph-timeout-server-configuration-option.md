---
title: PH timeout 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- time limit for protocol handler wait [SQL Server]
- timeout options [SQL Server], ph timeout option
- protocols [SQL Server], timing out
- ph timeout option
ms.assetid: ed19a07c-83fe-4582-9c9e-41b1ce571850
caps.latest.revision: 28
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9e99b38210816277160ab4f0991318dc7f3f266a
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="ph-timeout-server-configuration-option"></a>PH timeout 서버 구성 옵션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  PH timeout 옵션을 사용하여 전체 텍스트 프로토콜 처리기가 제한 시간까지 데이터베이스에 대한 연결을 대기하는 시간(초)을 지정할 수 있습니다. 기본값은 60초입니다. 일시적인 네트워크 문제로 인해 연결 시간을 초과하는 경우 ph timeout 값을 늘리십시오.  
  
 전체 텍스트 프로토콜 처리기는 필터 데몬 호스트에 호스팅되며 SQL Server에서 전체 텍스트 인덱싱할 데이터를 인출하는 데 사용됩니다. 전체 텍스트 검색 구성 요소에 대한 자세한 내용은 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)을 참조하세요.  
  
 데이터 행을 인출할 때 프로토콜 처리기에서 지정한 시간 내에 SQL Server에 연결할 수 없으면 해당 행에 대한 제한 시간 오류를 보고합니다. 전체 텍스트 Gatherer는 나중에 행을 다시 시도합니다. 전체 텍스트 Gatherer에 대한 자세한 내용은 [전체 텍스트 인덱스 채우기](../../relational-databases/search/populate-full-text-indexes.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
