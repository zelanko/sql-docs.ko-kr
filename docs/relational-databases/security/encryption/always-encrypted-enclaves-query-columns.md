---
title: 보안 enclave를 사용한 Always Encrypted를 이용하는 열 쿼리 | Microsoft Docs
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
ms.openlocfilehash: d0a522d6deb01169189d6f5faaf7ba2f189d1522
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595508"
---
# <a name="query-columns-using-always-encrypted-with-secure-enclaves"></a>보안 enclave를 사용한 Always Encrypted를 이용하는 열 쿼리
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

이 문서에서는 [보안 enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)에 대해 서버 쪽 보안 enclave를 사용하여 암호화된 열에서 쿼리를 실행하기 위한 일반적인 고려 사항을 설명합니다. 

다음 쿼리 유형은 보안 enclave 사용과 관련이 있습니다.
- Enclave 사용 키를 사용하여 내부 암호화 작업을 트리거하는 쿼리 - [Transact-SQL를 사용하여 열 암호화 구성](always-encrypted-enclaves-configure-encryption-tsql.md)을 참조하세요.
- *풍부한 쿼리* - 임의 암호화 및 enclave 사용 키를 사용하여 암호화된 열에 대한 다양한 범위 비교 또는 패턴 일치 작업.
- 임의 암호화 및 enclave 사용 키를 사용하여 암호화된 열에 대한 인덱스를 만들거나 업데이트하는 쿼리. 자세한 내용은 [보안 enclave를 사용한 Always Encrypted를 이용하여 열에 인덱스 만들기 및 사용](always-encrypted-enclaves-create-use-indexes.md)을 참조하세요.

> [!NOTE]
> 풍부한 쿼리 및 인덱스는 임의 암호화를 사용하는 enclave 사용 열(enclave 사용 열 암호화 키로 암호화된 열)에서만 지원됩니다. 결정적 암호화는 풍부한 쿼리 또는 인덱스를 지원하지 않습니다.

> [!NOTE]
> 암호화된 문자열 열에 풍부한 쿼리를 사용하려면 열에 binary2 정렬 순서(BIN2 데이터 정렬)가 있는 데이터 정렬을 사용해야 합니다. 


## <a name="next-steps"></a>Next Steps
- [SSMS로 보안 enclave를 사용한 Always Encrypted를 이용하는 열 쿼리](always-encrypted-enclaves-query-columns-ssms.md)

## <a name="see-also"></a>참고 항목
- [자습서: SSMS를 사용하여 보안 enclave를 사용한 Always Encrypted 시작](../tutorial-getting-started-with-always-encrypted-enclaves.md)

