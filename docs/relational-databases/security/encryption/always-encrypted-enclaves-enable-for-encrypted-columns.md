---
description: 기존 암호화된 열에 대해 보안 enclave를 사용한 Always Encrypted 사용
title: 기존 암호화된 열에 대해 보안 enclave를 사용한 Always Encrypted 사용 | Microsoft Docs"
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
ms.openlocfilehash: 4ef6fe83bd2d9671ccf43b4957497a8c1fc7a4cf
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130916"
---
# <a name="enable-always-encrypted-with-secure-enclaves-for-existing-encrypted-columns"></a>기존 암호화된 열에 대해 보안 enclave를 사용한 Always Encrypted 사용 
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

이 문서에서는 보안 enclave를 사용한 Always Encrypted의 기능을 잠금 해제하고 기존 암호화된 열에 대해 enclave 계산을 사용하도록 설정하는 방법을 설명합니다.  

enclave가 설정되지 않은 키로 암호화된 기존 열이 있는 경우 enclave 사용 키로 암호화된 열을 만들 수 있습니다. 이렇게 하면 열에 대한 쿼리에서 보안 enclave를 사용할 수 있습니다.

다음과 같이 몇 가지 방법으로 기존 암호화된 열에 enclave 계산을 사용하도록 설정할 수 있습니다.

- **범위/세분성:** 열 하위 집합 또는 지정된 열 마스터 키로 보호되는 모든 열의 Enclave 기능을 사용하도록 설정하고 싶나요?
- **데이터 크기:** Enclave 사용 열로 지정하려는 열이 포함된 테이블의 크기는 얼마나 되나요?
- 열의 암호화 유형을 변경하고 싶나요? 임의 암호화만 리치 계산(패턴 일치, 비교 연산자)을 지원한다는 점에 유의합니다. 결정적 암호화를 사용하여 열을 암호화한 경우에도, 임의 암호화로 다시 암호화하여 리치 계산을 잠금 해제해야 합니다.

다음 섹션에서는 기존 열에 대해 enclave를 사용하도록 설정하는 세 가지 방법에 대해 설명합니다.

## <a name="method-1-rotate-the-column-master-key-to-replace-it-with-an-enclave-enabled-column-master-key"></a>방법 1: 열 마스터 키를 순환하여 enclave 사용 열 마스터 키로 바꾸기
기존 열 마스터 키(enclave 사용 키가 아님)을 enclave 사용 키인 새 열 마스터 키로 바꾸면 결과적으로 해당 열 마스터 키와 관련된 모든 열 암호화 키도 enclave 사용 키로 만듭니다.

- 장점:
  - 데이터를 다시 암호화하지 않으므로 일반적으로 가장 빠른 방법입니다. 이것은 이미 리치 계산에 사용하도록 설정되어 있고 결정적 암호화를 사용하는 대량 데이터를 포함하는 열에 대해 권장되는 방법입니다.
  - 여러 열의 Enclave 기능을 대규모로 사용하도록 설정할 수 있습니다. 열 마스터 키를 enclave 사용 열 마스터 키로 바꾸면 모든 열 암호화 키 및 원래 열 암호화 키와 연결된 모든 암호화된 열이 enclave 사용 방식으로 지정됩니다.
  
- 단점:
  - 암호화 유형을 결정적에서 임의로 변경하는 것을 지원하지 않습니다. 결정적 암호화를 사용하여 암호화된 열에 대한 내부 암호화를 잠금 해제하지만 리치 계산은 설정하지 않습니다. 임의 암호화를 사용하려면 열을 다시 암호화해야 합니다.
  - 지정된 열 마스터 키와 연결된 일부 열만 선택적으로 변환할 수 없습니다.
  - 키 관리 오버 헤드가 발생합니다. 새 열 마스터 키를 만들어 영향을 받는 열을 쿼리하는 애플리케이션에서 사용하도록 해야 합니다.

열 마스터 키를 순환하는 방법에 대한 자세한 내용은 [enclave 사용 키 순환](always-encrypted-enclaves-rotate-keys.md)을 참조하세요.

## <a name="method-2-rotate-the-column-master-key-and-re-encrypt-columns-using-randomized-encryption-in-place"></a>방법 2 열 마스터 키를 순환하고 임의 내부 암호화를 사용하여 열을 다시 암호화
이 방법은 첫 번째 단계로 방법 1을 실행한 다음 열을 다시 암호화합니다. 열은 결정적 암호화를 사용하여 시작하고 임의 암호화를 사용하여 다시 암호화하여 풍부한 쿼리를 잠금 해제합니다.

- 장점:
  - 내부에서 데이터를 다시 암호화합니다. 현재 결정적 암호화를 사용하고 대량 데이터를 포함하는 암호화된 열에 대해 풍부한 쿼리를 사용하도록 설정해야 하는 경우 권장되는 방법입니다. 1단계(열 마스터 키 순환)는 결정적 암호화를 사용하여 열에 대해 내부 암호화를 잠금 해제하고 2단계(열 다시 암호화)는 내부에서 수행할 수 있습니다.
  - 여러 열의 Enclave 기능을 대규모로 사용하도록 설정할 수 있습니다.
  
- 단점:
  - 지정된 열 마스터 키와 연결된 일부 열만 선택적으로 변환할 수 없습니다.
  - 키 관리 오버 헤드가 발생합니다. 새 열 마스터 키를 만들어 영향을 받는 열을 쿼리하는 애플리케이션에서 사용하도록 해야 합니다.

열 마스터 키를 순환하고 내부에서 열을 다시 암호화하여 열 암호화 키를 순환하는 방법에 대한 자세한 내용은 [enclave 사용 키 순환](always-encrypted-enclaves-rotate-keys.md)을 참조하세요.

## <a name="method-3-re-encrypt-a-selected-column-with-an-enclave-enabled-column-encryption-key-on-the-client-side"></a>방법 3: 클라이언트 쪽에서 enclave 사용 열 암호화 키를 사용하여 선택한 열을 다시 암호화
이 방법은 enclave 사용 열 암호화 키를 사용하여 열을 다시 암호화하고 임의 암호화를 사용하여 풍부한 쿼리를 사용하도록 설정합니다. 현재 열 암호화 키에 enclave가 설정되어 있지 않으므로 해당 열을 내부에서 다시 암호화할 수 없습니다. Always Encrypted 마법사 또는 Set-SqlColumnEncryption cmdlet을 사용하여 데이터베이스 외부에서 열을 다시 암호화합니다.

- 장점:
  - 단일 열 또는 열의 작은 하위 집합에 대해 enclave 기능(임의 암호화를 사용하여 열을 다시 암호화하는 경우 내부 암호화 및 풍부한 쿼리)을 선택적으로 사용하도록 설정할 수 있습니다.
  - 그러면 한 단계에서 열에 대해 리치 계산을 수행할 수 있습니다.
  - 새 열 마스터 키를 만들 필요가 없으므로 애플리케이션에 미치는 영향이 더 적습니다.
  
- 단점:
  - 이 도구는 데이터를 다시 암호화하기 위해 데이터를 데이터베이스 외부로 이동하므로 시간이 오래 걸리고 네트워크 오류가 발생할 수 있습니다.

클라이언트 쪽 도구를 통해 열 암호화를 순환하는 방법에 대한 자세한 내용은 [SQL Server Management Studio를 사용하여 Always Encrypted 키 순환](rotate-always-encrypted-keys-using-ssms.md) 및 [PowerShell을 사용하여 Always Encrypted 키 순환](rotate-always-encrypted-keys-using-powershell.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
- [보안 Enclave를 사용한 Always Encrypted를 사용하여 열 쿼리](always-encrypted-enclaves-query-columns.md)
- [보안 enclave를 사용한 Always Encrypted를 이용하여 애플리케이션 개발](always-encrypted-enclaves-client-development.md)
