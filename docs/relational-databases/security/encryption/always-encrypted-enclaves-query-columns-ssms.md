---
title: SSMS로 보안 enclave를 사용한 Always Encrypted를 이용하는 열 쿼리 | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6bee04f4a794a503b89b73d4ef4a6a1cef897b4b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73595598"
---
# <a name="query-columns-using-always-encrypted-with-secure-enclaves-with-ssms"></a>SSMS로 보안 enclave를 사용한 Always Encrypted를 이용하는 열 쿼리
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

이 문서에서는 SQL Server Management Studio를 사용하여 [보안 enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)에 대해 서버 쪽 보안 enclave를 사용하는 쿼리를 발급하는 방법을 설명하며 여기에는 다음이 포함됩니다.
- 내부 암호화 작업을 트리거하는 쿼리
- Enclave 사용 키로 암호화된 열에 대한 범위 비교 또는 패턴 일치 작업을 포함하여 다양한 계산을 트리거하는 쿼리
- 임의 암호화 및 Enclave 사용 키를 사용하여 암호화된 열에 대한 인덱스를 만들거나 업데이트하는 쿼리.  

SSMS를 사용하여 보안 enclave로 암호화된 열에 대한 쿼리를 실행하려면 [SQL Server Management Studio로 Always Encrypted를 사용하는 열 쿼리](always-encrypted-query-columns-ssms.md)의 지침을 따르세요. 다음은 enclave와 관련하여 주의해야 할 몇 가지 사항입니다.

- SSMS 버전 18.3 이상이 필요합니다.
- Always Encrypted 및 enclave 계산을 사용하도록 설정된 연결에서 보안 enclave을 활용하여 쿼리 창에서 쿼리를 실행해야 합니다. 자세한 지침은 [자습서: SSMS를 사용하여 보안 enclaves 사용 Always Encrypted 시작](../tutorial-getting-started-with-always-encrypted-enclaves.md) 및 [데이터베이스 연결에 Always Encrypted 사용 및 사용 안 함](always-encrypted-query-columns-ssms.md#en-dis)을 참조하세요.

## <a name="next-steps"></a>다음 단계
- [보안 enclave를 사용한 Always Encrypted를 이용하여 애플리케이션 개발](always-encrypted-enclaves-client-development.md)

## <a name="see-also"></a>참고 항목  
- [자습서: SSMS를 사용하여 보안 Enclave를 사용한 Always Encrypted 시작](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [Transact-SQL을 사용하여 바로 열 암호화 구성](always-encrypted-enclaves-configure-encryption-tsql.md)
- [보안 Enclave를 사용한 Always Encrypted를 사용하여 열에 인덱스 만들기 및 사용](always-encrypted-enclaves-create-use-indexes.md)

