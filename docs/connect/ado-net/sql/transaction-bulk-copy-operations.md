---
title: 트랜잭션 및 대량 복사 작업
description: 트랜잭션을 커밋하거나 롤백하는 방법을 포함해 트랜잭션 내에서 대량 복사 작업을 수행하는 방법을 설명합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: f6f0cbc9-f7bf-4d6e-875f-ad1ba0b4aa62
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 82f3f7fd1b796d8854363afd84768cd4ee4d3358
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896000"
---
# <a name="transaction-and-bulk-copy-operations"></a>트랜잭션 및 대량 복사 작업

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

대량 복사 작업은 격리된 작업이나 여러 단계 트랜잭션의 일부로 수행할 수 있습니다. 후자 옵션을 사용하면 동일한 트랜잭션 내에서 둘 이상의 대량 복사 작업을 수행할 뿐만 아니라 전체 트랜잭션을 커밋하거나 롤백하면서 다른 데이터베이스 작업(예: 삽입, 업데이트 및 삭제)을 수행할 수 있습니다.  
  
기본적으로 대량 복사 작업은 격리된 작업으로 수행됩니다. 대량 복사 작업은 트랜잭션되지 않은 방식으로 수행되어 롤백할 수 없습니다. 오류가 발생할 때 대량 복사의 전체 또는 일부를 롤백해야 하는 경우에는 <xref:Microsoft.Data.SqlClient.SqlBulkCopy>에서 관리형 트랜잭션을 사용하거나 기존 트랜잭션 내에서 대량 복사 작업을 수행하거나, 또는 **System.Transactions**<xref:System.Transactions.Transaction>에 인리스트먼트될 수 있습니다.  
  
## <a name="performing-a-non-transacted-bulk-copy-operation"></a>트랜잭션되지 않은 대량 복사 작업 수행  
다음 콘솔 애플리케이션에서는 트랜잭션되지 않은 대량 복사 작업 중 오류가 발생할 경우 어떻게 되는지를 보여 줍니다.  
  
이 예제에서 원본 테이블과 대상 테이블에는 `Identity`ProductID**라는**  열이 각각 포함되어 있습니다. 먼저 코드는 모든 행을 삭제한 다음, **ProductID**가 원본 테이블에 있는 것으로 알려진 단일 행을 삽입하여 대상 테이블을 준비합니다. 기본적으로 `Identity` 열에 대한 새 값은 추가된 각 행에 대한 대상 테이블에 생성됩니다. 이 예제에서 옵션은 대량 로드 프로세스에서 원본 테이블의 `Identity` 값을 대신 강제로 사용하도록 하는 연결을 열 때 설정됩니다.  
  
대량 복사 작업은 <xref:Microsoft.Data.SqlClient.SqlBulkCopy.BatchSize%2A> 속성을 10으로 설정하여 실행됩니다. 작업에서 잘못된 행이 발견되는 경우 예외가 throw됩니다. 이 첫 번째 예제에서는 대량 복사 작업이 트랜잭션되지 않습니다. 오류 지점까지 복사된 모든 일괄 처리가 커밋됩니다. 중복 키가 포함된 일괄 처리는 롤백되고 대량 복사 작업은 다른 모든 일괄 처리를 처리하기 전에 중지됩니다.  
  
> [!NOTE]
>  이 샘플은 가져올 [대량 복사 샘플 설정](bulk-copy-example-setup.md)에 설명된 대로 작업 테이블을 만들지 않은 경우 실행되지 않습니다. 이 코드는 **SqlBulkCopy**를 사용하는 구문을 보여 주는 용도로 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있으면 Transact-SQL`INSERT … SELECT` 문을 사용하여 데이터를 더 쉽고 빠르게 복사할 수 있습니다.  
  
[!code-csharp[DataWorks SqlBulkCopyOpeions_Default#1](~/../sqlclient/doc/samples/SqlBulkCopyOptions_Default.cs#1)]
  
## <a name="performing-a-dedicated-bulk-copy-operation-in-a-transaction"></a>트랜잭션에서 전용 대량 복사 작업 수행  
기본적으로 대량 복사 작업은 고유한 트랜잭션입니다. 전용 대량 복사 작업을 수행하려면 연결 문자열을 사용하여 <xref:Microsoft.Data.SqlClient.SqlBulkCopy>의 새 인스턴스를 만들거나 활성 트랜잭션 없이 기존 <xref:Microsoft.Data.SqlClient.SqlConnection> 개체를 사용합니다. 각 시나리오에서는 대량 복사 작업에서 트랜잭션을 만든 다음 커밋하거나 롤백합니다.  
  
<xref:Microsoft.Data.SqlClient.SqlBulkCopyOptions.UseInternalTransaction> 클래스 생성자에서 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 옵션을 명시적으로 지정하여 명시적으로 대량 복사 작업이 고유한 트랜잭션을 실행하도록 함으로써 대량 복사 작업의 각 일괄 처리가 별도의 트랜잭션 내에서 실행되도록 할 수 있습니다.  
  
> [!NOTE]
>  다른 일괄 처리는 다른 트랜잭션에서 실행되므로 대량 복사 작업 중 오류가 발생하는 경우 현재 일괄 처리의 모든 행이 롤백되지만 이전 일괄 처리의 행은 데이터베이스에 유지됩니다.  
  
다음 콘솔 애플리케이션은 한 가지를 제외하고 이전 예제와 유사합니다. 이 예제에서 대량 복사 작업은 고유 트랜잭션을 관리합니다. 오류 지점까지 복사된 모든 일괄 처리가 커밋됩니다. 중복 키가 포함된 일괄 처리는 롤백되고 대량 복사 작업은 다른 모든 일괄 처리를 처리하기 전에 중지됩니다.  
  
> [!IMPORTANT]
>  이 샘플은 가져올 [대량 복사 샘플 설정](bulk-copy-example-setup.md)에 설명된 대로 작업 테이블을 만들지 않은 경우 실행되지 않습니다. 이 코드는 **SqlBulkCopy**를 사용하는 구문을 보여 주는 용도로 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있으면 Transact-SQL`INSERT … SELECT` 문을 사용하여 데이터를 더 쉽고 빠르게 복사할 수 있습니다.  
  
[!code-csharp[DataWorks SqlBulkCopyOptions_UseInternalTransaction#1](~/../sqlclient/doc/samples/SqlBulkCopyOptions_UseInternalTransaction.cs#1)]
  
## <a name="using-existing-transactions"></a>기존 트랜잭션 사용  
<xref:Microsoft.Data.SqlClient.SqlBulkCopy> 생성자에서 기존 <xref:Microsoft.Data.SqlClient.SqlTransaction> 개체를 매개 변수로 지정할 수 있습니다. 이 상황에서는 대량 복사 작업이 기존 트랜잭션에서 수행되며 트랜잭션 상태가 변경되지 않습니다. 즉, 커밋되거나 중단되지 않습니다. 따라서 애플리케이션이 다른 데이터베이스 작업과 함께 대량 복사 작업을 트랜잭션에 포함할 수 있습니다. 그러나 <xref:Microsoft.Data.SqlClient.SqlTransaction> 개체를 지정하지 않고 null 참조를 전달하며 연결에 활성 트랜잭션이 있는 경우 예외가 throw됩니다.  
  
오류가 발생하여 전체 대량 복사 작업을 롤백해야 하는 경우 또는 롤백할 수 있는 더 큰 프로세스의 일부로 대량 복사를 실행해야 하는 경우 <xref:Microsoft.Data.SqlClient.SqlTransaction> 개체를 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 생성자로 제공할 수 있습니다.  
  
다음 콘솔 애플리케이션은 한 가지 예외를 제외하고 트랜잭션되지 않은 첫 번째 예제와 유사합니다. 이 예제에서는 대량 복사 작업이 더 큰 외부 트랜잭션에 포함됩니다. 기본 키 위반 오류가 발생하면 전체 트랜잭션이 롤백되고 행이 대상 테이블에 추가되지 않습니다.  
  
> [!IMPORTANT]
>  이 샘플은 가져올 [대량 복사 샘플 설정](bulk-copy-example-setup.md)에 설명된 대로 작업 테이블을 만들지 않은 경우 실행되지 않습니다. 이 코드는 **SqlBulkCopy**를 사용하는 구문을 보여 주는 용도로 제공됩니다. 원본 테이블과 대상 테이블이 동일한 SQL Server 인스턴스에 있으면 Transact-SQL`INSERT … SELECT` 문을 사용하여 데이터를 더 쉽고 빠르게 복사할 수 있습니다.  
  
[!code-csharp[DataWorks SqlBulkCopy_ExternalTransaction#1](~/../sqlclient/doc/samples/SqlBulkCopy_ExternalTransaction.cs#1)]
  
## <a name="next-steps"></a>다음 단계
- [SQL Server에서 대량 복사 작업](bulk-copy-operations-sql-server.md)
