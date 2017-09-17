---
title: "SQL Server에 설치된 패키지 확인 | Microsoft 문서"
ms.custom: 
ms.date: 08/31/2016
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
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 90e7146bde123ca8ac8a8e6ff3e11d212fd4a35a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="determine-which-packages-are-installed-on-sql-server"></a>SQL Server에 설치된 패키지 확인
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 설치된 R 패키지를 확인하는 방법을 설명합니다.  
  
기본적으로 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 설치는 각 인스턴스와 연결된 R 패키지 라이브러리를 만듭니다. 따라서 컴퓨터에 설치된 패키지를 확인하려면 R Services가 설치된 각 별도 인스턴스에서 이 쿼리를 실행해야 합니다. 패키지 라이브러리는 인스턴스 간에 공유되지 **않으므로** 각각 다른 인스턴스에 패키지를 설치할 수 있습니다.

인스턴스의 기본 라이브러리 위치를 확인하는 방법에 대한 자세한 내용은 [R 패키지 설치 및 관리](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)를 참조하세요.   
   
 
## <a name="get-a-list-of-installed-packages-using-r"></a>R을 사용하여 설치된 패키지 목록 가져오기  
 R 도구 및 R 함수를 사용하여 여러 가지 방법으로 설치 또는 로드된 패키지 목록을 가져올 수 있습니다.  
  
+   대부분의 R 개발 도구는 현재 R 작업 영역에서 설치 또는 로드되어 있는 패키지의 목록이나 개체 브라우저를 제공합니다.  

+ 계산 컨텍스트에서 패키지 관리를 위해 특별히 제공되는 RevoScaleR 패키지의 다음 함수를 사용하는 것이 좋습니다.
  - [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxfindpackage)
  - [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinstalledpackages)   
  
+   설치된 `installed.packages()`패키지에 포함되어 있는 `utils` 등의 R 함수를 사용할 수 있습니다. 이 함수는 지정한 라이브러리에서 확인된 각 패키지의 DESCRIPTION 파일을 검사한 다음 패키지 이름, 라이브러리 경로 및 버전 번호의 행렬을 반환합니다.  
 
### <a name="examples"></a>예  
다음 예제에서는 `rxInstalledPackages` 함수를 사용하여 제공된 SQL Server 계산 컨텍스트에서 사용할 수 있는 패키지 목록을 가져옵니다.

~~~~
sqlServerCompute <- RxInSqlServer(connectionString = 
"Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
     sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
     sqlPackages
~~~~

 다음 예제에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저의 기본 R 함수 `installed.packages()`를 사용하여 현재 인스턴스에 대한 R_SERVICES 라이브러리에 설치된 패키지 매트릭스를 가져옵니다. DESCRIPTION 파일의 필드 구문 분석을 방지하기 위해 이름만 반환됩니다.  
  
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
  
 자세한 내용은 [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)에서 R 패키지 설명 파일의 선택적 필드 및 기본 필드에 대한 설명을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server에 추가 R 패키지 설치](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
  

