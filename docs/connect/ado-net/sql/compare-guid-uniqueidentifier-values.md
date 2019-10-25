---
title: GUID 및 uniqueidentifier 값 비교
description: SQL Server 및 .NET에서 GUID 및 uniqueidentifier 값을 사용 하는 방법을 보여 줍니다.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: aababd75-2335-43e3-ace8-4b7ae84191a8
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 8a4c5fcc63c2d2ddb8414227ea049e78db1cba10
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452285"
---
# <a name="comparing-guid-and-uniqueidentifier-values"></a>GUID 및 uniqueidentifier 값 비교

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server의 GUID (globally unique identifier) 데이터 형식은 16 바이트 이진 값을 저장 하는 `uniqueidentifier` 데이터 형식으로 표현 됩니다. GUID는 이진 번호이 고, 주된 용도는 많은 사이트에 많은 컴퓨터가 있는 네트워크에서 고유 해야 하는 식별자입니다. Guid는 Transact-sql NEWID 함수를 호출 하 여 생성할 수 있으며 전 세계에서 고유 하 게 보장 됩니다. 자세한 내용은 [uniqueidentifier (transact-sql)](../../../t-sql/data-types/uniqueidentifier-transact-sql.md)를 참조 하세요.  
  
## <a name="working-with-sqlguid-values"></a>SqlGuid 값 사용  
Guid 값은 길고 모호 하므로 사용자에 게는 의미가 없습니다. 키 값에 임의로 생성 된 Guid를 사용 하 고 많은 수의 행을 삽입 하는 경우 인덱스에 임의 i/o를 사용 하 여 성능에 부정적인 영향을 줄 수 있습니다. Guid는 다른 데이터 형식에 비해 상대적으로 크게 커집니다. 일반적으로 다른 데이터 형식이 적합 하지 않은 매우 좁은 시나리오에만 Guid를 사용 하는 것이 좋습니다.  
  
### <a name="comparing-guid-values"></a>GUID 값 비교  
비교 연산자는 `uniqueidentifier` 값으로 사용할 수 있습니다. 그러나 순서는 두 값의 비트 패턴을 비교하여 구현되지 않습니다. `uniqueidentifier` 값에 대해 허용되는 작업은 비교(=, <>, \<, >, \<=, >=) 및 NULL 검사(IS NULL 및 IS NOT NULL)뿐입니다. 다른 산술 연산자는 허용 되지 않습니다.  
  
@No__t_0 및 <xref:System.Data.SqlTypes.SqlGuid>에는 서로 다른 GUID 값을 비교 하는 `CompareTo` 메서드가 있습니다. 그러나 `System.Guid.CompareTo`와 `SqlTypes.SqlGuid.CompareTo`는 다르게 구현 됩니다. <xref:System.Data.SqlTypes.SqlGuid>는 SQL Server 동작을 사용 하 여 `CompareTo`를 구현 하며, 값의 마지막 6 바이트에서 가장 중요 합니다. <xref:System.Guid>는 모두 16 바이트를 계산 합니다. 다음 예제에서는 이러한 동작의 차이를 보여 줍니다. 코드의 첫 번째 섹션은 정렬 되지 않은 <xref:System.Guid> 값을 표시 하 고 코드의 두 번째 섹션에서는 정렬 된 <xref:System.Guid> 값을 보여 줍니다. 세 번째 섹션에서는 정렬 된 <xref:System.Data.SqlTypes.SqlGuid> 값을 보여 줍니다. 출력은 코드 목록 아래에 표시 됩니다.  
  
[!code-csharp[DataWorks SqlGuid#1](~/../sqlclient/doc/samples/SqlGuid.cs#1)]
  
이 예에서 생성되는 결과는 다음과 같습니다.  
  
```console
Unsorted Guids:  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
  
Sorted Guids:  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
  
Sorted SqlGuids:  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
```  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server 데이터 형식 및 ADO.NET](sql-server-data-types.md)
