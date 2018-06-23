---
title: 최적 성능을 위해 최대 병렬 처리 수준 옵션 설정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3fc4f4c3da6505d3c9464144a37eb98682969d9d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36173108"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>최적 성능을 위해 최대 병렬 처리 수준 옵션 설정
  이 규칙은 8보다 큰 값에 대한 MAXDOP(max degree of parallelism) 옵션을 결정합니다. 이 옵션을 큰 값으로 설정하면 불필요하게 리소스가 소비되고 성능이 저하될 수 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 sp_configure를 사용하여 최대 병렬 처리 수준 옵션을 8 이하로 설정합니다.  
  
## <a name="for-more-information"></a>참조 항목  
 [Microsoft 기술 자료 문서 329204](http://go.microsoft.com/fwlink/?linkid=117786)  
  
 [max degree of parallelism 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
