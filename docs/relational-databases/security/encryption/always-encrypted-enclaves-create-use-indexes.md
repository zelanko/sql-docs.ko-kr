---
description: 보안 Enclave를 사용한 Always Encrypted를 이용하여 열에 인덱스 만들기 및 사용
title: 보안 Enclave를 사용한 Always Encrypted를 이용하여 열에 인덱스 만들기 및 사용 | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 420e2bc398bbaa75c21130b2f9b8e8024d33fd83
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127738"
---
# <a name="create-and-use-indexes-on-columns-using-always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted를 이용하여 열에 인덱스 만들기 및 사용
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

이 문서에서는 [보안 Enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)에서 Enclave 사용 열 암호화 키를 사용하여 암호화된 열에서 인덱스를 만들고 사용하는 방법을 설명합니다. 

보안 Enclave를 사용한 Always Encrypted는 다음을 지원합니다.
- 결정적 암호화 및 Enclave 사용 키를 사용하여 암호화된 열에 대한 클러스터형 및 비클러스터형 인덱스.
  - 이러한 인덱스는 암호 텍스트를 기준으로 정렬됩니다. 이러한 인덱스에는 특별한 고려 사항이 없습니다. 결정적 암호화와 Enclave를 사용하지 않는 키를 사용하여 암호화된 열의 인덱스를 (Always Encrypted와) 동일한 방식으로 관리하고 사용할 수 있습니다. 
- 임의 암호화 및 Enclave 사용 키를 사용하여 암호화된 열에 대한 비클러스터형 인덱스.
  - Enclave 내에서 쿼리를 처리하는 것이 유용하며, 임의 암호화를 사용하여 암호화된 열의 인덱스가 중요한 데이터를 누출하지 않도록 할 수 있습니다. 인덱스 데이터 구조(B 트리)의 키 값은 암호화되고 일반 텍스트 값을 기준으로 정렬됩니다. 자세한 내용은 [임의 암호화를 사용하는 Enclave 사용 열의 인덱스](always-encrypted-enclaves.md#indexes-on-enclave-enabled-columns-using-randomized-encryption)를 참조하세요.

> [!NOTE]
> 이 문서의 나머지 부분에서는 임의 암호화 및 Enclave 사용 키를 사용하여 암호화된 열의 비클러스터형 인덱스에 대해 설명합니다.

임의 암호화 및 Enclave 사용 열 암호화 키를 사용하는 열의 인덱스는 일반 텍스트를 기준으로 정렬된 암호화된(암호 텍스트) 데이터를 포함하므로 SQL Server 엔진은 다음을 포함하여 인덱스를 만들거나 업데이트하거나 검색해야 하는 모든 작업에 Enclave를 사용해야 합니다.

- 인덱스 만들기 또는 다시 작성
- 인덱스의 인덱스 키 삽입 및/또는 제거를 트리거하는 테이블의 행 삽입, 업데이트 또는 삭제(인덱싱된/암호화된 열 포함)
- 인덱스 무결성 검사가 필요한 `DBCC` 명령(예: [DBCC CHECKDB(Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 또는 [DBCC CHECKTABLE(Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)) 실행
- SQL Server에서 인덱스 변경 내용을 취소해야 하는 경우 데이터베이스 복구(예: SQL Server에서 오류가 발생하고 다시 시작된 후)(자세한 내용은 아래 참조)

위의 모든 작업을 수행하려면 Enclave에 인덱싱된 열에 대한 열 암호화 키가 있어야 합니다. 키는 인덱스 키의 암호를 해독하는 데 필요합니다. 일반적으로 enclave는 다음 두 가지 방법 중 하나로 열 암호화 키를 가져올 수 있습니다.
- 클라이언트 애플리케이션에서 직접
- 열 암호화 키 캐시에서

## <a name="invoke-indexing-operations-with-column-encryption-keys-provided-directly-by-the-client"></a>클라이언트에서 직접 제공하는 열 암호화 키를 사용하여 인덱싱 작업 호출
인덱싱 작업을 호출하기 위한 이 방법이 유효하려면 인덱스에서 작업을 트리거하는 쿼리를 실행하는 애플리케이션(예: SSMS(SQL Server Management Studio))이 다음과 같아야 합니다.

- 데이터베이스 연결에 Always Encrypted 및 Enclave 계산을 모두 사용하는 데이터베이스에 연결합니다.
- 애플리케이션이 인덱싱된 열의 열 암호화 키를 보호하는 열 마스터 키에 액세스할 수 있어야 합니다.

SQL Server 엔진이 애플리케이션 쿼리를 구문 분석하고 쿼리를 실행하기 위해 암호화된 열의 인덱스를 업데이트해야 한다고 결정하면, 보안 채널을 통해 필요한 열 암호화 키를 Enclave에 제공하도록 클라이언트 드라이버에 지시합니다. 다른 모든 쿼리를 처리하기 위해 Enclave에 열 암호화 키를 제공하는 데 사용되는 것과 동일한 메커니즘입니다. 예를 들어, 패턴 일치 및 범위 비교를 사용하는 내부 암호화 또는 쿼리입니다.

이 방법은 Always Encrypted 및 Enclave 계산을 사용하는 데이터베이스에 이미 연결된 애플리케이션에서 암호화된 열 인덱스의 현재 상태가 투명하도록 유지하는 데 유용합니다. 애플리케이션 연결은 쿼리 처리에 Enclave를 사용할 수 있습니다. 열에 인덱스를 만든 후, 앱 내부 드라이버가 인덱싱 작업을 위해 열 암호화 키를 enclave에 투명하게 제공합니다. 인덱스를 만드는 경우 애플리케이션이 열 암호화 키를 enclave로 보내야 하는 쿼리 수가 늘어날 수 있습니다.

이 방법을 사용하려면 [보안 Enclave를 사용한 Always Encrypted를 이용하는 열 쿼리](always-encrypted-enclaves-query-columns.md)에서 설명하는 보안 Enclave를 사용하여 쿼리를 실행하는 일반 지침을 따르세요.

이 방법을 사용하는 단계별 지침은 [자습서: 임의 암호화를 사용하는 Enclave 사용 열에 인덱스 만들기 및 사용](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md)을 참조하세요.

## <a name="invoke-indexing-operations-using-cached-column-encryption-keys"></a>캐시된 열 암호화 키를 사용하여 인덱싱 작업 호출

Enclave 계산이 필요한 쿼리 처리를 위해 클라이언트 애플리케이션이 열 암호화 키를 Enclave로 보내면 Enclave는 내부 캐시에 열 암호화 키를 캐시합니다. 이 캐시는 Enclave 내부에 있고 외부에서 액세스할 수 없습니다.

같거나 다른 사용자가 사용하는 같거나 다른 클라이언트 애플리케이션이 필요한 열 암호화를 직접 제공하지 않고 인덱스 작업을 트리거하면 Enclave는 캐시에서 열 암호화 키를 조회합니다. 그 결과, 클라이언트 애플리케이션이 키를 제공하지 않았지만 인덱스 작업이 성공합니다.

인덱싱 작업을 호출하는 이 방법이 성공하려면 애플리케이션이 연결에 대해 Always Encrypted를 사용하지 않는 데이터베이스에 연결되어야 하고, enclave 내부 캐시에서 필요한 열 암호화 키를 사용할 수 있어야 합니다.

작업을 호출하는 이 방법은 인덱스와 관련이 없는 다른 작업에 대해 열 암호화 키가 필요 없는 쿼리에서만 지원됩니다. 예를 들어 `INSERT` 문을 사용하여 암호화된 열을 포함하는 테이블에 행을 삽입하는 애플리케이션은 연결 문자열에서 Always Encrypted를 사용하는 데이터베이스에 연결되어야 하며, 암호화된 열에 인덱스가 있는지 여부와 관계없이 키에 액세스할 수 있어야 합니다.

이 방법은 다음과 같은 경우에 유용합니다.
 - 일반 텍스트로 키와 데이터에 액세스할 수 없는 애플리케이션 및 사용자에게 임의 암호화를 사용한 enclave 사용 열 인덱스의 현재 상태가 투명하도록 유지합니다. 
 - 암호화된 열에 인덱스를 만들어도 기존 쿼리가 중단되지 않도록 합니다. 애플리케이션이 키에 액세스하지 않고도 암호화된 열을 포함하는 테이블에 대해 쿼리를 실행하는 경우 DBA가 인덱스를 만든 후에도 키에 액세스하지 않고 애플리케이션에서 계속 실행할 수 있습니다. 예를 들어, 암호화된 열을 포함하는 **Employees** 테이블에서 아래 쿼리를 실행하는 애플리케이션이 있다고 가정합니다. DBA는 암호화된 열에 인덱스를 만들지 않았습니다.

   ```sql
   DELETE FROM [dbo].[Employees] WHERE [EmployeeID] = 1;
   GO
   ```

   애플리케이션에서 Always Encrypted 및 Enclave 계산을 사용하지 않는 연결을 통해 쿼리를 제출하면 쿼리가 성공합니다. 쿼리는 암호화된 열에 대한 계산을 트리거하지 않습니다. DBA가 암호화된 열에 인덱스를 만든 후에는 쿼리가 인덱스 키 제거를 트리거합니다. 이 경우에는 Enclave에 열 암호화 키가 필요합니다. 그러나 데이터 소유자가 enclave에 열 암호화 키를 제공한 경우 애플리케이션이 동일한 연결을 통해 이 쿼리를 계속 실행할 수 있습니다.

 - DBA가 중요한 데이터에 액세스하지 않고도 암호화된 열에 인덱스를 만들고 변경할 수 있기 때문에 인덱스를 관리할 때 역할을 구분합니다. 

> [!TIP] 
> [sp_Enclave_send_keys (Transact-SQL)](../../system-stored-procedures/sp-enclave-send-keys-sql.md)를 사용하면 인덱스에 사용되는 모든 Enclave 사용 열 암호화 키를 Enclave로 쉽게 보내고 키 캐시를 채울 수 있습니다.

이 방법을 사용하는 단계별 지침은 [자습서: 임의 암호화를 사용하는 Enclave 사용 열에 인덱스 만들기 및 사용](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md)을 참조하세요. 

## <a name="next-steps"></a>다음 단계
- [보안 Enclave를 사용한 Always Encrypted를 이용하는 열 쿼리](always-encrypted-enclaves-query-columns.md)

## <a name="see-also"></a>참고 항목  
- [자습서: 임의 암호화를 사용하는 Enclave 사용 열에 인덱스 만들기 및 사용](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md)을 참조하세요.
- [sp_Enclave_send_keys (Transact-SQL)](../../system-stored-procedures/sp-enclave-send-keys-sql.md)
