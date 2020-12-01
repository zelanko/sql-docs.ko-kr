---
title: 연결 문자열 빌더
description: ADO.NET의 여러 공급자에 사용되는 연결 문자열 작성기 클래스에 대해 알아봅니다. 이 클래스는 모두 DbConnectionStringBuilder에서 상속됩니다.
ms.date: 11/13/2020
dev_langs:
- csharp
ms.assetid: 8434b608-c4d3-43d3-8ae3-6d8c6b726759
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 74031c0c3711ce768b919692fde0cb687060f227
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126516"
---
# <a name="connection-string-builders"></a>연결 문자열 빌더

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

이전 버전의 ADO.NET에서는 연결된 문자열 값이 있는 연결 문자열의 컴파일 시간 검사가 발생하지 않았으므로 런타임에 잘못된 키워드가 <xref:System.ArgumentException>을 생성했습니다. Microsoft SqlClient Data Provider for SQL Server에는 <xref:System.Data.Common.DbConnectionStringBuilder>에서 상속하는 강력한 유형의 연결 문자열 작성기 클래스 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder?displayProperty=nameWithType>이 포함되어 있습니다.

## <a name="connection-string-injection-attacks"></a>연결 문자열 삽입 공격

연결 문자열 삽입 공격은 사용자 입력에 대해 동적 문자열 연결을 사용하여 연결 문자열을 작성할 때 발생할 수 있습니다. 문자열의 유효성이 확인되지 않고 악의적인 텍스트 또는 문자를 이스케이프할 수 없는 경우 공격자가 서버에서 중요한 데이터 또는 기타 리소스에 액세스할 가능성이 있습니다. 예를 들어 공격자가 세미콜론을 입력한 다음 값을 추가하여 공격을 시작할 수 있습니다. 연결 문자열은 "**최신항목 사용(last one wins)** " 알고리즘을 사용하여 구문 분석되고 악의적인 입력이 적법한 값으로 대체됩니다.

연결 문자열 작성기 클래스는 모호한 작업을 제거하고 구문 오류 및 보안 취약점으로부터 보호하도록 디자인되었습니다. 데이터 공급자가 허용하는 알려진 키/값 쌍에 해당하는 메서드와 속성을 제공합니다. 각 클래스는 고정된 동의어 컬렉션을 유지하며 동의어를 그에 해당하는 잘 알려진 키 이름으로 변환할 수 있습니다. 또한, 유효한 키/값 쌍에 대한 검사를 수행하며 유효하지 않은 쌍이 있는 경우 예외를 throw합니다. 뿐만 아니라 삽입된 값을 안전한 방식으로 처리합니다.

다음 예제에서는 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder>에서 `Initial Catalog` 설정에 삽입된 추가 값을 처리하는 방법을 보여 줍니다.

[!code-csharp[SqlConnectionStringBuilder_InjectionAttack#1](~/../sqlclient/doc/samples/SqlConnectionStringBuilder_InjectionAttack.cs#1)]

출력은 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder>에서 추가 값을 새 키/값 쌍으로 연결 문자열에 추가하는 대신 큰 따옴표로 이스케이프하여 올바르게 처리했음을 보여줍니다.

```output
data source=(local);Integrated Security=True;
initial catalog="AdventureWorks;NewValue=Bad"
```

## <a name="building-connection-strings-from-configuration-files"></a>구성 파일에서 연결 문자열 작성

연결 문자열의 특정 요소가 이미 알려져 있는 경우 해당 요소를 구성 파일에 저장하고 런타임에 검색하여 완전한 연결 문자열을 구성할 수 있습니다. 예를 들어 데이터베이스 이름은 미리 알고 있는 경우가 많지만 서버 이름은 그렇지 않습니다. 또는 연결 문자열에 다른 값을 삽입할 수 없도록 런타임에 사용자가 이름과 암호를 입력하도록 할 수도 있습니다.

연결 문자열 작성기의 오버로드된 생성자 중 하나는 <xref:System.String>을 인수로 사용하므로 작성기를 사용하면 부분 연결 문자열을 제공하여 이러한 사용자 입력을 통해 연결 문자열을 완성하는 것이 가능합니다. 이 부분 연결 문자열을 구성 파일에 저장한 후 런타임에 검색할 수 있습니다.

> [!NOTE]
> <xref:System.Configuration> 네임스페이스를 사용하면 <xref:System.Web.Configuration.WebConfigurationManager>(웹 애플리케이션의 경우) 및 <xref:System.Configuration.ConfigurationManager>(Windows 애플리케이션의 경우)를 통해 구성 파일에 프로그래밍 방식으로 액세스할 수 있습니다. 연결 문자열 및 구성 파일 작업에 대한 자세한 내용은 [연결 문자열 및 구성 파일](connection-strings-and-configuration-files.md)을 참조하세요.

### <a name="example"></a>예제

이 예제에서는 구성 파일에서 부분 연결 문자열을 검색한 후 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.DataSource%2A>의 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.UserID%2A>, <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.Password%2A> 및 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> 속성을 설정하여 완성하는 방법을 보여 줍니다. 구성 파일은 다음과 같이 정의됩니다.

```xml
<connectionStrings>
  <clear/>
  <add name="partialConnectString"
    connectionString="Initial Catalog=Northwind;"
    providerName="Microsoft.Data.SqlClient" />
</connectionStrings>
```

> [!NOTE]
> 코드를 실행하려면 프로젝트에서 `System.Configuration.dll`에 대한 참조를 설정해야 합니다.

[!code-csharp[DataWorks SqlConnectionStringBuilder.UserNamePwd#1](~/../sqlclient/doc/samples/SqlConnectionStringBuilder_UserNamePwd.cs#1)]
  
## <a name="see-also"></a>참고 항목

- [연결 문자열](connection-strings.md)
