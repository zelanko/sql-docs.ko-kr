---
title: SQL Server 언어 확장의 새로운 기능
titleSuffix: ''
description: 외부 언어와 데이터 플랫폼 간의 통합을 확장하고 심화하는 SQL Server 언어 확장의 새로운 기능에 대해 알아봅니다.
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ca15786b88c62b41202310bd537a3224ddea458e
ms.sourcegitcommit: fe59f8dc27fd633f5dfce54519d6f5dcea577f56
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91934878"
---
# <a name="whats-new-in-sql-server-language-extensions"></a>SQL Server 언어 확장의 새로운 기능
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

Microsoft는 외부 언어와 데이터 플랫폼 간의 통합을 계속 확장하고 발전시키고 있으며, 릴리스마다 SQL Server에 [언어 확장](language-extensions-overview.md) 기능을 추가하고 있습니다.

## <a name="new-python-and-r-language-extensions-in-sql-server-2019"></a>SQL Server 2019의 새로운 Python 및 R 언어 확장

+ [Windows의 Python](../machine-learning/install/custom-runtime-python.md)에 사용자 지정 런타임을 사용할 수 있습니다. Linux에 설치하려면 [Linux에 SQL Server용 Python 사용자 지정 런타임 설치](../machine-learning/install/custom-runtime-python.md?view=sql-server-linux-ver15&preserve-view=true)를 참조하세요.

+ [Windows의 R](../machine-learning/install/custom-runtime-r.md)에 사용자 지정 런타임을 사용할 수 있습니다. Linux에 설치하려면 [Linux에 SQL Server용 R 사용자 지정 런타임 설치](../machine-learning/install/custom-runtime-r.md?view=sql-server-linux-ver15&preserve-view=true)를 참조하세요.


## <a name="new-java-language-extension-in-sql-server-2019"></a>SQL Server 2019의 새로운 Java 언어 확장

이 릴리스의 모든 기능에 대한 자세한 내용은 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md) 및 [Release Notes for SQL Server 2019](../sql-server/sql-server-version-15-release-notes.md)(SQL Server 2019 릴리스 정보)를 참조하세요.

- Windows 및 Linux의 기본 Java 런타임은 Open Zulu JRE이며, [SQL Server Language Extensions installation on Windows](install/install-sql-server-language-extensions-on-windows.md)(Windows에 SQL Server 언어 확장 설치) 및 [Linux에 SQL Server 언어 확장 설치](../linux/sql-server-linux-setup-language-extensions.md)에 포함되어 있습니다.
- 지원되는 [Java 데이터 형식](how-to/java-to-sql-data-types.md).
- SQL Server에서 외부 언어(예: Java)를 등록하는 데 사용되는 [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md).
- [Microsoft Extensibility SDK for Java](how-to/extensibility-sdk-java-sql-server.md)(Java용 Microsoft 확장성 SDK).
- Windows 및 Linux에서 [CREATE EXTERNAL LIBRARY(Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) 문을 사용하여 외부 라이브러리에 있는 Java 코드에 액세스할 수 있습니다. 자세한 정보: [SQL Server에서 Java를 호출하는 방법](how-to/call-java-from-sql.md)
- Windows 및 Linux의 [Java 언어 확장](language-extensions-overview.md). 사용 권한을 할당하고 경로를 설정하여 SQL Server에서 컴파일된 Java 코드를 사용할 수 있도록 설정할 수 있습니다. SQL Server에 액세스할 수 있는 클라이언트 앱은 SQL Server Machine Learning Services에서 R 및 Python 통합에 사용되는 것과 동일한 절차인 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 호출하여 데이터를 사용하고 코드를 실행할 수 있습니다.

## <a name="next-steps"></a>다음 단계

+ [Windows에 SQL Server 언어 확장 설치](install/install-sql-server-language-extensions-on-windows.md) 또는 [Linux에 SQL Server 언어 확장 설치](../linux/sql-server-linux-setup-language-extensions.md)