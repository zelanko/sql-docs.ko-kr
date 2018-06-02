---
title: Integration Services-병렬 데이터 웨어하우스를 로드 | Microsoft Docs
description: SQL Server Integration Services (SSIS) 패키지를 사용 하 여 병렬 데이터 웨어하우스 (PDW)에 데이터를 로드 하기 위한 참조 및 배포 정보를 제공 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 718a076822a4304e0ba951f3ca1903bb7c009e17
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34586065"
---
# <a name="load-data-with-integration-services-to-parallel-data-warehouse"></a>병렬 데이터 웨어하우스를 Integration Services를 사용 하 여 데이터를 로드 합니다.
SQL Server Integration Services (SSIS) 패키지를 사용 하 여 데이터를 SQL Server 병렬 데이터 웨어하우스에 로드 하기 위한 참조 및 배포 정보를 제공 합니다.  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](http://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx) on MSDN.  

-->
  
## <a name="Basics"></a>기본 사항  
Integration Services 고성능 추출, 변환 및 로드 (ETL)의 데이터에 대 한 SQL Server의 구성 요소 이며 일반적으로 채우고 데이터 웨어하우스를 업데이트 하는 데 사용 됩니다.  
  
PDW 대상 어댑터는 PDW를 Integration Services dtsx 패키지를 사용 하 여 데이터를 로드할 수 있도록 Integration Services 구성 요소입니다. SQL ServerPDW에 대 한 패키지 워크플로 로드 하 고 여러 원본의 데이터와 여러 대상으로 데이터를 병합할 수 있습니다. 로드는 한 패키지 내에서, 그리고 동시에 실행 중인 여러 패키지에 걸쳐 병렬로 실행되며 동일한 어플라이언스에서 병렬로 실행할 수 있는 최대 로드는 10개입니다.  
  
이 항목에서 설명 하는 작업 외에도 필터링, 변환, 분석, Integration Services의 다른 기능을 사용할 수 있으며 데이터 웨어하우스에 로드 하기 전에 데이터를 정리할 수 있습니다. 또한 SQL 문을 실행하거나, 자식 패키지를 실행하거나, 메일을 전송하여 패키지의 워크플로를 개선할 수도 있습니다.  
  
Integration Services의 전체 설명서를 참조 하십시오. [SQL Server Integration Services](http://msdn.microsoft.com/library/ms141026(v=sql11).aspx)합니다.  
  
## <a name="HowToDeployPackage"></a>Integration Services 패키지를 실행 하기 위한 메서드  
Integration Services 패키지를 실행 하려면 다음이 방법 중 하나를 사용 합니다.  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>SQL Server 2008 R2 Business Intelligence Development Studio (BIDS)에서 실행  
BIDS 내에서 패키지를 실행 하려면 패키지를 마우스 오른쪽 단추로 클릭 하 고 선택 **패키지 실행**합니다.  
  
BIDS는 기본적으로 64 비트 이진 파일을 사용 하 여 패키지를 실행 합니다. 에 의해 결정 됩니다이 **Run64BitRuntime** 속성 패키지 합니다. 이 속성을 설정 하려면로 이동 **솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다. 에 **Integration Services 속성 페이지**로 이동 **구성 속성** 선택 **디버깅**합니다. 표시 됩니다는 **Run64BitRuntime** 아래의 속성은 **디버그 옵션**합니다. 를 사용 하려면 32 비트 런타임을 설정이 **False**합니다. 를 사용 하려면 64 비트 런타임을 설정이 **True**합니다.  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>SQL Server 2012 SQL Server 데이터 도구 실행  
SQL Server 데이터 도구 내에서 패키지를 실행 하려면 패키지를 마우스 오른쪽 단추로 클릭 하 고 선택 **패키지 실행**합니다.  
  
### <a name="run-from-powershell"></a>PowerShell에서 실행  
Windows PowerShell에서 패키지를 실행 하려면를 사용 하 여 **dtexec** 유틸리티: `dtexec /FILE <packagePath>`  
  
예를 들어 IPv4 주소를 사용하는 경우 `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
### <a name="run-from-a-windows-command-prompt"></a>Windows에서 실행 명령 프롬프트 
Windows 명령 프롬프트에서 패키지를 실행 하려면를 사용 하 여 **dtexec** 유틸리티: `dtexec /FILE <packagePath>`  
  
예: `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="DataTypes"></a>데이터 형식  
Integration Services를 사용 하 여 SQL Server PDW 데이터베이스에 데이터 원본에서 데이터 로드를 데이터에 먼저 매핑됩니다 원본 데이터에서 Integration Services 데이터 형식입니다. 이를 통해 여러 데이터 원본의 데이터가 데이터 형식의 공통 집합에 매핑될 수 있습니다.  
  
그런 다음 데이터를 Integration Services에서 SQL Server PDW 데이터 형식에 매핑됩니다. 각 SQL Server PDW 데이터 형식에 대해 다음 표에서 SQL Server PDW 데이터 형식으로 변환 될 수 있는 Integration Services 데이터 형식을 나열 합니다.  
  
|PDW 데이터 형식|Integration Services 데이터 형식 (s) PDW 데이터 형식에 매핑되는|  
|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|  
|BIT|DT_BOOL|  
|bigint|DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4|  
|CHAR|DT_STR|  
|DATE|DT_DBDATE|  
|DATETIME|DT_DATE, DT_DBDATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2|  
|DATETIME2|DT_DATE, DT_DBDATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2|  
|DATETIMEOFFSET|DT_WSTR|  
|DECIMAL|DT_DECIMAL, DT_I1, DT_I2, DT_I4, DT_I4, DT_I8, DT_NUMERIC, DT_UI1, DT_UI2, DT_UI4, DT_UI8|  
|FLOAT|DT_R4, DT_R8|  
|INT|DT_I1, DTI2, DT_I4, DT_UI1, DT_UI2|  
|MONEY|DT_CY|  
|NCHAR|DT_WSTR|  
|NUMERIC|DT_DECIMAL, DT_I1, DT_I2, DT_I4, DT_I8, DT_NUMERIC, DT_UI1, DT_UI2, DT_UI4, DT_UI8|  
|NVARCHAR|DT_WSTR, DT_STR|  
|real|DT_R4|  
|SMALLDATETIME|DT_DBTIMESTAMP2|  
|SMALLINT|DT_I1, DT_I2, DT_UI1|  
|SMALLMONEY|DT_R4|  
|TIME|DT_WSTR|  
|TINYINT|DT_I1|  
|VARBINARY|DT_BYTES|  
|VARCHAR|DT_STR|  
  
**데이터 형식 전체 자릿수에 대 한 제한 된 지원**  
  
PDW 전체 자릿수가 28 보다 큰 값을 포함 하는 DT_NUMERIC 또는 DT_DECIMAL 입력된 열을 매핑하는 경우 유효성 검사 오류를 생성 합니다.  
  
**지원 되지 않는 데이터 형식**  
  
SQL Server PDW 다음 Integration Services 데이터 형식 지원 하지 않습니다.  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
SQL Server PDW에 이러한 형식의 데이터를 포함 하는 열을 로드 하려면 호환 되는 데이터 형식으로 데이터를 변환 하는 데이터 흐름에는 데이터 변환 업스트림을 추가 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
Integration Services 부하 패키지를 실행 하려면 다음을 수행 해야 합니다.  
  
-   데이터베이스에 대 한 권한을 로드 합니다.  
  
-   적용 가능한 삽입, 업데이트, 대상 테이블에 대 한 삭제 권한을 합니다.  
  
-   준비 데이터베이스를 사용 하는 경우 준비 데이터베이스에 대 한 만들기 권한이 있습니다. 이것은 임시 테이블을 만들면 됩니다.  
  
-   준비 데이터베이스가 사용 되는 경우 대상 데이터베이스에 대 한 만들기 권한이 있습니다. 이것은 임시 테이블을 만들면 됩니다.  
  
## <a name="GenRemarks"></a>일반 설명  
Integration Services 패키지를 실행 하는 여러 SQL Server PDW 대상에 연결 중 하나가 종료 될 경우 Integration Services의 모든 SQL Server PDW 대상에 데이터 밀어넣기를 중지 합니다.  
  
## <a name="Limits"></a>제한 사항 및 제한 사항  
Integration Services 패키지에 대 한 동일한 데이터 원본에 대 한 SQL Server PDW 대상 수는 최대 활성 로드 수로 제한 됩니다. 최대값은 미리 구성되며 사용자가 구성할 수 없습니다. 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
동일한 데이터 원본에 대 한 각 Integration Services 패키지 대상은 패키지가 실행 중일 때 하나의 부하로 계산 합니다. 예를 들어 최대 활성 로드가 10개인 경우 동일한 데이터 원본의 대상을 11개 이상 열려고 하면 패키지가 실행되지 않습니다.  
  
각 패키지가 최대 활성 로드보다 더 많은 로드를 사용하지 않는 한 여러 패키지를 동시에 실행할 수 있습니다. 예를 들어 최대 활성 로드가 10개인 경우 각각 10개 대상을 사용하는 패키지 2개를 동시에 실행할 수 있습니다. 하나의 패키지가 실행되는 동안 다른 패키지는 로드 큐에서 대기합니다.  
  
로드 큐의 로드 수가 최대 대기 로드 수를 초과하면 패키지가 실행되지 않습니다. 예를 들어 경우 최대 로드 수가 어플라이언스 당 10 이며 최대 대기 로드 수가 어플라이언스 당 40 개인은 실행할 수 있습니다 동시에 다섯 개의 Integration Services 패키지를 각각 10 개 대상을 여 합니다. 여섯 번째 패키지를 실행하려고 하면 실행되지 않습니다.  

> [!IMPORTANT]
> PDW 대상 어댑터가 SSIS에서 OLE DB 데이터 원본을 사용 하 여, 원본 테이블에 있는 경우 SQL 데이터 정렬과 함께 char 및 varchar 열 데이터가 손상이 될 수 있습니다. 원본 테이블 SQL 데이터 정렬이 있는 char 또는 varchar 열을 포함 하는 경우 ADO.NET 원본을 사용 하는 것이 좋습니다. 

  
## <a name="Locks"></a>잠금 동작  
Integration Services를 사용 하 여 데이터를 로드할 때 SQL ServerPDW 행 수준 잠금을 사용 하 여 대상 테이블의 데이터를 업데이트 합니다. 따라서 각 행이 업데이트될 때는 각 행에 대한 읽기 및 쓰기가 잠깁니다. 데이터가 준비 테이블에 로드될 때는 대상 테이블의 행이 잠기지 않습니다.  
  
## <a name="Examples"></a>예제  
  
### <a name="Walkthrough"></a>A. 플랫 파일에서 간단한 부하  
다음 연습에는 Integration Services를 사용 하 여 SQL Server PDW 어플라이언스에 플랫 파일 데이터를 로드 하는 간단한 데이터 로드를 보여 줍니다.  이 예에서는 위에 설명 된 대로 클라이언트 컴퓨터에 이미 설치 된 Integration Services 및 SQL Server PDW 대상 설치가 완료 된 후 가정 합니다.  
  
이 예제에서는으로 로드 된 `Orders` DDL 테이블입니다. `Orders` 테이블의 일부인는 `LoadExampleDB` 데이터베이스입니다.  
  
```sql  
CREATE TABLE LoadExampleDB.dbo.Orders (  
   id INT,  
   city varchar(25),  
   lastUpdateDate DATE,  
   orderDate DATE)  
;  
```  
  
데이터 로드는 다음과 같습니다.  
  
```  
id        city           lastUpdateDate     orderdate  
--------- -------------- ------------------ ----------  
1         Seattle        2010-05-01         2010-01-01  
2         Denver         2002-06-25         1999-01-02  
```  
  
로드 준비 과정에서 플랫 파일을 만들 `exampleLoad.txt`, 데이터 로드를 포함 하 합니다.  
  
```  
id,city,lastUpdateDate,orderDate  
1,Seattle,2010-05-01,2010-01-01  
2,Denver,2002-06-25,1999-01-02  
```  
  
먼저, 다음이 단계를 수행 하 여 Integration Services 패키지를 만듭니다.  
  
1.  SQL Server Data Tools에서 \(SSDT\)선택, **파일**, **새로**, 차례로 **프로젝트**합니다. 선택 **Integration Services 프로젝트** 옵션 목록에서 합니다. 이 프로젝트의 이름을 `ExampleLoad`를 클릭 하 고 **확인**합니다.  
  
2.  클릭는 **제어 흐름** 탭 한 다음 끌어는 **데이터 흐름 태스크** 에서 **도구 상자** 에 **제어 흐름** 창.  
  
3.  클릭는 **데이터 흐름** 탭 한 다음 끌어 **플랫 파일 원본** 에서 **도구 상자** 에 **데이터 흐름** 창. 열려는 방금 만든 상자를 두 번 클릭은 **플랫 파일 원본 편집기**합니다.  
  
4.  클릭 **연결 관리자** 클릭 하 고 **새로**합니다.  
  
5.  에 **연결 관리자 이름** 상자는 연결에 대 한 친숙 한 이름을 입력 합니다. 예를 들어 `Example Load Flat File CM`합니다.  
  
6.  클릭 **찾아보기** 선택 하 고는 `ExampleLoad.txt` 로컬 컴퓨터에서 파일입니다.  
  
7.  플랫 파일에 열 이름 사용 하 여 행이 포함 되어 있으므로 클릭는 **첫 번째 데이터 행의 열 이름** 상자입니다.  
  
8.  클릭 **열** 왼쪽된 열 및 미리 보기에 열 이름이 있는지 확인 하 여 로드 되는 데이터와 데이터 올바르게 해석 되었습니다.  
  
9. 클릭 **고급** 왼쪽된 열에 있습니다. 데이터와 연결 된 데이터 형식을 검토 하려면 각 열 이름을 클릭 합니다. 로드 된 데이터의 데이터 형식이 대상 열 유형과 호환 수 있도록 변경 상자에 입력 합니다.  
  
10. 클릭 **확인** 연결 관리자를 저장 합니다.  
  
11. 클릭 **확인** 종료 하 고 **플랫 파일 원본 편집기**합니다.  
  
데이터 흐름에 대 한 대상을 지정 합니다.  
  
1.  끌어서는 **SQL Server PDW 대상** 에서 **도구 상자** 에 **데이터 흐름** 창.  
  
2.  로드를 방금 만든 상자를 두 번 클릭은 **SQL Server PDW 대상 편집기**합니다.  
  
3.  옆에 있는 아래쪽 화살표를 클릭 **연결 관리자**합니다.  
  
4.  선택 **새 연결을 만들**합니다.  
  
5.  관련 정보 어플라이언스로 서버, 사용자, 암호 및 대상 데이터베이스에 대 한 정보를 입력 합니다. (예는 아래 참조). 마치면 **확인**을 클릭합니다.  
  
    InfiniBand 연결에 대 한 **서버 이름**: 입력 < 응용 프로그램 이름 >-SQLCTL01, 17001 합니다.  
  
    이더넷 연결에 대 한 **서버 이름**: 노드 클러스터 제어, 쉼표, 포트 17001의 IP 주소를 입력 합니다. 예를 들어 10.192.63.134,17001 합니다.  
  
    **사용자:**`user1`  
  
    **암호:**`password1`  
  
    **대상 데이터베이스의 경우:**`LoadExampleDB`  
  
6.  대상 테이블 선택: `Orders`합니다.  
  
7.  선택 **Append** 로드 모드와 클릭으로 **확인**합니다.  
  
데이터 흐름 원본에서 대상으로 지정 합니다.  
  
1.  에 **데이터 흐름** 창에서 녹색 화살표를 끌어는 **플랫 파일 원본** 상자는 **SQL Server PDW 대상** 상자.  
  
2.  두 번 클릭 하 여 **SQL Server PDW 대상** 상자를 표시는 **SQL Server PDW 대상 편집기** 다시 합니다. 아래 표시 됩니다는 왼쪽에 플랫 파일에서 열 이름을 **매핑되지 않은 입력 열**합니다. 아래 표시 됩니다는 대상 테이블의 열 이름 오른쪽의 **매핑되지 않은 대상 열**합니다. 끌거나에 일치 하는 열 이름을 두 번 클릭 하 여 열을 매핑할는 **매핑되지 않은 입력 열** 및 **매핑되지 않은 대상 열** 목록을 **매핑된 열**상자입니다. 클릭 **확인** 여 설정을 저장 합니다.  
  
3.  클릭 하 여 패키지를 저장할 **저장** 에 **파일** 메뉴.  
  
Integration Services 컴퓨터에 패키지를 실행 합니다.  
  
1.  Integration Services에서**솔루션 탐색기** (오른쪽 열)을 마우스 오른쪽 단추로 클릭 `Package.dtsx` 선택 **Execute**합니다.  
  
2.  패키지 실행 되 고 진행 상황 및 오류에 표시 됩니다는 **진행률** 창. SQL 클라이언트를 사용 하 여 부하를 확인 하거나 SQL Server PDW 관리 콘솔을 통해 로드를 모니터링 합니다.  
  
## <a name="see-also"></a>관련 항목  
[SSIS PDW 대상 어댑터를 사용 하는 스크립트 태스크 만들기](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](http://msdn.microsoft.com/library/ms141026\(v=sql11\).aspx)  
[(Integration Services) 패키지 디자인 및 구현](http://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx)  
[자습서: 마법사를 사용 하 여 기본 패키지 만들기](http://technet.microsoft.com/library/ms365330\(v=sql11\).aspx)  
[시작 (Integration Services)](http://go.microsoft.com/fwlink/?LinkId=202412)  
[동적 패키지 생성 예제 추가 정보](http://go.microsoft.com/fwlink/?LinkId=202413)  
[병렬 처리 (SQL Server 비디오)에 대 한 SSIS 패키지 디자인](http://msdn.microsoft.com/library/dd795221.aspx)  
[Microsoft SQL Server 커뮤니티 예제: Integration Services](http://go.microsoft.com/fwlink/?LinkId=202415)  
[증분 로드 개선 변경 데이터 캡처](http://msdn.microsoft.com/library/bb895315\(v=sql11\).aspx)  
[느린 변경 차원 변환](http://msdn.microsoft.com/library/ms141715\(v=sql11\).aspx)  
[대량 삽입 태스크](http://msdn.microsoft.com/library/ms141239\(v=sql11\).aspx)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->
