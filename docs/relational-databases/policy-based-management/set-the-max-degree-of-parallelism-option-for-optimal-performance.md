---
title: 최대 병렬 처리 수준 및 정책 기반 관리
description: SQL Server 정책 기반 관리의 최대 병렬 처리 수준 값을 확인하는 정책을 구성하는 방법을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6aada496465c642570f9b60a0b1659bbe9ee3db6
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91890903"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>최적 성능을 위해 최대 병렬 처리 수준 옵션 설정
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 규칙은 8보다 큰 값에 대한 MAXDOP(max degree of parallelism) 옵션을 결정합니다. 이 옵션을 큰 값으로 설정하면 불필요하게 리소스가 소비되고 성능이 저하될 수 있습니다.  
  
## <a name="best-practice-recommendations"></a>모범 사례 권장 사항  
 MAXDOP(최대 병렬 처리 수준) 구성 옵션은 병렬 계획에서 쿼리를 실행하는 데 사용되는 프로세서 수를 제어합니다. 이 옵션은 작업을 병렬로 수행하는 쿼리 계획 연산자에 사용되는 스레드 수를 결정합니다. SMP(대칭적 다중 처리) 컴퓨터, NUMA(Non-Uniform Memory Access) 컴퓨터 또는 하이퍼스레딩 사용 프로세서에서 SQL Server가 설정되었는지에 따라, 최대 병렬 처리 수준 옵션을 적절하게 구성해야 합니다. 
 
 MAXDOP 구성에 대한 권장 사항은 사용 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 따라 달라집니다. 버전 관련 지침은 [최대 병렬 처리 수준 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)을 참조하고, 이에 따라 최대 병렬 처리 수준 값을 확인하도록 정책을 구성합니다.     
  
## <a name="for-more-information"></a>참조 항목  
 [SQL Server의 최대 병렬 처리 수준 구성 옵션에 대한 권장 사항 및 지침](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)    
 [최대 병렬 처리 수준 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)     
