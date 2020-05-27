---
title: SQL Server에서 대량 복사 작업
description: .NET Data Provider for SQL Server의 대량 복사 기능에 대해 설명합니다.
ms.date: 09/30/2019
ms.assetid: 83a7a0d2-8018-4354-97b9-0b1d99f8342b
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: c827ae70d9aa344f52de1d76c482beaef90c09aa
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78897030"
---
# <a name="bulk-copy-operations-in-sql-server"></a>SQL Server에서 대량 복사 작업

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Microsoft SQL Server에는 **bcp**라는 많이 사용되는 명령줄 유틸리티가 있어 SQL Server 데이터베이스의 테이블이나 뷰로 큰 파일을 신속하게 대량 복사할 수 있습니다. <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 클래스를 사용하면 비슷한 기능을 제공하는 관리 코드 솔루션을 작성할 수 있습니다. INSERT 문과 같은 다른 방법을 사용하여 데이터를 SQL Server 테이블에 로드할 수 있지만 <xref:Microsoft.Data.SqlClient.SqlBulkCopy>는 훨씬 더 향상된 성능을 제공합니다.  
  
<xref:Microsoft.Data.SqlClient.SqlBulkCopy> 클래스를 사용하면 다음을 수행할 수 있습니다.  
  
- 단일 대량 복사 작업  
  
- 여러 대량 복사 작업  
  
- 트랜잭션 내의 대량 복사 작업  
  
> [!NOTE]
>  <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 클래스를 지원하지 않는 .NET Framework 버전 1.1 이하를 사용하는 경우 <xref:Microsoft.Data.SqlClient.SqlCommand> 개체를 사용하여 SQL Server Transact-SQL **BULK INSERT** 문을 실행할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
[대량 복사 예제 설정](bulk-copy-example-setup.md)  
대량 복사 예제에 사용된 테이블에 대해 설명하고 AdventureWorks 데이터베이스에서 테이블을 만들기 위한 SQL 스크립트를 제공합니다.  
  
[단일 대량 복사 작업](single-bulk-copy-operations.md)  
<xref:Microsoft.Data.SqlClient.SqlBulkCopy> 클래스를 사용하여 SQL Server 인스턴스에 데이터의 단일 대량 복사를 수행하는 방법 및 Transact-SQL 문과 <xref:Microsoft.Data.SqlClient.SqlCommand> 클래스를 사용하여 대량 복사 작업을 수행하는 방법을 각각 설명합니다.  
  
[여러 대량 복사 작업](multiple-bulk-copy-operations.md)  
<xref:Microsoft.Data.SqlClient.SqlBulkCopy> 클래스를 사용하여 SQL Server 인스턴스에 데이터의 여러 대량 복사 작업을 수행하는 방법을 설명합니다.  
  
[트랜잭션 및 대량 복사 작업](transaction-bulk-copy-operations.md)  
트랜잭션을 커밋하거나 롤백하는 방법을 포함해 트랜잭션 내에서 대량 복사 작업을 수행하는 방법을 설명합니다.  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server 및 ADO.NET](index.md)
