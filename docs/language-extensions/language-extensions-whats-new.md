---
title: SQL Server 언어 확장의 새로운 기능
titleSuffix: ''
description: 외부 언어와 데이터 플랫폼 간의 통합을 확장하고 심화하는 SQL Server 언어 확장의 새로운 기능에 대해 알아봅니다.
author: dphansen
ms.author: davidph
ms.date: 11/09/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: b737f8764f387faa88d0e5de0c844e55c89a4a30
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471704"
---
# <a name="whats-new-in-sql-server-language-extensions"></a>SQL Server 언어 확장의 새로운 기능
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

Microsoft는 외부 언어와 데이터 플랫폼 간의 통합을 계속 확장하고 발전시키고 있으며, 릴리스마다 SQL Server에 [언어 확장](language-extensions-overview.md) 기능을 추가하고 있습니다.

## <a name="sql-server-2019"></a>SQL Server 2019

SQL Server 2019의 새로운 [언어 확장](language-extensions-overview.md) 기능은 아래에서 찾을 수 있습니다. 이 릴리스의 모든 기능에 대한 자세한 내용은 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md) 및 [Release Notes for SQL Server 2019](../sql-server/sql-server-version-15-release-notes.md)(SQL Server 2019 릴리스 정보)를 참조하세요.

### <a name="new-python-and-r-language-extensions"></a>새로운 Python 및 R 언어 확장

- [Python 사용자 지정 런타임](../machine-learning/install/custom-runtime-python.md)을 언어 확장과 함께 사용할 수 있습니다. 자세한 내용은 [Windows에 Python 사용자 지정 런타임 설치](../machine-learning/install/custom-runtime-python.md?view=sql-server-ver15&preserve-view=true) 또는 [Linux에 Python 사용자 지정 런타임 설치](../machine-learning/install/custom-runtime-python.md?view=sql-server-linux-ver15&preserve-view=true) 방법을 참조하세요.

- [R 사용자 지정 런타임](../machine-learning/install/custom-runtime-r.md)을 언어 확장과 함께 사용할 수 있습니다. 자세한 내용은 [Windows에 R 사용자 지정 런타임 설치](../machine-learning/install/custom-runtime-r.md?view=sql-server-ver15&preserve-view=true) 또는 [Linux에 R 사용자 지정 런타임 설치](../machine-learning/install/custom-runtime-r.md?view=sql-server-linux-ver15&preserve-view=true) 방법을 참조하세요.

### <a name="new-java-language-extension"></a>새 Java 언어 확장

- Windows 및 Linux의 기본 Java 런타임은 Open Zulu JRE이며, [SQL Server Language Extensions installation on Windows](install/windows-java.md)(Windows에 SQL Server 언어 확장 설치) 및 [Linux에 SQL Server 언어 확장 설치](../linux/sql-server-linux-setup-language-extensions-java.md)에 포함되어 있습니다.
- 지원되는 [Java 데이터 형식](how-to/java-to-sql-data-types.md).
- SQL Server에서 외부 언어(예: Java)를 등록하는 데 사용되는 [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md).
- [Microsoft Extensibility SDK for Java](how-to/extensibility-sdk-java-sql-server.md)(Java용 Microsoft 확장성 SDK).
- Windows 및 Linux에서 [CREATE EXTERNAL LIBRARY(Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) 문을 사용하여 외부 라이브러리에 있는 Java 코드에 액세스할 수 있습니다. 자세한 정보: [SQL Server에서 Java를 호출하는 방법](how-to/call-java-from-sql.md)
- Windows 및 Linux의 [Java 언어 확장](language-extensions-overview.md). 사용 권한을 할당하고 경로를 설정하여 SQL Server에서 컴파일된 Java 코드를 사용할 수 있도록 설정할 수 있습니다. SQL Server에 액세스할 수 있는 클라이언트 앱은 SQL Server Machine Learning Services에서 R 및 Python 통합에 사용되는 것과 동일한 절차인 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 호출하여 데이터를 사용하고 코드를 실행할 수 있습니다.

## <a name="next-steps"></a>다음 단계

+ [Windows에 SQL Server 언어 확장 설치](install/windows-java.md) 또는 [Linux에 SQL Server 언어 확장 설치](../linux/sql-server-linux-setup-language-extensions-java.md)
