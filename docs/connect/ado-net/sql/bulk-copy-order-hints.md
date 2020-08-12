---
title: 대량 복사 작업을 위한 순서 힌트
description: 대량 복사 작업에서 순서 힌트를 사용하는 방법을 설명합니다.
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: c7365bdc6da75e04d019ca1a6a87b90dd8d4ec3c
ms.sourcegitcommit: 6b3569977b034554883a94d73d1c4df6e2f74fe2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2020
ms.locfileid: "85110184"
---
# <a name="order-hints-for-bulk-copy-operations"></a>대량 복사 작업을 위한 순서 힌트

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

대량 복사 작업은 SQL Server 테이블에 데이터를 로드하는 다른 방법에 비해 상당한 성능 이점을 제공합니다. 순서 힌트를 사용하여 성능을 향상할 수 있습니다. 대량 복사 작업에 순서 힌트를 지정하면 클러스터형 인덱스가 있는 테이블에 정렬된 데이터를 삽입하는 시간을 줄일 수 있습니다.

기본적으로 대량 삽입 작업은 들어오는 데이터가 정렬되지 않았음을 전제로 합니다. SQL Server는 이 데이터를 대량으로 로드하기 전에 강제로 데이터를 중간 정렬합니다. 들어오는 데이터가 이미 정렬되어 있는 경우에는 순서 힌트를 사용하여 대량 복사 작업에 클러스터형 인덱스의 일부인 대상 열의 정렬 순서를 알릴 수 있습니다.
  
## <a name="adding-order-hints-to-a-bulk-copy-operation"></a>대량 복사 작업에 순서 힌트 추가  
다음 예제에서는 **AdventureWorks** 샘플 데이터베이스의 원본 테이블에서 동일한 데이터베이스의 대상 테이블로 데이터를 대량 복사합니다. **ProductNumber** 열의 정렬 순서를 정의하기 위해 SqlBulkCopyColumnOrderHint 개체가 생성됩니다. 그런 다음 SqlBulkCopy 인스턴스에 순서 힌트가 추가됩니다. 그러면 결과 `INSERT BULK` 쿼리에 적절한 순서 힌트 인수가 추가됩니다.

[!code-csharp [SqlBulkCopy.ColumnOrderHint#1](~/../sqlclient/doc/samples/SqlBulkCopy_ColumnOrderHint.cs#1)]

## <a name="next-steps"></a>다음 단계
- [SQL Server에서 대량 복사 작업](bulk-copy-operations-sql-server.md)
