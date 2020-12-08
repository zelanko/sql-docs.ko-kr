---
title: 데이터베이스에서 단일 값 가져오기
description: ADO.NET에서 단일 값을 반환하는 방법을 알아봅니다. 이 예제 코드는 삽입된 레코드의 ID 열 값을 반환합니다.
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: b38526cd-a62a-48cb-822a-e91dfa68e02d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: c4815d048e5648e2c89c2cc32b8f159cc515f2b5
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96428232"
---
# <a name="obtaining-a-single-value-from-a-database"></a>데이터베이스에서 단일 값 가져오기

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

테이블이나 데이터 스트림 형식보다는 단순히 단일 값인 데이터베이스 정보를 반환해야 하는 경우가 있습니다. 예를 들어 COUNT(\*), SUM(Price) 또는 AVG(Quantity)와 같은 집계 함수의 결과를 반환하려 할 수 있습니다. **Command** 개체는 **ExecuteScalar** 메서드를 사용하여 단일 값을 반환하는 기능을 제공합니다. **ExecuteScalar** 메서드는 결과 집합에서 첫째 행의 첫째 열 값을 스칼라 값으로 반환합니다.

## <a name="example"></a>예

다음 코드 예제에서는 <xref:Microsoft.Data.SqlClient.SqlCommand>를 사용하여 데이터베이스에 새 값을 삽입합니다. 여기서 <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteScalar%2A> 메서드는 삽입된 레코드의 ID 열 값을 반환하는 데 사용됩니다.

[!code-csharp[DataWorks SqlCommand.ExecuteScalar#1](~/../sqlclient/doc/samples/SqlCommand_ExecuteScalar_Return_Id.cs#1)]

## <a name="see-also"></a>참조

- [명령 및 매개 변수](commands-parameters.md)
- [명령 실행](execute-command.md)
