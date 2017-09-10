---
title: "R 패키지 설치 및 관리 | Microsoft 문서"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ae30bfc42e42b69158dbba5a38b0bccbe93523b4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="installing-and-managing-r-packages"></a>R 패키지 설치 및 관리
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서 실행되는 모든 R 솔루션은 기본 R 라이브러리에 설치된 패키지를 사용해야 합니다. 일반적으로 R 솔루션은 R 코드에서 파일 경로를 지정하여 사용자 라이브러리를 참조하지만 프로덕션 환경에는 권장되는 방법이 아닙니다.

따라서 모든 필수 패키지가 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스에 설치되도록 하는 것은 데이터베이스 관리자 및 기타 서버 관리자의 태스크입니다. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스를 호스트하는 컴퓨터에 대한 관리 권한이 없는 경우에는 R 패키지 설치 방법에 대한 관리자 정보를 제공하고 사용자가 요청한 패키지를 얻을 수 있는 보안 설정된 패키지 리포지토리에 대한 액세스 권한을 제공할 수 있습니다. 이 섹션에서는 해당 정보를 제공합니다. 

> [!TIP]
> [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]에서는 데이터베이스 관리자와 데이터 과학자가 패키지 사용 및 설치를 더 자유롭게 사용하고 세밀하게 제어할 수 있도록 하는 R 패키지 설치 및 관리를 위한 새로운 기능을 제공합니다. 자세한 내용은 [SQL Server에 대한 R 패키지 관리](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)를 참조하세요. 

## <a name="installed-packages"></a>설치된 패키지
[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 설치할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 연결을 지원하는 **RevoScaleR** 패키지와 함께 `stats` 및 `utils`와 같은 R **기본** 패키지가 기본적으로 설치됩니다.  
  
 
> [!NOTE]  
>  기본적으로 설치되는 패키지 목록을 보려면 [Packages Installed with Microsoft R Open](https://mran.microsoft.com/rro/installed/)(Microsoft R Open과 함께 설치된 패키지)을 참조하세요.  

 CRAN 또는 또 다른 리포지토리에서 추가 패키지가 필요한 경우 패키지를 다운로드하여 워크스테이션에 설치해야 합니다.  
  
 새 패키지를 서버 컨텍스트에서 실행해야 하는 경우 관리자는 패키지를 서버에도 설치해야 합니다.   
   
## <a name="where-and-how-to-get-new-packages"></a>새 패키지를 가져오는 위치 및 방법  
 R 패키지에 대한 여러 출처가 있으며 특히 CRAN 및 Bioconductor가 가장 널리 알려져 있습니다. R 언어 공식 사이트([https://www.r-project.org/](https://www.r-project.org/))에 다양한 리소스가 나와 있습니다. 많은 패키지는 소스 코드를 가져올 수 있는 GitHub에도 게시됩니다. 그러나 회사의 누군가가 개발한 R 패키지가 지정되었을 수도 있습니다.  
  
 출처에 관계 없이 패키지는 설치할 압축된 파일 형식으로 제공해야 합니다. 또한 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서 패키지를 사용하려면 Windows 이진 형식으로 압축된 파일을 가져와야 합니다. 일부 패키지는 이 형식을 지원하지 않을 수 있습니다. R 패키지를 만드는 방법 및 zip 파일 형식의 콘텐츠에 대한 자세한 내용은 [Freidrich Leisch: Creating R Packages](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf)(Freidrich Leisch: R 패키지 만들기) 자습서를 참조하세요. 이 자습서는 R 사이트에서 PDF 형식으로 다운로드할 수 있습니다. 
  
 일반적으로 R 패키지는 컴퓨터가 인터넷에 연결된 경우 패키지를 미리 다운로드하지 않고 명령줄에서 쉽게 설치할 수 있습니다.  일반적인 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]를 실행하는 서버에는 이 방법을 적용할 수 없습니다.  따라서 인터넷에 액세스할 수 **없는** 컴퓨터에 R 패키지를 설치하려면 패키지를 올바른 압축 형식으로 미리 다운로드하고 압축 파일을 컴퓨터에서 액세스할 수 있는 폴더로 복사해야 합니다. 
 
 다음 항목에서는 패키지를 오프라인에서 설치할 수 있는 두 가지 방법을 설명합니다. 

+ [miniCRAN을 사용하여 오프라인 패키지 리포지토리 만들기](../../advanced-analytics/r-services/create-a-local-package-repository-using-minicran.md)

  R 패키지 **miniCRAN**을 사용하여 오프라인 리포지토리를 만드는 방법을 설명합니다. 패키지를 여러 서버에 설치하고 한 곳에서 리포지토리를 관리해야 하는 경우 이 방법이 가장 효율적일 수 있습니다. 
+ [인터넷에서 새 R 패키지 설치](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)

  압축 파일을 수동으로 복사하여 패키지를 오프라인에서 설치하는 지침을 포함합니다.   

## <a name="permissions-required-for-installing-r-packages"></a>R 패키지를 설치하는 데 필요한 사용 권한  
  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]을 실행하는 컴퓨터에서 새 R 패키지를 설치하려면 컴퓨터에 대한 관리자 권한이 있어야 합니다.   

이러한 권한이 없는 경우 관리자에 게 문의하고 설치할 패키지에 관한 정보를 제공합니다.  
  

R 워크스테이션으로 사용 중인 컴퓨터에 새 R 패키지를 설치하고 컴퓨터에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]의 인스턴스가 설치되어 있지 **않은** 경우 패키지를 설치하려면 여전히 컴퓨터에 대한 관리자 권한이 있어야 합니다. 패키지를 설치한 후 로컬 컴퓨터에서 실행할 수 있습니다.  
 
> [!NOTE]
> [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]에서는 인스턴스 수준 및 데이터베이스 수준에서 패키지 설치 권한의 범위 지정을 지원하도록 새 데이터베이스 역할이 추가되었습니다. 자세한 내용은 [SQL Server에 대한 R 패키지 관리](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)를 참조하세요.
 

### <a name="location-of-default-r-library-location-for-r-services"></a>R Services에 대한 기본 R 라이브러리의 위치

기본 인스턴스를 사용하여 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 설치한 경우 인스턴스에서 사용되는 R 패키지 라이브러리는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스 폴더 아래에 있습니다. 예를 들어 

+ 기본 인스턴스 _MSSQLSERVER_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
+ 명명된 인스턴스 _MyNamedInstance_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library` 


다음 문을 실행하여 R의 현재 인스턴스에 대한 기본 라이브러리를 확인할 수 있습니다. 
~~~~
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
~~~~

자세한 내용은 [SQL Server에 설치된 패키지 확인](../../advanced-analytics/r-services/determine-which-packages-are-installed-on-sql-server.md)을 참조하세요.

## <a name="managing-installed-packages"></a>설치된 패키지 관리

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]에서는 데이터베이스 관리자와 데이터 과학자가 패키지 사용 및 설치를 더 자유롭게 사용하고 세밀하게 제어할 수 있도록 하는 R 패키지 설치 및 관리를 위한 새로운 기능을 제공합니다. 자세한 내용은 [SQL Server에 대한 R 패키지 관리](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md)를 참조하세요. 

SQL Server 2106 R Services를 사용 중인 경우 현재 새 패키지 관리 기능을 사용할 수 없습니다. 현재는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터에 설치된 패키지를 확인할 수 있는 다음 옵션 중 하나를 사용합니다.

+ 폴더에 대한 사용 권한이 없는 경우 기본 라이브러리를 봅니다.
+ R 명령에서 명령을 실행하여 R_SERVICES 라이브러리 위치에서 패키지를 나열합니다.
+ 인스턴스에서 다음과 같은 저장 프로시저를 사용합니다.
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
 [R 솔루션 관리 및 모니터링](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  

