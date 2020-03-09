---
title: GUID 및 uniqueidentifier 값 비교
description: SQL Server 및 .NET에서 GUID 및 uniqueidentifier 값을 사용하는 방법을 보여 줍니다.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: aababd75-2335-43e3-ace8-4b7ae84191a8
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 22d27f9a80765aacdfab25c568e8e2635f1779cc
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/07/2020
ms.locfileid: "78897026"
---
# <a name="comparing-guid-and-uniqueidentifier-values"></a>GUID 및 uniqueidentifier 값 비교

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server의 GUID(고유 식별자) 데이터 형식은 16바이트 이진 값을 저장하는 `uniqueidentifier` 데이터 형식으로 표현됩니다. GUID는 이진 숫자이고, 기본 용도는 많은 사이트에 많은 컴퓨터가 있는 네트워크에서 고유해야 하는 식별자입니다. GUID는 Transact-SQL NEWID 함수를 호출하여 생성할 수 있으며 전역적으로 고유합니다. 자세한 내용은 [uniqueidentifier(Transact-SQL)](../../../t-sql/data-types/uniqueidentifier-transact-sql.md)를 참조하세요.  
  
## <a name="working-with-sqlguid-values"></a>SqlGuid 값 사용  
GUID 값은 길고 모호하므로 사용자에게는 의미가 없습니다. 키 값에 임의로 생성된 GUID를 사용하고 많은 수의 행을 삽입하는 경우 인덱스에 임의 I/O를 가져오게 되므로 성능에 부정적인 영향을 줄 수 있습니다. 또한 GUID는 다른 데이터 형식에 비해 상대적으로 큽니다. 일반적으로 다른 데이터 형식이 적합하지 않은 매우 제한적인 시나리오에만 GUID를 사용하는 것이 좋습니다.  
  
### <a name="comparing-guid-values"></a>GUID 값 비교  
비교 연산자는 `uniqueidentifier` 값으로 사용할 수 있습니다. 그러나 순서는 두 값의 비트 패턴을 비교하여 구현되지 않습니다. `uniqueidentifier` 값에 대해 허용되는 작업은 비교(=, <>, \<, >, \<=, >=) 및 NULL 검사(IS NULL 및 IS NOT NULL)뿐입니다. 다른 산술 연산자는 사용할 수 없습니다.  
  
<xref:System.Guid> 및 <xref:System.Data.SqlTypes.SqlGuid>에는 GUID 값을 비교하는 `CompareTo` 메서드가 있습니다. 그러나 `System.Guid.CompareTo`와 `SqlTypes.SqlGuid.CompareTo`는 다르게 구현됩니다. <xref:System.Data.SqlTypes.SqlGuid>는 SQL Server 동작을 사용하여 `CompareTo`를 구현합니다. 값의 마지막 6바이트가 가장 중요합니다. <xref:System.Guid>는 16바이트를 모두 평가합니다. 다음 예제에서는 이러한 동작의 차이를 보여 줍니다. 코드의 첫 번째 섹션은 정렬되지 않은 <xref:System.Guid> 값을 표시하고 코드의 두 번째 섹션은 정렬된 <xref:System.Guid> 값을 표시합니다. 세 번째 섹션은 정렬된 <xref:System.Data.SqlTypes.SqlGuid> 값을 표시합니다. 출력은 코드 목록 아래에 표시됩니다.  
  
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
