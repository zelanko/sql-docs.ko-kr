---
title: 클래스 파일에서 Java jar 파일 만들기
titleSuffix: SQL Server Language Extensions
description: 클래스 파일에서 Java jar 파일을 만드는 방법을 알아봅니다.
author: dphansen
ms.author: davidph
ms.date: 07/25/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4cec311a28f9d5119b5a0aeb696597e8b34ba25a
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "73588777"
---
# <a name="create-a-java-jar-file-from-class-files"></a>클래스 파일에서 Java jar 파일 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[SQL Server 언어 확장](../language-extensions-overview.md)을 사용하고 Java 코드를 실행할 때 클래스 파일을 jar 파일에 패키징하는 것이 좋습니다.

## <a name="create-a-jar-file"></a>jar 파일 만들기

클래스 파일에서 jar 파일을 만들려면 클래스 파일이 포함된 폴더로 이동하고 다음 명령을 실행합니다.

```cmd
jar -cf <MyJar.jar> *.class
```

`jar.exe` 경로가 시스템 경로 변수의 일부인지 확인합니다. 또는 JDK 폴더의 `/bin` 아래에서 찾을 수 있는 jar 파일 전체 경로를 지정합니다. 예를 들어

```cmd
C:\Users\MyUser\Desktop\jdk1.8.0_201\bin\jar -cf <MyJar.jar> *.class
```

## <a name="next-steps"></a>다음 단계

+ [SQL Server에서 Java를 호출하는 방법](../how-to/call-java-from-sql.md)