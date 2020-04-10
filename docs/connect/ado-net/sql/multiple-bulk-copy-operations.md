---
title: 여러 대량 복사 작업
description: SqlBulkCopy 클래스를 사용하여 SQL Server 인스턴스에 데이터의 여러 대량 복사 작업을 수행하는 방법을 설명합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 5ad12f94-7459-4a93-a421-4160d1a90715
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: a0a1f24970801698eedc8971f0db54bd08589945
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924292"
---
# <a name="multiple-bulk-copy-operations"></a>여러 대량 복사 작업

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

<xref:Microsoft.Data.SqlClient.SqlBulkCopy> 클래스의 단일 인스턴스를 사용하여 여러 대량 복사 작업을 수행할 수 있습니다. 복사본 간에 작업 매개 변수(예: 대상 테이블의 이름)가 변경되는 경우 다음 예제에 설명된 대로 **WriteToServer** 메서드에 대한 후속 호출 전에 업데이트해야 합니다. 명시적으로 변경한 경우가 아니라면 모든 속성 값이 지정된 인스턴스에 대한 이전 대량 복사 작업 시와 동일하게 유지됩니다.  
  
> [!NOTE]
>  <xref:Microsoft.Data.SqlClient.SqlBulkCopy>의 동일한 인스턴스를 사용하여 여러 대량 복사 작업을 수행하면 일반적으로 각 작업에 대해 별도의 인스턴스를 사용하는 경우보다 더 효율적입니다.  
  
동일한 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 개체를 사용하여 여러 대량 복사 작업을 수행하는 경우 원본 또는 대상 정보가 각 작업에서 동일한지 다른지에 대한 제한이 없습니다. 그러나 서버에 쓸 때마다 열 연결 정보가 제대로 설정되어 있는지 확인해야 합니다.  

## <a name="example"></a>예제

> [!IMPORTANT]
>  이 샘플은 가져올 [대량 복사 샘플 설정](bulk-copy-example-setup.md)에 설명된 대로 작업 테이블을 만들지 않은 경우 실행되지 않습니다. 이 코드는 **SqlBulkCopy**를 사용하는 구문을 보여 주는 용도로 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있으면 Transact-SQL `INSERT … SELECT` 문을 사용하여 데이터를 더 쉽고 빠르게 복사할 수 있습니다.  
  
[!code-csharp[DataWorks SqlBulkCopy_._ColumnMappingOrdersDetails#1](~/../sqlclient/doc/samples/SqlBulkCopy_ColumnMappingOrdersDetails.cs#1)]
  
## <a name="next-steps"></a>다음 단계
- [SQL Server에서 대량 복사 작업](bulk-copy-operations-sql-server.md)
