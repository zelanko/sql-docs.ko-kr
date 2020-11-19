---
title: Java용 Microsoft 확장성 SDK
description: Java용 Microsoft 확장성 SDK를 사용하여 SQL Server용 Java 프로그램을 구현하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: language-extensions
ms.date: 11/05/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 011d8ba2e9c92d0df6fe2956c190f61934948f54
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870139"
---
# <a name="microsoft-extensibility-sdk-for-java-for-sql-server"></a>SQL Server에 대한 Java용 Microsoft 확장성 SDK
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

Java용 Microsoft 확장성 SDK를 사용하여 SQL Server용 Java 프로그램을 구현하는 방법을 알아봅니다. 이 SDK는 SQL Server와 데이터를 교환하고 SQL Server에서 Java 코드를 실행하는 데 사용되는 Java 언어 확장용 인터페이스입니다.

이 SDK는 Windows 및 Linux에서 SQL Server 2019 릴리스 후보 1의 일부로 설치됩니다.

+ Windows 기본 설치 경로: **[인스턴스 설치 홈 디렉터리]\MSSQL\Binn\mssql-java-lang-extension.jar**
+ Linux 기본 설치 경로: **/opt/mssql/lib/mssql-java-lang-extension.jar**

이 코드는 오픈 소스이며 [SQL Server 언어 확장 GitHub 리포지토리](https://github.com/microsoft/sql-server-language-extensions)에서 찾을 수 있습니다.

## <a name="implementation-requirements"></a>구현 요구 사항

SDK 인터페이스는 SQL Server가 Java 런타임과 통신하기 위해 충족해야 하는 요구 사항 집합을 정의합니다. SDK를 사용하려면 기본 클래스에서 몇 가지 구현 규칙을 따라야 합니다. 그러면 SQL Server가 Java 클래스에서 특정 메서드를 실행하고 Java 언어 확장을 사용하여 데이터를 교환할 수 있습니다.

SDK를 사용하는 방법에 대한 예제를 보려면 [자습서: Java에서 regex(정규식)를 사용하여 문자열 검색](../tutorials/search-for-string-using-regular-expressions-in-java.md)을 참조하세요.

## <a name="sdk-classes"></a>SDK 클래스

SDK는 세 가지 클래스로 구성되어 있습니다.

Java 확장이 SQL Server와 데이터를 교환하는 데 사용하는 인터페이스를 정의하는 두 개의 추상 클래스.

- **AbstractSqlServerExtensionExecutor**
- **AbstractSqlServerExtensionDataset**

세 번째 클래스는 데이터 집합 개체의 구현을 포함하는 도우미 클래스입니다. 이 클래스는 사용할 수 있는 선택적 클래스로, 이를 통해 쉽게 시작할 수 있습니다. 대신 그러한 클래스의 자체 구현을 사용할 수도 있습니다.

- **PrimitiveDataset**

아래에는 SDK의 각 클래스에 대한 설명이 나와 있습니다. SDK 클래스의 소스 코드는 [SQL Server 언어 확장 GitHub 리포지토리](https://github.com/microsoft/sql-server-language-extensions/tree/master/language-extensions/java/sdk)에서 이용할 수 있습니다.

### <a name="class-abstractsqlserverextensionexecutor"></a>클래스: AbstractSqlServerExtensionExecutor

**AbstractSqlServerExtensionExecutor** 추상 클래스에는 SQL Server에 대한 Java 언어 확장으로 Java 코드를 실행하는 데 사용되는 인터페이스가 포함되어 있습니다.

기본 Java 클래스는 이 클래스에서 상속해야 합니다. 이 클래스에서 상속한다는 것은 클래스에 자체 클래스에서 구현해야 하는 특정 메서드가 있음을 의미합니다.

이 추상 클래스에서 상속하려면 클래스 선언에서 추상 클래스 이름으로 확장합니다.

```java
public class <MyClass> extends AbstractSqlServerExtensionExecutor {}
```

최소한, 기본 클래스는 execute(...) 메서드를 구현해야 합니다.

#### <a name="method-execute"></a>메서드 execute

execute 메서드는 SQL Server에서 Java 코드를 호출하기 위해 Java 언어 확장을 통해 SQL Server에서 호출되는 메서드입니다. SQL Server에서 실행하려는 주요 작업을 포함하는 주요 메서드입니다.

SQL Server에서 Java로 메서드 인수를 전달하려면 `sp_execute_external_script`에 `@param` 매개 변수를 사용합니다. **execute** 메서드는 해당 방식으로 인수를 사용합니다.

```java
public AbstractSqlServerExtensionDataset execute(AbstractSqlServerExtensionDataset input, LinkedHashMap<String, Object> params)  {}
```

#### <a name="method-init"></a>메서드 init

init 메서드는 생성자 뒤, execute 메서드 앞에서 실행됩니다. execute(...) 전에 실행해야 하는 모든 작업을 이 메서드에서 수행할 수 있습니다.

```java
public void init(String sessionId, int taskId, int numtask) {}
```

### <a name="class-abstractsqlserverextensiondataset"></a>클래스: AbstractSqlServerExtensionDataset

**AbstractSqlServerExtensionDataset** 추상 클래스는 Java 확장에서 사용하는 입력 및 출력 데이터를 처리하기 위한 인터페이스를 포함합니다.


### <a name="class-primitivedataset"></a>클래스: PrimitiveDataset

**PrimitiveDataset** 클래스는 단순 형식을 기본 배열로 저장하는 **AbstractSqlServerExtensionDataset** 의 구현입니다.

SDK에서 선택적 도우미 클래스로만 제공됩니다. 이 클래스를 사용하지 않는 경우 **AbstractSqlServerExtensionDataset** 에서 상속하는 자체 클래스를 구현해야 합니다.  

## <a name="next-steps"></a>다음 단계

+ [자습서: Java에서 regex(정규식)를 사용하여 문자열 검색](../tutorials/search-for-string-using-regular-expressions-in-java.md)
+ [SQL Server에서 Java를 호출하는 방법](call-java-from-sql.md)
