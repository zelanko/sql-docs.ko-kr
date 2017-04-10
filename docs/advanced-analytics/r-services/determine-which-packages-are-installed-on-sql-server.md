---
title: "SQL Server에 설치된 패키지 확인 | Microsoft Docs"
ms.custom: ""
ms.date: "08/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# SQL Server에 설치된 패키지 확인
  이 항목에는 R 패키지도 설치를 확인 하는 방법을 설명의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스.  
  
기본적으로 설치 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 각 인스턴스에 연결 하는 R 패키지 라이브러리를 만듭니다. 따라서 어떤 패키지가 컴퓨터에 설치 된 알아야 R 서비스를 설치한 별도 각 인스턴스에이 쿼리를 실행 해야 하면. 패키지 라이브러리는 **하지** 인스턴스에서 공유, 이므로 각각 다른 패키지를 다른 인스턴스에 설치 될 수 있습니다.

인스턴스에 대 한 기본 라이브러리 위치를 결정 하는 방법에 대 한 정보를 참조 하십시오. [설치 및 관리 하는 R 패키지](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)합니다.   
   
 
## R을 사용 하 여 설치 된 패키지 목록을 가져오려면  
 여러 가지 방법으로 R 도구 및 R 함수를 사용 하 여 설치 또는 로드 된 패키지의 목록을 가져올 수 있습니다.  
  
+   대부분의 R 개발 도구는 현재 R 작업 영역에서 설치 또는 로드되어 있는 패키지의 목록이나 개체 브라우저를 제공합니다.  

+ 패키지 관리를 위해 특별히 제공 되는 RevoScaleR 패키지에서 다음 함수는 컨텍스트를 계산 하는 것이 좋습니다.
  - [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/rxfindpackage)
  - [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/rxInstalledPackages)   
  
+   설치된 `installed.packages()`패키지에 포함되어 있는 `utils` 등의 R 함수를 사용할 수 있습니다. 함수는 지정 된 라이브러리에 패키지 이름, 라이브러리 경로 및 버전 번호의 행렬을 반환 하는 각 패키지의 설명 파일을 검색 합니다.  
 
### 예  
다음 예제에서는 함수를 사용 하 여 `rxInstalledPackages` 은 제공 된 SQL Server 계산 컨텍스트에서 사용할 수 있는 패키지의 목록을 가져올 수 있습니다.

~~~~
sqlServerCompute <- RxInSqlServer(connectionString = 
"Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
     sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
     sqlPackages
~~~~

 다음 예제에서는 기본 R 함수를 사용 하 여 `installed.packages()` 에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 현재 인스턴스에 대 한 R_SERVICES 라이브러리에 설치 된 패키지의 행렬을 가져옵니다. DESCRIPTION 파일의 필드 구문 분석을 방지하기 위해 이름만 반환됩니다.  
  
```  
EXECUTE sp_execute_external_script  
@language=N'R'  
,@script = N'str(OutputDataSet);  
packagematrix <- installed.packages();  
NameOnly <- packagematrix[,1];  
OutputDataSet <- as.data.frame(NameOnly);'  
,@input_data_1 = N'SELECT 1 as col'  
WITH RESULT SETS ((PackageName nvarchar(250) ))  
```  
  
 기본 및 R 패키지 설명 파일에 선택적 필드에 대 한 자세한 내용은 참조 [https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file](https://cran.r-project.org/doc/manuals/R-exts.html)합니다.  
  
## 참고 항목  
 [SQL Server에 추가 R 패키지 설치](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
  