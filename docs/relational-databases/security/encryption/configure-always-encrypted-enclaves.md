---
title: 보안 enclave를 사용한 Always Encrypted 구성 및 사용 | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: bda4d41d4f2a9c92dca2d41b959ad4c4b32a1c79
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594473"
---
# <a name="configure-and-use-always-encrypted-with-secure-enclaves"></a>보안 enclave를 사용한 Always Encrypted 구성 및 사용 

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[보안 Enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)는 기존 [Always Encrypted](always-encrypted-database-engine.md) 기능을 확장하여 데이터 기밀성을 유지하면서 중요한 데이터에 대해 보다 풍부한 기능을 사용하도록 설정합니다. 이 문서에서는 이 기능을 구성 및 사용하기 위한 일반적인 작업을 나열합니다.

보안 enclave를 사용한 Always Encrypted를 빠르게 시작하는 방법을 보여주는 자습서는 [자습서: SSMS를 사용하여 보안 enclave로 Always Encrypted 시작](../tutorial-getting-started-with-always-encrypted-enclaves.md)을 참조하세요.

## <a name="set-up-your-environment-to-support-enclaves-and-attestation"></a>Enclave 및 증명을 지원하도록 환경 설정
자세한 내용은 다음 문서를 참조하세요.
- [SQL Server에서 Always Encrypted의 호스트 보호자 서비스 설정](https://docs.microsoft.com/windows-server/security/set-up-hgs-for-always-encrypted-in-sql-server)

## <a name="manage-keys-for-always-encrypted-with-secure-enclaves"></a>보안 enclave를 사용한 Always Encrypted용 키 관리
자세한 내용은 다음 문서를 참조하세요.
- [보안 enclave를 사용한 Always Encrypted용 키 관리 - 개요](always-encrypted-enclaves-manage-keys.md)
- [Enclave 사용 키 프로비전](always-encrypted-enclaves-provision-keys.md)
- [Enclave 사용 키 순환](always-encrypted-enclaves-rotate-keys.md)

## <a name="configure-columns-with-always-encrypted-with-secure-enclaves"></a>보안 enclave를 사용한 Always Encrypted를 이용하여 열 구성
자세한 내용은 다음 문서를 참조하세요.
- [보안 enclave를 사용한 Always Encrypted를 이용하여 내부 열 암호화 구성 - 개요](always-encrypted-enclaves-configure-encryption.md)
- [Transact-SQL을 사용하여 내부 열 암호화 구성](always-encrypted-enclaves-configure-encryption-tsql.md)
- [기존 암호화된 열에 대해 보안 enclave를 사용한 Always Encrypted 사용](always-encrypted-enclaves-enable-for-encrypted-columns.md)

> [!NOTE]
> 테스트 환경을 설정하고 SSMS에서 보안 enclave를 사용하여 Always Encrypted 기능을 사용하는 방법에 대한 단계별 자습서는 [자습서: SSMS를 사용하여 보안 enclave로 Always Encrypted 시작](../tutorial-getting-started-with-always-encrypted-enclaves.md)을 참조하세요.

## <a name="query-columns-using-always-encrypted-with-secure-enclaves"></a>보안 enclave를 사용한 Always Encrypted를 이용하는 열 쿼리
자세한 내용은 다음 문서를 참조하세요.
- [보안 enclave를 사용한 Always Encrypted를 이용하는 열 쿼리 - 개요](always-encrypted-enclaves-query-columns.md)
- [SSMS로 보안 enclave를 사용한 Always Encrypted를 이용하는 열 쿼리](always-encrypted-enclaves-query-columns-ssms.md)

## <a name="create-and-use-indexes-on-enclave-enabled-columns"></a>Enclave 사용 열에 인덱스 만들기 및 사용
자세한 내용은 다음 문서를 참조하세요.
- [보안 enclave를 사용한 Always Encrypted를 이용하여 열에 인덱스 만들기 및 사용](always-encrypted-enclaves-create-use-indexes.md)

## <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>보안 enclave를 사용한 Always Encrypted를 이용하여 애플리케이션 개발
자세한 내용은 다음 문서를 참조하세요.
- [보안 enclave를 사용한 Always Encrypted를 이용하여 애플리케이션 개발](always-encrypted-enclaves-client-development.md)
