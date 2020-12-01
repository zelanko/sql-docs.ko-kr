---
title: 연결 문자열
description: 데이터 공급자에서 데이터 원본으로 매개 변수로 전달되는 초기화 정보가 포함된 Microsoft SqlClient Data Provider for SQL Server의 연결 문자열에 대해 알아봅니다.
ms.date: 11/13/2020
ms.assetid: 745c5f95-2f02-4674-b378-6d51a7ec2490
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: e37d77304644d1adb50bb195dd32d4c4e1222c09
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126498"
---
# <a name="connection-strings-in-adonet"></a>ADO.NET의 연결 문자열

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

연결 문자열에는 데이터 공급자에서 데이터 소스에 매개 변수로 전달되는 초기화 정보가 있습니다. 데이터 공급자는 연결 문자열을 <xref:System.Data.Common.DbConnection.ConnectionString?displayProperty=nameWithType> 속성 값으로 받습니다. 공급자는 연결 문자열을 구문 분석하고 구문이 정확하고 키워드가 지원되는지 확인합니다. 그런 다음 <xref:System.Data.Common.DbConnection.Open?displayProperty=nameWithType> 메서드는 구문 분석된 연결 매개 변수를 데이터 원본에 전달합니다. 데이터 원본에서는 추가 유효성 검사를 수행하고 연결을 설정합니다.

## <a name="connection-string-syntax"></a>연결 문자열 구문

연결 문자열은 키/값 매개 변수 쌍의 세미콜론으로 구분된 목록입니다.

```csharp
keyword1=value; keyword2=value;
```

키워드는 대/소문자를 구분하지 않습니다. 그러나 값은 데이터 원본에 따라 대/소문자를 구분할 수 있습니다. 키워드와 값 모두 [공백 문자](https://en.wikipedia.org/wiki/Whitespace_character#Unicode)를 포함할 수 있습니다. 선행 및 후행 공백은 키워드 및 따옴표가 없는 값에서 무시됩니다.

값에 세미콜론, [유니코드 제어 문자](https://en.wikipedia.org/wiki/Unicode_control_characters) 또는 선행/후행 공백이 포함된 경우 작은따옴표 또는 큰따옴표로 묶어야 합니다. 예를 들면 다음과 같습니다.

```csharp
Keyword=" whitespace  ";
Keyword='special;character';
```

묶는 문자는 포함하는 값 내에 있으면 안 됩니다. 따라서 작은따옴표를 포함하는 값은 큰따옴표로만 묶을 수 있으며 그 반대의 경우도 마찬가지입니다.

```csharp
Keyword='double"quotation;mark';
Keyword="single'quotation;mark";
```

두 개 문자를 함께 사용하여 바깥쪽 문자를 이스케이프할 수도 있습니다.

```csharp
Keyword="double""quotation";
Keyword='single''quotation';
```

따옴표 자체와 등호는 이스케이프를 요구하지 않으므로 다음 연결 문자열을 사용할 수 있습니다.

```csharp
Keyword=no "escaping" 'required';
Keyword=a=b=c
```

다음 세미콜론 또는 문자열 끝까지 각 값을 읽기 때문에 두 번째 예제의 값은 `a=b=c`가 되며 최종 세미콜론은 선택 사항입니다.

모든 연결 문자열은 위에서 설명한 것과 동일한 기본 구문을 공유합니다. 인식되는 키워드 집합은 공급자에 따라 달라집니다. *Microsoft SqlClient* Data Provider for *SQL Server* 는 이전 API의 많은 키워드를 지원하지만 일반적으로 더 유연하고 많은 공통 연결 문자열 키워드에 대한 동의어를 허용합니다.

실수로 입력하면 오류가 발생할 수 있습니다. 예를 들어 `Integrated Security=true`는 유효하지만 `IntegratedSecurity=true`는 오류를 일으킵니다.

검증되지 않은 사용자 입력으로부터 런타임에 수동으로 생성된 연결 문자열은 문자열 삽입 공격에 취약하고 데이터 원본의 보안을 위협합니다. 이러한 문제를 해결하기 위해 [연결 문자열 작성기](connection-string-builders.md)를 만들었습니다. 이 연결 문자열 작성기는 매개 변수를 강력한 형식의 속성으로 노출하고 데이터 원본으로 전송되기 전에 연결 문자열의 유효성을 검사할 수 있도록 합니다.

## <a name="in-this-section"></a>섹션 내용

[연결 문자열 작성기](connection-string-builders.md)\
`ConnectionStringBuilder` 클래스를 사용하여 런타임에 유효한 연결 문자열을 생성하는 방법을 보여줍니다.

[연결 문자열 및 구성 파일](connection-strings-and-configuration-files.md)\
구성 파일에서 연결 문자열을 저장하고 검색하는 방법을 보여 줍니다.

[연결 문자열 구문](connection-string-syntax.md)\
`SqlClient`에 대한 공급자별 연결 문자열을 구성하는 방법을 설명합니다.

[연결 정보 보호](protecting-connection-information.md)\
데이터 소스 연결에 사용되는 정보를 보호하는 기법을 보여 줍니다.
