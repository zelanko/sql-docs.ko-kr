---
title: CLR 사용자 정의 집계 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- custom aggregates [CLR integration]
- calculations [CLR integration]
- user-defined functions [CLR integration]
ms.assetid: bad9b7e8-5967-4afa-8dc8-6d840faf9372
author: rothja
ms.author: jroth
ms.openlocfilehash: 2e654e1e14aa09e5414a100e6d06c64eba93dab7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68009804"
---
# <a name="clr-user-defined-aggregates"></a>CLR 사용자 정의 집계
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  집계 함수는 값 집합에서 계산을 수행하고 단일 값을 반환합니다. 기존에는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 **SUM** 이나 **MAX**와 같이 입력 스칼라 값 집합에 대해 작동하고 해당 집합에서 단일 집계 값을 생성하는 기본 제공 집계 함수만 지원했습니다. 이제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework CLR(공용 언어 런타임)의 통합을 통해 개발자는 관리 코드로 사용자 지정 집계 함수를 만들어 [!INCLUDE[tsql](../../includes/tsql-md.md)]이나 다른 관리 코드에서 이러한 함수에 액세스할 수 있게 만들 수 있습니다.  
  
 다음 표에서는 이 섹션에서 다루는 항목을 나열합니다.  
  
 [CLR 사용자 정의 집계 요구 사항](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates-requirements.md)  
 CLR 사용자 정의 집계 함수를 구현하기 위한 요구 사항에 대해 간략히 설명합니다.  
  
 [CLR 사용자 정의 집계 함수 호출](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
 사용자 정의 집계를 호출하는 방법에 대해 설명합니다.  
  
  
