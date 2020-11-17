---
title: Java 언어 확장이란?
titleSuffix: SQL Server Language Extensions
description: Java 언어 확장은 외부 Java 코드를 실행하는 데 사용되는 SQL Server의 기능입니다. 확장성 프레임워크를 사용하여 외부 Java 코드에 관계형 데이터를 사용할 수 있습니다.
author: dphansen
ms.author: davidph
ms.date: 11/10/2020
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6489ce49a1236f65ef5ff2fec677327bd6a7f84e
ms.sourcegitcommit: 4545b502e3cae7136411fd9a7c15450315665f38
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2020
ms.locfileid: "94549991"
---
# <a name="what-is-java-language-extension"></a>Java 언어 확장이란?
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

Java 언어 확장은 외부 Java 코드를 실행하는 데 사용되는 SQL Server의 기능입니다. [확장성 프레임워크](concepts/extensibility-framework.md)를 사용하여 외부 Java 코드에 관계형 데이터를 사용할 수 있습니다. Java 언어 확장은 [SQL Server 언어 확장](language-extensions-overview.md)의 일부입니다.

기본 Java 런타임은 Zulu Open JRE입니다. 다른 Java JRE 또는 SDK를 사용할 수도 있습니다.

## <a name="what-you-can-do-with-the-java-language-extension"></a>Java 언어 확장으로 수행 가능한 작업

Java 언어 확장은 외부 Java 코드를 실행하는 데 확장성 프레임워크를 사용합니다. 코드 실행이 코어 엔진 프로세스에서 격리되지만 SQL Server 쿼리 실행에 완전히 통합됩니다. 데이터 원본에서 Java 코드를 실행할 수 있으므로 네트워크를 통해 데이터를 끌어오지 않아도 됩니다.

외부 Java 언어는 [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql)를 사용하여 정의됩니다. 시스템 저장 프로시저 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)가 Java 코드를 실행하기 위한 인터페이스로 사용됩니다.

## <a name="get-started-with-java-language-extension"></a>Java 언어 확장 시작

1. [Windows에 SQL Server Java 언어 확장을 설치하거나](install/windows-java.md) [Linux에 SQL Server Java 언어 확장을 설치합니다](../linux/sql-server-linux-setup-language-extensions-java.md).

1. 개발 도구를 구성합니다.

    + Java 코드 개발에는 선호하는 IDE를 사용합니다.
    + SQL Server에서 Java 코드를 실행하려면 [Java용 Microsoft 확장성 SDK](how-to/extensibility-sdk-java-sql-server.md)를 설치합니다.
    + SQL Server에서 외부 코드를 실행하는 데는 [Azure Data Studio](../azure-data-studio/what-is.md)를 사용합니다.
    + SQL Server에서 Java 코드를 실행하려면 시스템 저장 프로시저 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)를 사용합니다.

1. 첫 번째 Java 코드를 작성합니다.

    + [자습서: Java를 사용하는 정규식](tutorials/search-for-string-using-regular-expressions-in-java.md)

## <a name="limitations"></a>제한 사항

입력 및 출력 버퍼의 값 개수가 Java의 배열에서 할당될 수 있는 최대 요소 수인 `MAX_INT (2^31-1)`를 초과할 수 없습니다.

## <a name="next-steps"></a>다음 단계

+ [Windows에 SQL Server Java 언어 확장 설치](install/windows-java.md) 또는 [Linux에 SQL Server Java 언어 확장 설치](../linux/sql-server-linux-setup-language-extensions-java.md)
+ [Java 용 Microsoft 확장성 SDK](how-to/extensibility-sdk-java-sql-server.md) 설치
