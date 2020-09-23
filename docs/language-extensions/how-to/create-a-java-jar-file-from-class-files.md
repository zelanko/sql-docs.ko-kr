---
title: 클래스 파일에서 Java jar 파일 만들기
description: SQL Server 언어 확장을 사용하여 Java 코드를 실행할 때 클래스 파일을 jar 파일로 패키지합니다.
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c324fca6893af35cafe6e9f65eccd0e8a0e478f9
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180285"
---
# <a name="create-a-java-jar-file-from-class-files"></a>클래스 파일에서 Java jar 파일 만들기
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

[SQL Server 언어 확장](../language-extensions-overview.md)을 사용하여 Java 코드를 실행할 때 클래스 파일을 jar 파일로 패키징하는 방법을 알아봅니다. 파일을 패키징하는 것이 좋습니다.

## <a name="create-a-jar-file"></a>jar 파일 만들기

클래스 파일에서 jar 파일을 만들려면 클래스 파일이 포함된 폴더로 이동하고 다음 명령을 실행합니다.

```cmd
jar -cf <MyJar.jar> *.class
```

`jar.exe` 경로가 시스템 경로 변수의 일부인지 확인합니다. 또는 JDK 폴더의 `/bin` 아래에서 찾을 수 있는 jar 파일 전체 경로를 지정합니다. 다음은 그 예입니다.

```cmd
C:\Users\MyUser\Desktop\jdk1.8.0_201\bin\jar -cf <MyJar.jar> *.class
```

## <a name="next-steps"></a>다음 단계

+ [SQL Server 언어 확장에서 Java 런타임을 호출하는 방법](../how-to/call-java-from-sql.md)