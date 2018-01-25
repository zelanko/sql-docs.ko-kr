---
title: "R 패키지는 SQL Server에 설치 된 확인 | Microsoft Docs"
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: e76a42ead115c8ee4fa89599b192d722ecfbb2ee
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="determine-which-r-packages-are-installed-on-sql-server"></a>R 패키지는 SQL Server에 설치 된 확인

기계 학습 SQL Server에서 R 언어 옵션을 설치 하면 인스턴스에 의해 R 패키지 라이브러리 특별히 사용 하기 위해 만들어집니다. 서버에서 각 인스턴스는 자체 패키지 라이브러리를 있습니다. 패키지 라이브러리 인스턴스 간에 공유할 수 없습니다.

이 문서에서는 특정 SQL Server 인스턴스에 대해 설치 된 R 패키지를 확인 하는 방법을 설명 합니다.

## <a name="generate-r-package-list-using-a-stored-procedure"></a>저장된 프로시저를 사용 하 여 R 패키지 목록 생성

다음 예제에서는 R 함수를 사용 하 여 `installed.packages()` 에 [!INCLUDE [tsql](..\..\includes\tsql-md.md)] 저장 프로시저는 현재 인스턴스에 대 한 R_SERVICES 라이브러리에 설치 된 패키지의 행렬을 가져옵니다. DESCRIPTION 파일의 필드 구문 분석을 방지하기 위해 이름만 반환됩니다.

```SQL
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
NameOnly <- packagematrix[,1];
OutputDataSet <- as.data.frame(NameOnly);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250) ))
```

자세한 선택적에 대 한 정보 및 R 패키지 DESCRIPTION 필드에 대 한 기본 필드를 참조 하세요. [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)합니다.

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>패키지 인스턴스에 설치 되어 있는지 확인 하십시오.

패키지를 설치 하 고 특정 SQL Server 인스턴스를 사용할 수 있는지 확인 하려는 경우에 패키지를 로드 하 고 메시지에만 반환 하려면 다음 저장된 프로시저 호출을 실행할 수 있습니다. 이 예제에서는 찾아서 사용할 수 있는 경우 RevoScaleR 라이브러리를 로드 합니다.

```sql
EXEC sp_execute_external_script  @language =N'R',
@script=N'library("RevoScaleR")'
GO
```

+ 패키지를 찾을 경우 메시지가 반환 됩니다: "명령이 완료 되었습니다."

+ 패키지를 찾거나 로드할 수 없습니다, 하는 경우 텍스트를 포함 하는 오류가 발생 합니다. "라는 'MissingPackageName' 없는 패키지는"

## <a name="get-a-list-of-installed-packages-using-r"></a>R을 사용 하 여 설치 된 패키지 목록 가져오기

R 도구 및 R 함수를 사용하여 여러 가지 방법으로 설치 또는 로드된 패키지 목록을 가져올 수 있습니다. 대부분의 R 개발 도구는 현재 R 작업 영역에서 설치 또는 로드되어 있는 패키지의 목록이나 개체 브라우저를 제공합니다. 이 섹션에서는 sp 또는 모든 R 명령줄에서 사용할 수 있는 몇 가지 간단한 명령\_실행\_외부\_스크립트입니다.

+ 로컬 R 유틸리티를 사용 하 여 기본 R 함수를 같은 `installed.packages()`에 포함 되어 있는 `utils` 패키지 합니다. 인스턴스에 대 한 정확한 목록을 가져오려는 라이브러리 경로 명시적으로 지정 하거나 인스턴스 라이브러리와 연결 된 R 도구를 사용 하 여 해야 합니다.

+ 특정 계산 컨텍스트에서 패키지를 확인 하려면 다음 함수는 RevoScaleR 패키지에서 사용할 수 있습니다. 이러한 함수를 사용 하면 지정 된 계산 컨텍스트에서 패키지를 식별할 수 있습니다.

+ [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxfindpackage)

+ [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinstalledpackages)

예를 들어 지정 된 SQL Server 계산 컨텍스트에서 사용할 수 있는 패키지의 목록을 가져오려면 다음 R 코드를 실행 합니다.

```r
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
sqlPackages
```

## <a name="get-library-location-and-version"></a>가져오기 라이브러리 위치 및 버전

다음 예제에서는 로컬 계산 컨텍스트 및 패키지 버전에서 RevoScaleR의 라이브러리 위치를 가져옵니다.

```r
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

## <a name="determine-path-of-library-used-by-sql-server"></a>SQL Server에서 사용 되는 라이브러리의 경로 확인 합니다.

기계 학습 바인딩을 사용 하 여 구성 요소를 업그레이드 한 경우 경로 R 라이브러리를 변경할 수 있습니다. 이 경우 이전의 바로 가기가 R 도구를 이전 버전을 참조할 수 있습니다. 하도록 하려면 SQL Server에서 사용 하는 경로 패키지 버전의 다음과 같은 명령을 실행할 수 있습니다.

```sql
EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    sql_r_path <- rxSqlLibPaths("local")
      print(sql_r_path)
    version_info <-packageVersion("RevoScaleR")
      print(version_info)'
```

**결과**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```
## <a name="see-also"></a>참고 항목

[SQL Server에 추가 R 패키지를 설치 합니다.](install-additional-r-packages-on-sql-server.md)
