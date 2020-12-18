---
description: MSSQLSERVER_8632
title: MSSQLSERVER_8632
ms.custom: ''
ms.date: 10/27/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8632 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 36f8b6f7eb55a30becf0f56eb318c6740b5783ec
ms.sourcegitcommit: f87f2f0f1edc91fe400040d8e3a5810347aa8d70
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96868924"
---
# <a name="mssqlserver_8632"></a>MSSQLSERVER_8632
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>세부 정보

|attribute|값|
|---|---|
|제품 이름|SQL Server|
|이벤트 ID|8632|
|이벤트 원본|MSSQLSERVER|
|구성 요소|SQLEngine|
|심볼 이름|QUERY_EXPRESSION_TOO_COMPLEX|
|메시지 텍스트|내부 오류: 식 서비스 제한에 도달했습니다. 쿼리에서 복잡한 식을 찾아서 단순하게 만드십시오.|
||

## <a name="explanation"></a>설명

단일 식에 많은 식별자와 상수가 포함된 쿼리를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 실행하면 오류 8632가 발생합니다. 사용자에게 보고되는 오류 메시지는 다음과 같습니다.

> 서버:  메시지 8632, 수준 17, 상태 2, 줄 1  
내부 오류: 식 서비스 제한에 도달했습니다. 쿼리에서 복잡한 식을 찾아서 단순하게 만드십시오.

## <a name="cause"></a>원인

이 문제는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 쿼리의 단일 식에 포함될 수 있는 식별자 및 상수의 수를 제한하기 때문에 발생합니다. 이 제한은 65,535입니다. 예를 들어 다음 쿼리에는 하나의 식만 있습니다.

```sql
select a, b + c, d + e
```

이 식은 5개의 열을 모두 검색하고 더하기 연산자를 계산한 다음 프로젝션된 결과 세 개를 클라이언트로 보냅니다.

식별자 및 상수의 수에 대한 테스트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 참조된 모든 식별자와 상수를 확장한 후에 수행됩니다. 예를 들어 다음 항목을 확장할 수 있습니다.

- 선택 목록의 별표(*)
- 보기
- 계산된 열 정의

확장 후 개수가 제한을 초과하는 경우 쿼리가 실행되지 않습니다.

## <a name="user-action"></a>사용자 조치

이 문제를 해결하려면 쿼리를 다시 작성합니다. 쿼리의 가장 큰 식에서 더 적은 식별자와 상수를 참조합니다. 쿼리의 각 식에서 식별자와 상수의 수가 제한을 초과하지 않도록 해야 합니다. 이렇게 하려면 쿼리를 둘 이상의 단일 쿼리로 분할해야 할 수 있습니다. 그런 다음 임시 중간 결과를 만듭니다.
