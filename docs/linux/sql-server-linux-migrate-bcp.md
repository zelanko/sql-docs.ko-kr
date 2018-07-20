---
title: 대량으로 Linux에서 SQL Server로 데이터 복사 | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 7b93d0d7-7946-4b78-b33a-57d6307cdfa9
ms.openlocfilehash: 3542ee739d2c5e47a2203b8c2eed9d243f0cb5d8
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086475"
---
# <a name="bulk-copy-data-with-bcp-to-sql-server-on-linux"></a>Linux의 SQL Server bcp 사용 하 여 데이터 대량 복사

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 사용 하는 방법을 보여 줍니다.는 [bcp](../tools/bcp-utility.md) 명령줄 유틸리티를 Linux의 SQL Server 2017 인스턴스와 사용자가 지정한 형식의 데이터 파일 간에 데이터를 대량 복사 합니다.

사용할 수 있습니다 `bcp` 를 SQL Server 테이블로 많은 수의 행을 가져올 수 또는 SQL Server 테이블에서 데이터 파일로 데이터를 내보냅니다. Queryout 옵션을 사용 하는 경우를 제외 하 고 `bcp` transact-sql 지식이 없어도 됩니다. `bcp` 명령줄 유틸리티는 Linux, Windows 나 Docker 및 Azure SQL Database 및 Azure SQL Data Warehouse에서 클라우드 또는 온-프레미스를 실행 중인 Microsoft SQL Server를 사용 하 여 작동 합니다.

이 아티클에서는 다음을 수행하는 방법을 보여줍니다.
- 사용 하 여 테이블 데이터 가져오기는 `bcp in` 명령
- 사용 하 여 테이블에서 데이터 내보내기는 `bcp out` 명령

## <a name="install-the-sql-server-command-line-tools"></a>SQL Server 명령줄 도구 설치

`bcp` Linux의 SQL Server를 사용 하 여 자동으로 설치 되어 있지 않은 SQL Server 명령줄 도구를의 부분이입니다. Linux 컴퓨터에 SQL Server 명령줄 도구를 이미 설치 되지 않은 경우 설치 해야 합니다. 도구를 설치 하는 방법에 대 한 자세한 내용은 다음 목록에서 Linux 배포를 선택 합니다.

- [Red Hat Enterprise Linux(RHEL)](sql-server-linux-setup-tools.md#RHEL)
- [Ubuntu](sql-server-linux-setup-tools.md#ubuntu)
- [SUSE Linux Enterprise Server(SLES)](sql-server-linux-setup-tools.md#SLES)

## <a name="import-data-with-bcp"></a>Bcp 사용 하 여 데이터 가져오기

이 자습서에서 만든 예제 데이터베이스 및 테이블을 로컬 SQL Server 인스턴스에서 (**localhost**) 사용 하 여 `bcp` 디스크에 있는 텍스트 파일에서 예제 테이블로 로드 합니다.

### <a name="create-a-sample-database-and-table"></a>예제 데이터베이스 및 테이블 만들기

이 자습서의 나머지 부분에 사용 되는 간단한 테이블을 사용 하 여 샘플 데이터베이스를 만들어 보겠습니다.

1. Linux 상자에서 명령을 터미널을 엽니다.

2. 복사 하 고 터미널 창에서 다음 명령을 붙여넣습니다. 다음이 명령을 사용 합니다 **sqlcmd** 샘플 데이터베이스를 만들려면 명령줄 유틸리티 (**BcpSampleDB**) 및 테이블 (**TestEmployees**) 인스턴스에서 로컬 SQL Server (**localhost**). 교체 해야 합니다 `username` 및 `<your_password>` 명령을 실행 하기 전에 필요에 따라 합니다.

데이터베이스를 만듭니다 **BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -Q "CREATE DATABASE BcpSampleDB;"
```
테이블을 만듭니다 **TestEmployees** 데이터베이스의 **BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -d BcpSampleDB -Q "CREATE TABLE TestEmployees (Id INT IDENTITY(1,1) NOT NULL PRIMARY KEY, Name NVARCHAR(50), Location NVARCHAR(50));"
```
### <a name="create-the-source-data-file"></a>원본 데이터 파일 만들기
복사 하 고 터미널 창에서 다음 명령을 붙여넣습니다. 기본 제공 사용 `cat` 으로 홈 디렉터리에 파일을 저장 하는 세 개의 레코드를 사용 하 여 샘플 텍스트 데이터 파일을 만들려면 명령 **~/test_data.txt**합니다. 레코드의 필드는 쉼표로 구분 됩니다.

```bash
cat > ~/test_data.txt << EOF
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
EOF
```

터미널 창에서 다음 명령을 실행 하 여 데이터 파일을 제대로 만든 것을 확인할 수 있습니다.
```bash 
cat ~/test_data.txt
```

이 다음 터미널 창에서 표시할 수 있습니다.
```bash
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

### <a name="import-data-from-the-source-data-file"></a>원본 데이터 파일에서 데이터 가져오기
복사 하 고 터미널 창에서 다음 명령을 붙여넣습니다. 이 명령은 `bcp` 로컬 SQL Server 인스턴스에 연결 하려면 (**localhost**) 및 데이터 파일에서 데이터 가져오기 (**~/test_data.txt**) 테이블로 (**TestEmployees** ) 데이터베이스에서 (**BcpSampleDB**). 사용자 이름으로 바꿔야 하 고 `<your_password>` 명령을 실행 하기 전에 필요에 따라 합니다.

```bash 
bcp TestEmployees in ~/test_data.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t  ','
```

다음은 명령줄 매개 변수를 사용 했습니다 간략 한 개요 `bcp` 이 예제에서:
- `-S`: 연결할 SQL Server의 인스턴스를 지정 합니다.
- `-U`: SQL Server에 연결할 때 사용할 ID의 로그인을 지정
- `-P`: 로그인 ID에 대 한 암호를 지정 합니다.
- `-d`: 연결할 데이터베이스를 지정 합니다.
- `-c`: 문자 데이터 형식을 사용 하 여 작업을 수행 합니다.
- `-t`: 필드 종결자를 지정 합니다. 사용 하 여 `comma` 데이터 파일에 있는 레코드를 필드 종결자로

> [!NOTE]
> 이 예제의 사용자 지정 행 종결자를 지정 하지 않는 것입니다. 텍스트 데이터 파일의 행으로 올바르게 종료 되었습니다 `newline` 우리가 사용 하는 경우는 `cat` 이전 데이터 파일을 만드는 명령입니다.

터미널 창에서 다음 명령을 실행 하 여 성공적으로 데이터를 가져왔는지 확인할 수 있습니다. 교체 해야 합니다 `username` 및 `<your_password>` 명령을 실행 하기 전에 필요에 따라 합니다.
```bash 
sqlcmd -S localhost -d BcpSampleDB -U sa -P <your_password> -I -Q "SELECT * FROM TestEmployees;"
```

그러면 다음과 같은 결과가 표시 됩니다.
```bash
Id          Name                Location
----------- ------------------- -------------------
          1 Jared               Australia
          2 Nikita              India
          3 Tom                 Germany

(3 rows affected)
```

## <a name="export-data-with-bcp"></a>Bcp 사용 하 여 데이터 내보내기

이 자습서를 사용 하 여 `bcp` 새 데이터 파일에 앞에서 만든 샘플 테이블에서 데이터 내보내기.

복사 하 고 터미널 창에서 다음 명령을 붙여넣습니다. 이러한 명령을 사용 합니다 `bcp` 테이블에서 데이터를 내보내려면 명령줄 유틸리티 **TestEmployees** 데이터베이스의 **BcpSampleDB** 라는 새 데이터 파일로 **~/test_export.txt** .  사용자 이름으로 바꿔야 하 고 `<your_password>` 명령을 실행 하기 전에 필요에 따라 합니다.

```bash 
bcp TestEmployees out ~/test_export.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t ','
```

터미널 창에서 다음 명령을 실행 하 여 데이터를 올바르게 내보냈는지 확인할 수 있습니다.
```bash 
cat ~/test_export.txt
```

이 다음 터미널 창에서 표시할 수 있습니다.
```
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

## <a name="see-also"></a>참고자료
- [bcp 유틸리티](../tools/bcp-utility.md)
- [Bcp를 사용 하는 경우 호환성에 대 한 데이터 형식](../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)
- [BULK INSERT를 사용 하 여 데이터 대량 가져오기](../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
- [BULK INSERT (TRANSACT-SQL)](../t-sql/statements/bulk-insert-transact-sql.md)
