---
title: "SQL Server에 추가 R 패키지 설치 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 16
---
# SQL Server에 추가 R 패키지 설치
이 항목의 인스턴스를 새 R 패키지를 설치 하는 방법에 설명 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 인터넷에 액세스할 수 있는 컴퓨터에 있습니다.

## <a name="1-locate-the-windows-binaries-in-zip-file-format"></a>1. ZIP 파일 형식으로 Windows 바이너리를 찾습니다.

R 패키지는 다양 한 플랫폼에서 지원 됩니다. 설치 하려는 패키지에는 Windows 플랫폼에 대 한 이진 형식이 있는지 확인 해야 합니다. 그렇지 않은 경우 다운로드 한 패키지는 작동 하지 않습니다.

예를 들어 Bioconductor에서 [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) 패키지를 가져오려면:  
  
1.  **패키지 보관** 목록에서 **Windows 이진** 버전을 찾습니다.  
  
2.  .ZIP 파일에 대한 링크를 마우스 오른쪽 단추로 클릭하고  **다른 이름으로 대상 저장**을 선택합니다.  
  
3.  압축된 패키지가 저장된 로컬 폴더로 이동하고 **저장**을 클릭합니다.  
  
 이 프로세스는 패키지의 로컬 복사본을 만듭니다. 그런 다음 패키지를 설치 하거나 인터넷에 액세스 하지 않은 서버에 압축 된 패키지를 복사할 수 있습니다.  
  
  
## <a name="2-open-the-default-r-package-library-for-sql-server-r-services"></a>2. SQL Server R 서비스에 대 한 기본 R 패키지 라이브러리를 엽니다. 

R 패키지 연관 서버의 폴더로 이동 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 설치 합니다. 현재 인스턴스와 연결 된 기본 라이브러리에 패키지를 설치 하는 것입니다. 

이 라이브러리를 찾는 방법에 대 한 지침을 참조 하십시오. [설치 및 관리 하는 R 패키지](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)합니다.

   패키지를 실행할 각 인스턴스에 대해 별도 패키지의 복사본을 설치 해야 합니다. 현재 패키지 인스턴스 간에 공유할 수 없습니다.
     
  
## <a name="3-open-an-administrative-command-prompt"></a>3. 관리 명령 프롬프트를 열으십시오 

관리자 권한으로 R을 엽니다.  이렇게 하려면 Windows 명령 p ropt를 사용 하거나 R 유틸리티 중 하나를 사용 하 여 합니다.
  
### <a name="using-the-windows-command-prompt"></a>Windows 명령 프롬프트 사용 

1. 관리자 권한으로 Windows 명령 프롬프트를 열고 RTerm.Exe 또는 RGui.exe 파일이 있는 디렉터리로 이동 합니다.  
  
    기본 성치의 경우 이는 R **\bin** 디렉터리입니다. 예를 들어, [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], R 도구는 여기에서 확인할: 

    **기본 인스턴스**

     `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin` 
 
     **명명 된 인스턴스**
   
     `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`  
  
2. Run **R.Exe**.  
  
### <a name="using-the-r-commandline-utilities"></a>R 명령줄 유틸리티 사용 
  
1. Windows 탐색기를 사용하여 R 도구가 포함된 디렉터리로 이동합니다.  
  
2. 마우스 오른쪽 단추로 클릭 **RGui.exe** 또는 **RTerm.exe**, 를 선택 하 고 **관리자 권한으로 실행**합니다.  
## <a name="4-install-the-package"></a>4. 패키지 설치

패키지를 설치 하는 R 명령이 인터넷 또는 로컬 압축 된 파일에서 패키지를 가져 오는 있는지 여부에 따라 달라 집니다.  
  
### <a name="install-package-from-internet"></a>인터넷에서 패키지를 설치 합니다.  
  
1.  일반적으로 CRAN 또는 미러 사이트 중 하나에서 새 패키지를 설치 하려면 다음 명령을 사용 합니다.  
  
    ```  
    install.packages("target_package_name")  
    ```
    
    참고로 큰따옴표는 패키지 이름에 대해 언제나 필요합니다.

2.  패키지를 설치 해야 하는 라이브러리를 지정 하려면이 이와 같은 명령을 사용 하 여 라이브러리 위치를 설정 합니다.
    
    ```  
    lib.SQL <- "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.MSSQLSERVER\\R_SERVICES\\library"    
    ```

    에 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], 현재 라이브러리 패키지를 하나만 허용 됩니다. 사용자 라이브러리에 패키지를 설치 하지 않으면 또는에서 패키지를 실행할 수 없습니다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다.   
     
3.  다음 문은 라이브러리 위치를 정의 R 서비스에서 사용 되는 패키지 라이브러리에 인기 있는 e1070 패키지를 설치 합니다.  
  
    ```  
    install.packages("e1071", lib = lib.SQL)  
    ```  
  
4.  패키지를 가져올 미러 사이트에 대해 묻는 메시지가 나타납니다. 사용자의 위치에 편리한 미러 사이트를 선택합니다.  
  
    현재 CRAN 미러의 목록에 대해서는 [이 사이트](https://cran.r-project.org/mirrors.html)를 참조하세요.  
  
    > [!TIP]  
    >  새 패키지를 추가할 때마다 미러 사이트를 선택할 필요가 없도록 하려면 언제나 같은 리포지토리를 사용하도록 R 개발 환경을 구성할 수 있습니다.  
    >   
    >  이렇게 하려면 글로벌 R 설정 파일 .Rprofile을 편집하고 다음 줄을 추가합니다.  
    >   
    >  `options(repos=structure(c(CRAN="<mirror site URL>")))`  
    >   
    >  기본 설정 및 R 런타임이 시작될 때 로드된 다른 파일에 대한 자세한 내용을 보려면 R 콘솔에서 이 명령을 실행합니다.  
    >   
    >  `?Startup`  
  
5.  대상 패키지가 추가 패키지에 따라 달라지는 경우 R 설치 관리자가 자동으로 종속성을 다운로드하고 설치합니다.  
  
### <a name="manual-package-installation-or-installing-on-computer-with-no-internet-access"></a>수동 패키지 설치 또는 인터넷 액세스가 제외 된 컴퓨터에 설치 

1. 패키지를 설치 하려는 경우 종속성을 사전에 필요한 패키지를 가져오고 폴더에 파일을 zip 파일로 압축 하는 다른 패키지와 함께 추가 합니다.

    > [!TIP]
    > 
    > 사용 하 여 로컬 저장소를 설정 하는 것이 좋습니다 [miniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/) R 패키지의 자주 오프 라인 설치를 지원 해야 하는 경우.  
  
2.  R 명령 프롬프트에서 다음 명령을 입력하여 설치할 패키지의 경로 및 이름을 지정합니다.  
   
    ```  
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)  
    ``` 
     
    이 명령은 디렉터리에 복사본을 저장 하는 것으로 가정 하는 로컬 압축 된 파일의에서 R 패키지를 추출 `C:\Temp\Downloaded packages`, 로컬 컴퓨터에 R 라이브러리로 (종속성)과 함께 패키지를 설치 합니다.  
  
3.  이전에 컴퓨터의 R 환경을 수정 하는 경우 확인 해야 하는 R 환경 변수 `.libPath` 인스턴스에 대 한 R_SERVICES 폴더를 가리키는 하나의 경로 사용 합니다.  
  
> [!NOTE]
> SQL Server R 서비스 외에도 Microsoft R 서버 (독립 실행형)를 설치한 경우 컴퓨터의 R R 도구 및 라이브러리와 별도 설치를 갖습니다. R_SERVER 라이브러리에 설치 된 패키지를 Microsoft R 서버 에서만 사용 되 고에서 액세스할 수 없는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
> 
>  SQL Server에서 사용 하려는 패키지를 설치 하는 경우 R_SERVICES 라이브러리를 사용 해야 합니다.

  
## <a name="see-also"></a>관련 항목:  
 [SQL Server R 서비스 &#40; 데이터베이스에 &#41; 설정](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  