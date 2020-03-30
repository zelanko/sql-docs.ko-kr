---
title: 마이그레이션 평가용 PowerShell cmdlet | Microsoft 문서
ms.custom: ''
ms.date: 07/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 117250d3-9982-47fe-94fd-6f29f6159940
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5272203fb1a1c0ac2f755a4da99c654b2595a7f0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68698312"
---
# <a name="powershell-cmdlet-for-migration-evaluation"></a>마이그레이션 평가용 PowerShell cmdlet

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

`Save-SqlMigrationReport` cmdlet은 SQL Server 데이터베이스에서 여러 개체의 마이그레이션 적합성을 평가하는 도구입니다.

현재 이 cmdlet에서는 메모리 내 OLTP에 대한 마이그레이션 적합성만 평가할 수 있습니다. 이 cmdlet은 관리자 권한 Windows PowerShell 환경과 sqlps에서 모두 실행할 수 있습니다.

이 PowerShell cmdlet을 직접 실행하는 대신 SSMS(SQL Server Management Studio)를 사용하여 암시적으로 cmdlet을 실행할 수 있습니다. SSMS **개체 탐색기**에서 테이블을 마우스 오른쪽 단추로 클릭한 다음 **메모리 최적화 관리자**를 클릭할 수 있습니다.

## <a name="syntax"></a>구문

```
Save-SqlMigrationReport
    -FolderPath <output_path>
    [ -MigrationType <migration_scenario_type> ]
    [
        [ -Server <server_name> -Database <database_name>
            [ -Schema <schema_name> ] [ -Object <object_name> ]
        ]
       |
        [ -InputObject <smo_object> ]
    ]
;
```

## <a name="parameters"></a>매개 변수

아래의 표는 매개 변수에 대해 설명합니다.

구문과 관련하여 주의 사항이 있습니다. `-InputObject` 매개 변수를 지정하는 경우 다음 매개 변수를 지정할 수 없습니다.

- `-Server`
- `-Database`
- `-Schema`
- `-Object`

반대로 `-InputObject`를 지정하지 _않으면_`-Server` 및 `-Database`를 지정해야 합니다. `-Server`를 지정하면 `-Schema` 또는 `-Object`나 둘 다를 모두 지정하여 범위를 좁힐 수 있습니다.

| 매개 변수 이름 | Description |
| :------------- | :---------- |
| 데이터베이스 | 대상 SQL Server 데이터베이스의 이름입니다. `-Server`가 필수 항목인 경우 필수입니다.<br/><br/> SQLPS에서는 선택 사항입니다. |
| FolderPath | cmdlet이 생성된 보고서를 저장해야 하는 폴더입니다.<br/><br/> 필수 사항입니다. |
| InputObject | cmdlet의 대상으로 지정해야 하는 SMO 개체입니다.<br/><br/> `-Server` 매개 변수를 제공하지 않는 경우 Windows PowerShell 환경에서 필수 항목입니다.<br/><br/> SQLPS에서는 선택 사항입니다. |
| MigrationType | cmdlet의 대상인 마이그레이션 시나리오의 유형입니다. 현재 이 매개 변수에 사용 가능한 값은 기본 **'OLTP'** 뿐입니다.<br/><br/> (선택 사항) |
| Object | 보고할 개체의 이름입니다. 테이블 또는 저장 프로시저일 수 있습니다. |
| 암호 | `-Username`이 필요한 경우 필요합니다. |
| 스키마 | 보고할 개체를 소유하는 스키마의 이름입니다.<br/><br/> (선택 사항) |
| 서버 | 대상 SQL Server 인스턴스의 이름입니다. `-InputObject` 매개 변수를 제공하지 않는 경우 Windows PowerShell 환경에서 필수 항목입니다.<br/><br/> SQLPS에서는 선택 사항입니다. |
| 사용자 이름 | Windows 인증과 달리 SQL Server 인증을 통해 연결할 때 필요합니다. 이 외에는 생략됩니다. |
| &nbsp; | &nbsp; |

## <a name="prerequisites"></a>사전 요구 사항

이 cmdlet을 실행하려면 먼저 **SqlServer**라는 모듈을 설치해야 합니다.

- `Install-Module -Name SqlServer`

> [!NOTE]
> 이전 `SQLPS` 모듈은 더 이상 유지되지 않습니다. 최신 `SqlServer` 모듈을 사용하세요.

자세한 내용은 [SQL Server PowerShell 모듈 설치](../../powershell/download-sql-server-ps-module.md)를 참조하세요.

## <a name="example-cmdlet-line"></a>예제 cmdlet 줄

다음은 이 문서의 뒷부분에 표시되는 보고서를 생성하기 위해 실행된 실제 cmdlet 줄입니다.

```powershell
Save-SqlMigrationReport `
  -FolderPath 'C:\Test\PowerShell-ps1\Save-SqlMigrationReport\' `
  -Server 'MyUserName123456.database.windows.net' `
  -Database 'MyDatabaseName_31' `
  -Schema 'dbo' `
  -Object 'Table2' `
  -Username 'MyUserName' `
  -Password 'MyPassword' `
  -MigrationType 'OLTP' `
;
```

## <a name="example-output-report"></a>예제 출력 보고서

`-FolderPath` 매개 변수에 지정된 폴더 아래에 이 cmdlet을 실행하여 다음 두 폴더 경로가 생성됩니다. 두 경로는 모두 _server\_name_ 값으로 시작합니다.

- MyDatabaseName_31\Tables\
- MyDatabaseName_31\Stored Procedures\

각 개체 보고서 파일은 해당 폴더 아래에 저장됩니다.

보고서 파일 이름의 확장명은 **.html**입니다. 예를 들어 실제 생성된 파일 이름은 **MigrationAdvisorChecklistReport_Table2_20190728.html**입니다.

HTML은 주로 다음과 같은 헤더가 있는 2열 테이블입니다.

- Description
- 유효성 검사 결과

다음은 한 테이블에 대한 HTML 보고서의 실제 예입니다.

```html
<?xml version="1.0" encoding="utf-8"?>
<html>
  <head>
    <title>Memory optimization checklist for [MyDatabaseName_31].[Table2]</title>
  </head>
  <body>
    <p STYLE="font-family: Verdana, Arial, sans-serif; font-size: 14pt;">
      <b>Memory optimization checklist for [MyDatabaseName_31].[Table2]</b>
    </p>
    <p STYLE="font-family: Verdana, Arial, sans-serif; font-size: 10pt;">
      <b>Report Date/Time:</b>7/28/2019 2:25 PM<br /></p>
    <table border="1" cellpadding="5" cellspacing="0" STYLE="font-family: Verdana, Arial, sans-serif; font-size: 9pt;">
      <tr style="background-color:Silver">
        <th colspan="2" align="center">Description</th>
        <th align="center">Validation Result</th>
      </tr>
      <tr valign="top">
        <td colspan="2">No unsupported data types are defined on this table. </td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top" style="background-color:LightYellow">
        <td colspan="2">No sparse columns are defined for this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top">
        <td colspan="2">No identity columns with unsupported seed and increment are defined for this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top" style="background-color:LightYellow">
        <td colspan="2">No foreign key relationships are defined on this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top">
        <td colspan="2">No unsupported constraints are defined on this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top" style="background-color:LightYellow">
        <td colspan="2">No unsupported indexes are defined on this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top">
        <td colspan="2">No unsupported triggers are defined on this table.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top" style="background-color:LightYellow">
        <td colspan="2">Post migration row size does not exceed the row size limit of memory-optimized tables.</td>
        <td>Succeeded</td>
      </tr>
      <tr valign="top">
        <td colspan="2">Table is not partitioned or replicated.</td>
        <td>Succeeded</td>
      </tr>
    </table>
  </body>
</html>
```

그리고 그 다음은 테이블의 모양에 대한 대략적인 정보입니다.

| Description | 유효성 검사 결과 |
| :---------- | :---------------- |
| 이 테이블에 지원되지 않는 데이터 형식이 정의되지 않았습니다. | 성공 |
| 이 테이블에 스파스 열이 정의되지 않았습니다. | 성공 |
| 이 테이블에 지원되지 않는 시드와 증분을 가진 ID 열이 정의되지 않았습니다. | 성공 |
| 이 테이블에 외래 키 관계가 정의되지 않았습니다. | 성공 |
| 이 테이블에 지원되지 않는 제약 조건이 정의되지 않았습니다. | 성공 |
| 이 테이블에 지원되지 않는 인덱스가 정의되지 않았습니다. | 성공 |
| 이 테이블에 지원되지 않는 트리거가 정의되지 않았습니다. | 성공 |
| 마이그레이션 후 행 크기는 메모리 최적화 테이블의 행 크기 한도를 초과하지 않습니다. | 성공 |
| 테이블이 분할 또는 복제되지 않았습니다. | 성공 |
| &nbsp; | &nbsp; |

## <a name="related-links"></a>관련 링크

- 참조 설명서: [Save-SqlMigrationReport](/powershell/module/sqlserver/save-sqlmigrationreport?view=sqlserver-ps)
