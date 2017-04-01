---
title: "설치 하 고 R 패키지를 관리 합니다. | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 설치 하 고 R 패키지를 관리 합니다.
 실행 되는 R 솔루션 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 기본 R 라이브러리에 설치 된 패키지를 사용 해야 합니다. 보다 일반적으로 R 솔루션에서 R 코드에 파일 경로 지정 하 여 사용자 라이브러리를 참조 합니다 있지만이 프로덕션에 권장 되지 않습니다.

따라서 필요한 모든 패키지에 설치 되어 있는지 확인 하는 데이터베이스 관리자 또는 서버에서 다른 관리자의 작업을이 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스. 경우 있습니다 관리 권한이 없는 컴퓨터에서 호스트 하는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]  인스턴스 있습니다 수 R 패키지를 설치 하는 방법에 대 한 관리자 정보를 제공 및 사용자가 요구 하는 패키지를 구할 수 있는 보안 패키지 저장소에 대 한 액세스를 제공 합니다. 이 섹션에서는 해당 정보를 제공 합니다. 

> [!TIP]
> [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 설치 하 고 데이터베이스 관리자 및 데이터 과학자가 훨씬 자유롭게와 패키지 사용 및 설치에 대 한 제어를 제공 하는 R 패키지를 관리 하기 위한 새로운 기능을 제공 합니다. 자세한 내용은 참조 [SQL Server에 대 한 R 패키지 관리](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)합니다. 

## <a name="installed-packages"></a>설치 된 패키지
설치 하는 경우  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)],  R 기본적으로 **기본** 와 같은 패키지가 설치 되며 `stats` 및 `utils`, 함께 **RevoScaleR** 에 대 한 연결을 지 원하는 패키지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 
> [!NOTE]  
>  기본적으로 설치 된 패키지 목록에 대 한 참조 [Microsoft R Open과 패키지 설치](https://mran.microsoft.com/rro/installed/)합니다.  

 CRAN 또는 다른 저장소에서 한 추가 패키지를 해야 하는 경우에 패키지를 다운로드 하 고 워크스테이션에 설치 해야 합니다.  
  
 서버의 컨텍스트에서 새 패키지를 실행 해야 하는 경우 관리자가 서버에 설치 해야 합니다.   
   
## <a name="where-and-how-to-get-new-packages"></a>새 패키지를 가져오는 위치 및 방법  
 R 패키지에 대한 여러 출처가 있으며 특히 CRAN 및 Bioconductor가 가장 널리 알려져 있습니다. R 언어에 대 한 공식 사이트 ([https://www.r-project.org/](https://www.r-project.org/)) 많은이 리소스를 나열 합니다. 많은 패키지는 소스 코드를 가져올 수 있는 GitHub에도 게시됩니다. 그러나 회사의 누군가가 개발한 R 패키지가 지정되었을 수도 있습니다.  
  
 출처에 관계 없이 패키지는 설치할 압축된 파일 형식으로 제공해야 합니다. 또한 사용 하 여 패키지를 사용 하 여 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], Windows 이진 형식으로 압축 된 파일을 확인 합니다. (일부 패키지의 경우이 형식을 지원 하지 않습니다.) Zip 파일 형식 및 R 패키지를 만드는 방법의 내용에 대 한 자세한 내용은이 자습서에서는 R 프로젝트 사이트에서 PDF 형식으로 다운로드할 수 있는 권장: [Freidrich Leisch: R 패키지를 만드는](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf)합니다. 
  
 일반적으로 R 패키지에서에서 설치할 수 있습니다 쉽게 명령줄 사전에 다운로드 하지 않고 컴퓨터에 있는 경우 인터넷에 액세스 합니다.  일반적으로이 없는 경우 실행 하는 서버와 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 합니다.  따라서 컴퓨터에 설치 하는 R 패키지는 수행 하지 않는 **하지** 인터넷에 연결, 미리 올바른 압축 된 형식으로 패키지를 다운로드 하 고 다음 컴퓨터에서 액세스할 수 있는 폴더에 압축 된 파일을 복사 해야 합니다. 
 
 다음 항목에는 오프 라인 패키지를 설치 하기 위한 두 가지 방법을 설명 합니다. 

+ [오프 라인 패키지 리포지토리를 miniCRAN를 사용 하 여 만들기](../../advanced-analytics/r-services/create-a-local-package-repository-using-minicran.md)

  R 패키지를 사용 하는 방법에 설명 **miniCRAN** 는 오프 라인 저장소를 만들려고 합니다. 이것이 가장 효율적인 방법은 여러 서버에 패키지를 설치 하 고 단일 위치에서 저장소를 관리 하는 경우입니다. 
+ [인터넷에서 새 R 패키지를 설치 합니다.](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)

  압축 된 파일을 수동으로 복사 하 여 오프 라인 패키지를 설치 하기 위한 지침을 포함 합니다.   

## <a name="permissions-required-for-installing-r-packages"></a>R 패키지를 설치하는 데 필요한 사용 권한  
  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]을(를) 실행 중인 컴퓨터에 새 R 패키지를 설치하려면 컴퓨터에 대한 관리자 권한이 있어야 합니다.   

이러한 권한이 없는 경우 관리자에 게 문의하고 설치할 패키지에 관한 정보를 제공합니다.  
  

새 R 패키지를 설치 하는 R 워크스테이션으로 사용 되는 컴퓨터에서 한 컴퓨터는 **하지** 인스턴스 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치 해야 패키지를 설치 하는 컴퓨터에 대 한 관리 권한을 합니다. 패키지를 설치한 후 로컬 컴퓨터에서 실행할 수 있습니다.  
 
> [!NOTE]
>  [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], 새 데이터베이스 역할의 인스턴스 수준 및 데이터베이스 수준 패키지 설치 권한 범위 지정을 지원 하기 위해 추가 되었습니다. 자세한 내용은 참조 [SQL Server에 대 한 R 패키지 관리](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)합니다.
 

### <a name="location-of-default-r-library-location-for-r-services"></a>R 서비스에 대 한 기본 R 라이브러리 위치의 위치

설치한 경우  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 아래 인스턴스에서 사용 하는 R 패키지 라이브러리에 있는 기본 인스턴스를 사용 하 여 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스 폴더. 예를 들어 

+ 기본 인스턴스 _MSSQLSERVER_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
+ 명명 된 인스턴스 _MyNamedInstance_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library` 


오른쪽의 현재 인스턴스에 대 한 기본 라이브러리를 확인 하려면 다음 문을 실행할 수 있습니다. 
~~~~
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
~~~~

자세한 내용은 참조 [결정는 패키지 SQL Server에 설치 된](../../advanced-analytics/r-services/determine-which-packages-are-installed-on-sql-server.md)합니다.

## <a name="managing-installed-packages"></a>설치 된 패키지 관리

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 설치 하 고 데이터베이스 관리자 및 데이터 과학자가 훨씬 자유롭게와 패키지 사용 및 설치에 대 한 제어를 제공 하는 R 패키지를 관리 하기 위한 새로운 기능을 제공 합니다. 자세한 내용은 참조 [SQL Server에 대 한 R 패키지 관리](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)합니다. 

SQL Server 2106 R 서비스를 사용 하는 경우 새 패키지 관리 기능은 사용할 수 없는이 이번에 합니다. 패키지에 설치 된 확인에 대 한 이러한 옵션을 사용할 수는 그 동안에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터, 이러한 옵션 중 하나를 사용 합니다.

+ 폴더에 권한이 있는 경우 기본 라이브러리를 확인 합니다.
+ R R_SERVICES 라이브러리 위치에서 패키지를 나열 하는 명령에서 명령을 실행합니다
+ 인스턴스에서 다음과 같은 저장된 프로시저를 사용 합니다.
   ```SQL
   EXECUTE sp_execute_external_script  @language=N'R'  
        ,@script = N'str(OutputDataSet);  
        packagematrix <- installed.packages();  
        NameOnly <- packagematrix[,1];  
        OutputDataSet <- as.data.frame(NameOnly);'  
        ,@input_data_1 = N'SELECT 1 as col'  
        WITH RESULT SETS ((PackageName nvarchar(250) ))   
   ```


 ## <a name="see-also"></a>관련 항목:  
 [관리 및 모니터링 R 솔루션](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  