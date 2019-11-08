---
title: 보안 Enclave를 사용한 Always Encrypted를 사용하여 애플리케이션 개발 | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 54e282e7d68c23837c1865f1257ba7e159644d26
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595538"
---
# <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted를 사용하여 애플리케이션 개발
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[보안 Enclave를 사용한 Always Encrypted](always-encrypted-enclaves.md)는 [Always Encrypted](always-encrypted-database-engine.md)를 확장하여 암호화된 중요한 데이터베이스 열에서 더욱 다양한 애플리케이션 쿼리 기능을 지원합니다. 보안 Enclave 기술을 활용하여 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]의 쿼리 실행기가 암호화된 열에 대한 계산을 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 프로세스 내 보안 Enclave로 위임할 수 있도록 합니다.

## <a name="client-driver-for-always-encrypted-with-secure-enclaves"></a>보안 Enclave를 사용한 Always Encrypted의 클라이언트 드라이버

보안 Enclave를 사용한 Always Encrypted를 사용하여 애플리케이션을 개발하려면 보안 Enclave를 지원하는 버전의 SQL 클라이언트 드라이버가 있어야 합니다. 클라이언트 드라이버는 다음과 같은 중요한 역할을 수행합니다.
- 보안 Enclave를 사용한 쿼리를 실행하기 위해 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]에 제출하기 전에 드라이버가 Enclave 증명을 시작하여 보안 Enclave를 신뢰할 수 있고 중요한 데이터를 처리하는 데 안전하게 사용할 수 있는지 확인합니다. 증명에 대한 자세한 내용은 [보안 Enclave 증명](always-encrypted-enclaves.md#secure-enclave-attestation)을 참조하세요.
- 증명이 성공적으로 완료되면 클라이언트 드라이버는 공유 비밀을 협의하여 Enclave와 보안 세션을 설정합니다.
- 드라이버가 공유 비밀을 사용하여 Enclave에서 쿼리를 처리하는 데 필요한 열 암호화 키를 암호화하고 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]로 키를 보냅니다. SQL Server는 키를 보안 Enclave로 전달하여 암호 해독합니다. 
- 마지막으로 드라이버가 실행할 쿼리를 제출하면 보안 Enclave 내에서 계산이 트리거됩니다.

보안 Enclave 기능을 사용하려면 애플리케이션 및 클라이언트 드라이버가 데이터베이스에 연결할 때 Enclave 계산을 사용하도록 구성하고 Enclave 증명 서비스를 가리키는 증명 서비스 엔드포인트(Enclave 증명 URL)를 지정해야 합니다. 세부 정보는 사용 중인 드라이버 및 증명 서비스/프로토콜에 따라 달라집니다.

## <a name="next-steps"></a>다음 단계

보안 Enclave를 사용한 Always Encrypted를 지원하는 클라이언트 드라이버는 다음과 같습니다.
- .NET Framework 4.7.2 이상의 .NET Framework Data Provider for SQL Server 
    - 자세한 내용은 [.NET Framework Data Provider for SQL Server와 Always Encrypted 사용](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)을 참조하세요.
    - 단계별 자습서를 보려면 [자습서: 보안 Enclave를 사용한 Always Encrypted를 사용하여 .NET Framework 애플리케이션 개발](../tutorial-always-encrypted-enclaves-develop-net-framework-apps.md)을 참조하세요.
- Microsoft ODBC Driver for SQL Server 버전 17.4 이상 
    - 자세한 내용은 [상시 암호화와 ODBC 드라이버 사용](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)을 참조하세요. 
    - ODBC를 사용하는 데이터베이스 연결에 Enclave 계산을 사용하는 방법에 대한 자세한 내용은 [보안 Enclave를 사용한 Always Encrypted를 사용하도록 설정](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves) 섹션을 참조하세요.
