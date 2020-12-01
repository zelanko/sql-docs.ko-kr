---
description: Always Encrypted에서 Azure Key Vault 공급자 사용을 보여 주는 예제
title: Always Encrypted에서 Azure Key Vault 공급자 사용을 보여 주는 예제 | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2020
ms.reviewer: v-kaywon
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: karinazhou
ms.author: v-jizho2
ms.openlocfilehash: 51c99e679855ca762b7adc5763086b4ded9b6cf5
ms.sourcegitcommit: 4c3949f620d09529658a2172d00bfe37aeb1a387
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2020
ms.locfileid: "96123888"
---
# <a name="example-demonstrating-use-of-azure-key-vault-provider-with-always-encrypted"></a>Always Encrypted에서 Azure Key Vault 공급자 사용을 보여 주는 예제

[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

이 예에서는 암호화된 열에 액세스할 때 Azure Key Vault 공급자를 사용하는 방법을 보여 줍니다.

[!code-csharp [AKVProvider Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderExample.cs#1)]

> [!NOTE]
> - .NET Standard 애플리케이션에 대한 보안 Enclave 없이 Always Encrypted 기능을 사용하려면 **Microsoft.Data.SqlClient** 버전 2.1.0 이상이 필요합니다. 지원되는 .NET Standard 버전은 2.0 이상입니다. 
>
> - Linux 및 macOS에서 Always Encrypted 기능을 사용하려면 **Microsoft.Data.SqlClient** 버전 2.1.0 이상이 필요합니다.

## <a name="see-also"></a>참고 항목

- [보안 Enclave가 사용된 Always Encrypted를 이용한 Azure Key Vault 공급자 사용을 보여 주는 예제](azure-key-vault-enclave-example.md)
- [자습서: 보안 enclave를 사용한 Always Encrypted를 이용하여 .NET 애플리케이션 개발](tutorial-always-encrypted-enclaves-develop-net-apps.md)을 참조하세요.
- [Microsoft .NET Data Provider for SQL Server와 Always Encrypted 사용](sqlclient-support-always-encrypted.md)
