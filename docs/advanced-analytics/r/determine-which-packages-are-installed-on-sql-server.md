---
title: "R 패키지는 SQL Server에 설치 된 확인 | Microsoft Docs"
ms.custom: 
ms.date: 10/09/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 138368a3ca212cb4c176df57d78d02b6f41c4344
ms.contentlocale: ko-kr
ms.lasthandoff: 10/10/2017

---
# <a name="determine-which-r-packages-are-installed-on-sql-server"></a>R 패키지는 SQL Server에 설치 된 확인

기계 학습 SQL Server에서 R 언어 옵션을 설치 하면 설치 프로그램 인스턴스와 연결 된 R 패키지 라이브러리를 만듭니다. 각 인스턴스는 별도 패키지 라이브러리를 갖습니다. 패키지 라이브러리는 **하지** 인스턴스에서 공유 이므로 다른 인스턴스에 설치 될 하도록 다른 패키지에 대 한 합니다.

이 문서에서는 특정 인스턴스에 대해 설치 된 R 패키지를 확인 하는 방법을 설명 합니다.

## <a name="generate-r-package-list-using-a-stored-procedure"></a>저장된 프로시저를 사용 하 여 R 패키지 목록 생성

다음 예제에서는 R 함수를 사용 하 여 `installed.packages()` 에 [!INCLUDE [tsql](..\..\includes\tsql-md.md)] 저장 프로시저는 현재 인스턴스에 대 한 R_SERVICES 라이브러리에 설치 된 패키지의 행렬을 가져옵니다. DESCRIPTION 파일의 필드 구문 분석을 방지하기 위해 이름만 반환됩니다.

```SQL
EXECUTE sp_execute_external_script
@language=N'R'  
,@script = N'str(OutputDataSet);  
packagematrix <- installed.packages();  
NameOnly <- packagematrix[,1];  
OutputDataSet <- as.data.frame(NameOnly);'  
,@input_data_1 = N'SELECT 1 as col'  
WITH RESULT SETS ((PackageName nvarchar(250) ))  
```

자세한 선택적에 대 한 정보 및 R 패키지 DESCRIPTION 파일에 대 한 기본 필드 참조 [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)합니다.

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>패키지 인스턴스에 설치 되어 있는지 확인 하십시오.

패키지를 설치 하 고 특정 SQL Server 인스턴스를 사용할 수 있는지 확인 하려는 경우에 패키지를 로드 하 고 메시지에만 반환 하려면 다음 저장된 프로시저 호출을 실행할 수 있습니다.

```SQL
EXEC sp_execute_external_script  @language =N'R',
@script=N'library("RevoScaleR")'
GO
```

이 예제에서는 찾아서 RevoScaleR 라이브러리를 로드 합니다.

+ 반환 되는 메시지 "명령이 완료 되었습니다." 28gb 해야 패키지를 찾을 경우

+ 다음과 같은 오류가 발생 하는 패키지를 찾거나 로드할 수 없습니다, 하는 경우: "외부 스크립트 오류가 발생 했습니다: library("RevoScaleR")의 오류: 패키지는 없습니다 RevoScaleR 호출"

## <a name="get-a-list-of-installed-packages-using-r"></a>R을 사용 하 여 설치 된 패키지 목록 가져오기

R 도구 및 R 함수를 사용하여 여러 가지 방법으로 설치 또는 로드된 패키지 목록을 가져올 수 있습니다. 대부분의 R 개발 도구는 현재 R 작업 영역에서 설치 또는 로드되어 있는 패키지의 목록이나 개체 브라우저를 제공합니다.

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
## <a name="see-also"></a>참고 항목

[SQL Server에 추가 R 패키지를 설치 합니다.](install-additional-r-packages-on-sql-server.md)

