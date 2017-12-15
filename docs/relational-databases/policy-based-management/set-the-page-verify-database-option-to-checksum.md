---
title: "PAGE_VERIFY 데이터베이스 옵션을 CHECKSUM으로 설정 | Microsoft 문서"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: 686b9a4a-ea61-4263-9ab8-f444a3077679
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 48d446e02745228731ba700b3de5ce2a4e7f738a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="set-the-pageverify-database-option-to-checksum"></a>PAGE_VERIFY 데이터베이스 옵션을 CHECKSUM으로 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 규칙은 PAGE_VERIFY 데이터베이스 옵션이 CHECKSUM으로 설정되었는지 검사합니다. PAGE_VERIFY 데이터베이스 옵션에 CHECKSUM을 설정하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에서 페이지를 디스크에 쓸 때 전체 페이지 내용에 대한 체크섬이 계산되어 페이지 헤더에 값이 저장됩니다. 디스크에서 페이지를 읽으면 체크섬이 다시 계산되어 페이지 헤더에 저장된 체크섬 값과 비교됩니다. 이를 통해 높은 수준의 데이터 파일 무결성을 제공할 수 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 PAGE_VERIFY 데이터베이스 옵션을 CHECKSUM으로 설정합니다.  
  
## <a name="for-more-information"></a>참조 항목  
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
  
