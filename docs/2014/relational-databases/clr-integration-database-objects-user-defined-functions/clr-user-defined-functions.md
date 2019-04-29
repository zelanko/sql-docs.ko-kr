---
title: CLR 사용자 정의 함수 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- building database objects [CLR integration], user-defined functions
- functions [CLR integration]
- common language runtime [SQL Server], user-defined functions
- database objects [CLR integration], user-defined functions
- user-defined functions [CLR integration]
ms.assetid: 6f7491f1-9a46-4146-ae09-056248634de2
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f48a62e1dff2fbc1d226077c2271e8a8a71efb2e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874487"
---
# <a name="clr-user-defined-functions"></a>CLR 사용자 정의 함수
  사용자 정의 함수는 매개 변수를 사용하여 계산이나 다른 동작을 수행한 다음 결과를 반환하는 루틴입니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#과 같은 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 프로그래밍 언어를 사용하여 사용자 정의 함수를 작성할 수 있습니다.  
  
 함수에는 단일 값을 반환하는 스칼라 반환 함수와 행 집합을 반환하는 테이블 반환 함수의 두 가지 유형이 있습니다.  
  
 다음 표에서는 이 섹션에서 다루는 항목을 나열합니다.  
  
 [CLR 스칼라 반환 함수](clr-scalar-valued-functions.md)  
 스칼라 반환 함수의 구현 요구 사항과 예를 다룹니다.  
  
 [CLR 테이블 반환 함수](clr-table-valued-functions.md)  
 TVF(테이블 반환 함수)를 구현하고 사용하는 방법과 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 CLR(공용 언어 런타임) TVF 간의 차이점을 설명합니다.  
  
 [CLR 사용자 정의 집계](clr-user-defined-aggregates.md)  
 사용자 정의 집계를 구현하고 사용하는 방법을 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [사용자 정의 함수](../user-defined-functions/user-defined-functions.md)  
  
  
