---
title: 데이터 원본에서 데이터 업데이트
description: 데이터베이스의 데이터를 수정하는 명령 또는 저장 프로시저를 실행하는 방법을 설명합니다.
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: 55c545e5-dcd5-4323-a5b9-3825c2157462
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 41b81d0adedf48f0e33efe6c60d83dd4ed7b597a
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96428248"
---
# <a name="updating-data-in-a-data-source"></a>데이터 원본에서 데이터 업데이트

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

INSERT, UPDATE 또는 DELETE와 같이 데이터를 수정하는 SQL 문은 행을 반환하지 않습니다. 마찬가지로 대부분의 저장 프로시저도 동작을 수행하기는 하지만 행을 반환하지는 않습니다. 행을 반환하지 않는 명령을 실행하려면 필요한 **Parameters** 를 포함하여 적절한 SQL 명령 및 **Connection** 으로 **Command** 개체를 만듭니다. <xref:Microsoft.Data.SqlClient.SqlCommand> 개체의 <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> 메서드를 사용하여 명령을 실행합니다.

> [!NOTE]
> **ExecuteNonQuery** 메서드는 실행된 문 또는 저장 프로시저의 영향을 받는 행의 수를 나타내는 정수를 반환합니다. 여러 문을 실행하는 경우 반환되는 값은 실행된 모든 문에 의해 영향을 받는 레코드의 합계입니다.

## <a name="example"></a>예

다음 코드 예제에서는 **ExecuteNonQuery** 를 사용하여 레코드를 데이터베이스에 삽입하기 위한 INSERT 문을 실행합니다.
  
[!code-csharp[DataWorks SqlCommand.ExecuteNonQuery#1](~/../sqlclient/doc/samples/SqlCommand_ExecuteNonQuery_SP_DML.cs#1)]

다음 코드 예제에서는 [카탈로그 작업 수행](perform-catalog-operations.md)에 있는 샘플 코드에서 만든 저장 프로시저를 실행합니다. 저장 프로시저가 행을 반환하지 않으므로 **ExecuteNonQuery** 메서드가 사용되지만 저장 프로시저는 입력 매개 변수를 받고 출력 매개 변수와 반환 값을 반환합니다.

[!code-csharp[DataWorks SqlCommand.ExecuteNonQuery#2](~/../sqlclient/doc/samples/SqlCommand_ExecuteNonQuery_SP_DML.cs#2)]

## <a name="see-also"></a>참조

- [명령을 사용하여 데이터 수정](use-commands-to-modify-data.md)
- [명령 및 매개 변수](commands-parameters.md)
