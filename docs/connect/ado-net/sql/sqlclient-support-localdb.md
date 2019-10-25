---
title: LocalDB에 대한 SqlClient 지원
description: LocalDB 데이터베이스의 SqlClient 지원에 대해 설명 합니다.
ms.date: 08/15/2019
ms.assetid: cf796898-5575-46f2-ae6e-21e5aa8c4123
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 14cbe4ccf227c9462d2a2dc19fb42d913ca7bc5a
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451975"
---
# <a name="sqlclient-support-for-localdb"></a>LocalDB에 대한 SqlClient 지원

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 코드 이름 Denali 부터는 LocalDB 라고 하는 경량 버전의 SQL Server를 사용할 수 있습니다. 이 항목에서는 LocalDB 데이터베이스에 연결 하는 방법에 대해 설명 합니다.  
  
## <a name="remarks"></a>Remarks  
LocalDB 설치 및 LocalDB 인스턴스 구성 방법을 포함하여 LocalDB에 대한 자세한 내용은 SQL Server 온라인 설명서를 참조하세요.  
  
LocalDB로 수행할 수 있는 작업을 요약 하면 다음과 같습니다.  
  
- Sqllocaldb 또는 app.config 파일을 사용 하 여 LocalDB 인스턴스를 만들고 시작 합니다.  
  
- sqlcmd.exe를 사용하여 LocalDB 인스턴스에서 데이터베이스를 추가하고 수정할 수 있습니다. `sqlcmd -S (localdb)\myinst`)을 입력합니다.  
  
- @No__t_0 connection string 키워드를 사용 하 여 데이터베이스를 LocalDB 인스턴스에 추가 합니다. `AttachDBFilename`을 사용할 때 `Database` 연결 문자열 키워드를 사용하여 데이터베이스 이름을 지정하지 않으면 애플리케이션이 닫힐 때 LocalDB 인스턴스에서 데이터베이스가 제거됩니다.  
  
- 연결 문자열에 LocalDB 인스턴스를 지정합니다. 예를 들어, 인스턴스 이름이 `myInstance` 연결 문자열에는 다음이 포함 됩니다.  
  
```console
server=(localdb)\\myInstance  
```  
  
LocalDB 데이터베이스에 연결할 때는 `User Instance=True` 허용 되지 않습니다.  
  
[Microsoft SQL Server 2012 기능 팩](https://www.microsoft.com/download/en/details.aspx?id=29065)에서 LocalDB를 다운로드할 수 있습니다. sqlcmd.exe를 사용하여 LocalDB 인스턴스에서 데이터를 수정할 경우 SQL Server 2012의 sqlcmd가 필요합니다. sqlcmd는 SQL Server 2012 기능 팩에서도 가져올 수 있습니다.  
  
## <a name="programmatically-create-a-named-instance"></a>프로그래밍 방식으로 명명 된 인스턴스 만들기  
응용 프로그램에서는 명명 된 인스턴스를 만들고 다음과 같이 데이터베이스를 지정할 수 있습니다.  
  
- 다음과 같이 app.config 파일에 만들 LocalDB 인스턴스를 지정 합니다.  인스턴스의 버전 번호는 LocalDB 설치의 버전 번호와 동일 해야 합니다.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <configSections>  
        <section  
        name="system.data.localdb"  
        type="System.Data.LocalDBConfigurationSection,System.Data,Version=4.0.0.0,Culture=neutral,PublicKeyToken=b77a5c561934e089"/>  
      </configSections>  
      <system.data.localdb>  
        <localdbinstances>  
          <add name="myInstance" version="11.0" />  
        </localdbinstances>  
      </system.data.localdb>  
    </configuration>  
    ```  
  
- @No__t_0 연결 문자열 키워드를 사용 하 여 인스턴스의 이름을 지정 합니다.  `server` 연결 문자열 키워드에 지정된 인스턴스 이름은 app.config 파일에 지정된 이름과 일치해야 합니다.  
  
- @No__t_0 연결 문자열 키워드를 사용 하 여를 지정 합니다. MDF 파일.  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server 기능 및 ADO.NET](sql-server-features-adonet.md)
