---
title: SQL Server on Linuxr로 데이터 대량 복사
description: 이 문서에서는 bcp 유틸리티에 대해 설명합니다. bcp를 사용하여 다수의 행을 SQL Server 테이블로 가져오거나 SQL Server 테이블에서 데이터 파일로 데이터를 내보낼 수 있습니다.
author: VanMSFT
ms.author: vanto
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 7b93d0d7-7946-4b78-b33a-57d6307cdfa9
ms.openlocfilehash: 447304bf0927b08e76a668e93ca750f3f8bfc779
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896279"
---
# <a name="bulk-copy-data-with-bcp-to-sql-server-on-linux"></a>bcp를 사용하여 SQL Server on Linux로 데이터 대량 복사

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 [bcp](../tools/bcp-utility.md) 명령줄 유틸리티를 사용하여 SQL Server on Linux 인스턴스와 사용자 지정 형식의 데이터 파일 간에 데이터를 대량 복사하는 방법을 보여 줍니다.

`bcp`를 사용하여 다수의 행을 SQL Server 테이블로 가져오거나 SQL Server 테이블에서 데이터 파일로 데이터를 내보낼 수 있습니다. queryout 옵션과 함께 사용하는 경우를 제외하고 `bcp`에는 Transact-SQL 지식이 필요하지 않습니다. `bcp` 명령줄 유틸리티는 Linux, Windows 또는 Docker에서 온-프레미스 또는 클라우드로 실행되는 Microsoft SQL Server와 Azure SQL Database 및 Azure SQL Data Warehouse에서 작동합니다.

이 아티클에서는 다음을 수행하는 방법을 보여줍니다.
- `bcp in` 명령을 사용하여 테이블로 데이터 가져오기
- `bcp out` 명령을 사용하여 테이블에서 데이터 내보내기

## <a name="install-the-sql-server-command-line-tools"></a>SQL Server 명령줄 도구 설치

`bcp`는 SQL Server on Linux와 함께 자동으로 설치되지 않는 SQL Server 명령줄 도구의 일부입니다. Linux 머신에 SQL Server 명령줄 도구를 아직 설치하지 않은 경우 설치해야 합니다. 도구 설치 방법에 대한 자세한 내용을 보려면 다음 목록에서 해당 Linux 배포를 선택합니다.

- [Red Hat Enterprise Linux(RHEL)](sql-server-linux-setup-tools.md#RHEL)
- [Ubuntu](sql-server-linux-setup-tools.md#ubuntu)
- [SUSE Linux Enterprise Server(SLES)](sql-server-linux-setup-tools.md#SLES)

## <a name="import-data-with-bcp"></a>bcp를 사용하여 데이터 가져오기

이 자습서에서는 로컬 SQL Server 인스턴스(**localhost**)에서 샘플 데이터베이스 및 테이블을 만든 다음, `bcp`를 사용하여 디스크의 텍스트 파일에서 샘플 테이블로 로드합니다.

### <a name="create-a-sample-database-and-table"></a>샘플 데이터베이스 및 테이블 만들기

먼저 이 자습서의 나머지 부분에서 사용되는 간단한 테이블로 샘플 데이터베이스를 만들겠습니다.

1. Linux 상자에서 명령 터미널을 엽니다.

2. 다음 명령을 복사하여 터미널 창에 붙여넣습니다. 이 명령은 **sqlcmd** 명령줄 유틸리티를 사용하여 로컬 SQL Server 인스턴스(**localhost**)에 샘플 데이터베이스(**BcpSampleDB**) 및 테이블(**TestEmployees**)을 만듭니다. 필요한 경우, 명령을 실행하기 전에 `username` 및 `<your_password>`를 바꾸어야 합니다.

**BcpSampleDB** 데이터베이스를 만듭니다.
```bash 
sqlcmd -S localhost -U sa -P <your_password> -Q "CREATE DATABASE BcpSampleDB;"
```
**BcpSampleDB** 데이터베이스에 **TestEmployees** 테이블을 만듭니다.
```bash 
sqlcmd -S localhost -U sa -P <your_password> -d BcpSampleDB -Q "CREATE TABLE TestEmployees (Id INT IDENTITY(1,1) NOT NULL PRIMARY KEY, Name NVARCHAR(50), Location NVARCHAR(50));"
```
### <a name="create-the-source-data-file"></a>원본 데이터 파일 만들기
다음 명령을 복사하여 터미널 창에 붙여넣습니다. 기본 제공 `cat` 명령을 사용하여 레코드 3개가 포함된 샘플 텍스트 데이터 파일을 만들고, 홈 디렉터리에 파일을 **~/test_data.txt**로 저장합니다. 레코드의 필드는 쉼표로 구분됩니다.

```bash
cat > ~/test_data.txt << EOF
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
EOF
```

터미널 창에서 다음 명령을 실행하면 데이터 파일이 올바르게 만들어졌는지 확인할 수 있습니다.
```bash 
cat ~/test_data.txt
```

터미널 창에 다음과 같이 표시되어야 합니다.
```bash
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

### <a name="import-data-from-the-source-data-file"></a>원본 데이터 파일에서 데이터 가져오기
다음 명령을 복사하여 터미널 창에 붙여넣습니다. 이 명령은 `bcp`를 사용하여 로컬 SQL Server 인스턴스(**localhost**)에 연결하고 데이터 파일( **~/test_data.txt**)에서 데이터베이스(**BcpSampleDB**)의 테이블(**TestEmployees**)로 데이터를 가져옵니다. 필요한 경우, 명령을 실행하기 전에 username 및 `<your_password>`를 바꾸어야 합니다.

```bash 
bcp TestEmployees in ~/test_data.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t  ','
```

다음은 이 예제에서 `bcp`와 함께 사용한 명령줄 매개 변수에 대한 간략한 개요입니다.
- `-S`: 연결할 SQL Server 인스턴스를 지정합니다.
- `-U`: SQL Server에 연결하는 데 사용되는 로그인 ID를 지정합니다.
- `-P`: 로그인 ID의 암호를 지정합니다.
- `-d`: 연결할 데이터베이스를 지정합니다.
- `-c`: 문자 데이터 형식을 사용하여 작업을 수행합니다.
- `-t`: 필드 종결자를 지정합니다. 데이터 파일에서 레코드의 필드 종결자로 `comma`를 사용하고 있습니다.

> [!NOTE]
> 이 예제에서는 사용자 지정 행 종결자를 지정하지 않습니다. 앞에서 `cat` 명령을 사용하여 데이터 파일을 만들 때 텍스트 데이터 파일의 행이 `newline`으로 올바르게 종결되었습니다.

터미널 창에서 다음 명령을 실행하면 데이터를 성공적으로 가져왔는지 확인할 수 있습니다. 필요한 경우, 명령을 실행하기 전에 `username` 및 `<your_password>`를 바꾸어야 합니다.
```bash 
sqlcmd -S localhost -d BcpSampleDB -U sa -P <your_password> -I -Q "SELECT * FROM TestEmployees;"
```

다음과 같은 결과가 표시되어야 합니다.
```bash
Id          Name                Location
----------- ------------------- -------------------
          1 Jared               Australia
          2 Nikita              India
          3 Tom                 Germany

(3 rows affected)
```

## <a name="export-data-with-bcp"></a>bcp를 사용하여 데이터 내보내기

이 자습서에서는 `bcp`를 사용하여 앞서 만든 샘플 테이블에서 새 데이터 파일로 데이터를 내보냅니다.

다음 명령을 복사하여 터미널 창에 붙여넣습니다. 이 명령은 `bcp` 명령줄 유틸리티를 사용하여 **BcpSampleDB** 데이터베이스의 **TestEmployees** 테이블에서 **~/test_export.txt**라는 새 데이터 파일로 데이터를 내보냅니다.  필요한 경우, 명령을 실행하기 전에 username 및 `<your_password>`를 바꾸어야 합니다.

```bash 
bcp TestEmployees out ~/test_export.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t ','
```

터미널 창에서 다음 명령을 실행하면 데이터를 올바르게 내보냈는지 확인할 수 있습니다.
```bash 
cat ~/test_export.txt
```

터미널 창에 다음과 같이 표시되어야 합니다.
```
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

## <a name="see-also"></a>참고 항목
- [bcp 유틸리티](../tools/bcp-utility.md)
- [bcp 사용 시 데이터 형식의 호환성](../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)
- [BULK INSERT를 사용하여 대량 데이터 가져오기](../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
- [BULK INSERT(Transact-SQL)](../t-sql/statements/bulk-insert-transact-sql.md)
