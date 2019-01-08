---
title: GEOMETRY, GEOGRAPHY 및 HIERARCHYID의 클라이언트 쪽 사용에 대 한 경고 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 500ee6b3-2154-45d2-a3cf-8760166d9413
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d9ee14c39f7fee577065de934f839f9d6c88e630
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52413773"
---
# <a name="warning-about-client-side-usage-of-geometry-geography-and-hierarchyid"></a>GEOMETRY, GEOGRAPHY 및 HIERARCHYID의 클라이언트 쪽 사용에 대한 경고
  공간 데이터 형식을 포함하는 **Microsoft.SqlServer.Types.dll**어셈블리가 버전 10.0에서 버전 11.0으로 업그레이드되었습니다. 이 어셈블리를 참조하는 사용자 지정 애플리케이션에서는 특정 조건에 해당될 때 오류가 발생할 수 있습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 공간 데이터 형식을 포함하는 **Microsoft.SqlServer.Types.dll**어셈블리가 버전 10.0에서 버전 11.0으로 업그레이드되었습니다. 이 어셈블리를 참조하는 사용자 지정 애플리케이션에서는 다음 조건에 해당될 때 오류가 발생할 수 있습니다.  
  
-   컴퓨터에서 사용자 지정 응용 프로그램을 이동 하는 경우 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 만 있는 컴퓨터에 설치 된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 가 설치 된 응용 프로그램 실패로 인해의 참조 된 버전 10.0 합니다 **SqlTypes** 어셈블리 존재 하지 않습니다. `"Could not load file or assembly 'Microsoft.SqlServer.Types, Version=10.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. The system cannot find the file specified."`라는 오류 메시지가 나타날 수 있습니다.  
  
-   참조 하는 경우는 **SqlTypes** 어셈블리 버전 11.0 버전 10.0도 설치 되 고이 오류 메시지가 표시 될 수 있습니다. `"System.InvalidCastException: Unable to cast object of type 'Microsoft.SqlServer.Types.SqlGeometry' to type 'Microsoft.SqlServer.Types.SqlGeometry'."`  
  
-   .NET 3.5, 4 또는 4.5를 대상으로 하는 사용자 지정 애플리케이션에서 **SqlTypes** 어셈블리 버전 11.0을 참조하는 경우 SqlClient는 기본적으로 이 어셈블리의 버전 10.0을 로드하므로 애플리케이션 오류가 발생합니다. 이 오류는 애플리케이션이 다음 메서드 중 하나를 호출할 때 발생합니다.  
  
    -   `GetValue` 클래스의 `SqlDataReader` 메서드  
  
    -   `GetValues` 클래스의 `SqlDataReader` 메서드  
  
    -   `SqlDataReader` 클래스의 대괄호 인덱스 연산자 []  
  
    -   `ExecuteScalar` 클래스의 `SqlCommand` 메서드  
  
## <a name="corrective-action"></a>수정 동작  
 다음 메서드 중 하나를 사용하여 이 문제를 해결할 수 있습니다.  
  
-   코드에서 위에 나열된 Get 메서드 대신 다음 예와 같이 CLR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 형식을 검색하는 `GetSqlBytes` 메서드를 호출하여 이 문제를 해결할 수 있습니다.  
  
    ```csharp  
    string query = "SELECT [SpatialColumn] FROM [SpatialTable]";  
          using (SqlConnection conn = new SqlConnection("..."))  
          {  
                SqlCommand cmd = new SqlCommand(query, conn);  
  
                conn.Open();  
                SqlDataReader reader = cmd.ExecuteReader();  
  
                while (reader.Read())  
                {  
                      // In version 11.0 only  
                      SqlGeometry g =   
    SqlGeometry.Deserialize(reader.GetSqlBytes(0));  
  
                      // In version 10.0 or 11.0  
                      SqlGeometry g2 = new SqlGeometry();  
                      g.Read(new BinaryReader(reader.GetSqlBytes(0).Stream));  
                }  
          }  
    ```  
  
-   다음 예와 같이 애플리케이션 구성 파일에 어셈블리 리디렉션을 사용하여 이 문제를 해결할 수 있습니다.  
  
    ```xml  
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
        ...  
        <dependentAssembly>  
            <assemblyIdentity name="Microsoft.SqlServer.Types" publicKeyToken="89845dcd8080cc91" culture="neutral" />  
            <bindingRedirect oldVersion="10.0.0.0" newVersion="11.0.0.0" />  
        </dependentAssembly>  
        ...  
    </assemblyBinding>  
    ```  
  
-   SqlClient가 어셈블리의 버전 11.0을 로드하도록 연결 문자열에서 "Type System Version" 특성에 대해 "SQL Server 2012" 값을 지정하여 이 문제를 해결할 수 있습니다. 이 연결 문자열 특성은 .NET 4.5 이상에서만 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
