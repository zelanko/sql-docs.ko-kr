---
title: Integration Services를 사용하여 로드
description: SQL Server Integration Services (SSIS) 패키지를 사용 하 여 데이터를 PDW (병렬 데이터 웨어하우스)로 로드 하기 위한 참조 및 배포 정보를 제공 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b0bcb5cfe1ec4111aaea7153f35bca084df62b76
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401012"
---
# <a name="load-data-with-integration-services-to-parallel-data-warehouse"></a>병렬 데이터 웨어하우스에 Integration Services를 사용 하 여 데이터 로드
SQL Server Integration Services (SSIS) 패키지를 사용 하 여 SQL Server 병렬 데이터 웨어하우스로 데이터를 로드 하기 위한 참조 및 배포 정보를 제공 합니다.  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx) on MSDN.  

-->
  
## <a name="Basics"></a>기본 사항  
Integration Services은 고성능의 데이터 ETL (추출, 변환 및 로드)을 위한 SQL Server 구성 요소 이며 일반적으로 데이터 웨어하우스를 채우고 업데이트 하는 데 사용 됩니다.  
  
PDW 대상 어댑터는 Integration Services package.dtsx 패키지를 사용 하 여 PDW로 데이터를 로드할 수 있도록 하는 Integration Services 구성 요소입니다. SQL ServerPDW에 대 한 패키지 워크플로에서 여러 원본의 데이터를 로드 및 병합 하 고 데이터를 여러 대상으로 로드할 수 있습니다. 로드는 한 패키지 내에서, 그리고 동시에 실행 중인 여러 패키지에 걸쳐 병렬로 실행되며 동일한 어플라이언스에서 병렬로 실행할 수 있는 최대 로드는 10개입니다.  
  
이 항목에서 설명 하는 태스크 외에도 Integration Services의 다른 기능을 사용 하 여 데이터를 데이터 웨어하우스에 로드 하기 전에 필터링, 변환, 분석 및 정리할 수 있습니다. 또한 SQL 문을 실행하거나, 자식 패키지를 실행하거나, 메일을 전송하여 패키지의 워크플로를 개선할 수도 있습니다.  
  
Integration Services에 대 한 전체 설명서는 [SQL Server Integration Services](../integration-services/sql-server-integration-services.md)를 참조 하세요.  
  
## <a name="HowToDeployPackage"></a>Integration Services 패키지를 실행 하는 방법  
이러한 방법 중 하나를 사용 하 여 Integration Services 패키지를 실행 합니다.  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>SQL Server 2008 R2 Business Intelligence Development Studio에서 실행 (BIDS)  
BIDS 내에서 패키지를 실행 하려면 패키지를 마우스 오른쪽 단추로 클릭 하 고 **패키지 실행**을 선택 합니다.  
  
기본적으로 BIDS는 64 비트 이진 파일을 사용 하 여 패키지를 실행 합니다. 이는 **Run64BitRuntime** package 속성에 의해 결정 됩니다. 이 속성을 설정 하려면 **솔루션 탐색기**로 이동 하 여 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다. **Integration Services 속성 페이지**에서 **구성 속성** 으로 이동 하 고 **디버깅**을 선택 합니다. **디버그 옵션**아래에 **Run64BitRuntime** 속성이 표시 됩니다. 32 비트 런타임을 사용 하려면이를 **False**로 설정 합니다. 64 비트 런타임을 사용 하려면이를 **True**로 설정 합니다.  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>SQL Server 2012 SQL Server Data Tools에서 실행  
SQL Server Data Tools 내에서 패키지를 실행 하려면 패키지를 마우스 오른쪽 단추로 클릭 하 고 **패키지 실행**을 선택 합니다.  
  
### <a name="run-from-powershell"></a>PowerShell에서 실행  
**Dtexec** 유틸리티를 사용 하 여 Windows PowerShell에서 패키지를 실행 하려면 다음을 수행 합니다.`dtexec /FILE <packagePath>`  
  
예를 들어 `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
### <a name="run-from-a-windows-command-prompt"></a>Windows 명령 프롬프트에서 실행 
**Dtexec** 유틸리티를 사용 하 여 Windows 명령 프롬프트에서 패키지를 실행 하려면 다음을 수행 합니다.`dtexec /FILE <packagePath>`  
  
예: `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="DataTypes"></a>데이터 형식  
Integration Services를 사용 하 여 데이터 원본에서 SQL Server PDW 데이터베이스로 데이터를 로드할 때 데이터는 먼저 원본 데이터에서 Integration Services 데이터 형식으로 매핑됩니다. 이를 통해 여러 데이터 원본의 데이터가 데이터 형식의 공통 집합에 매핑될 수 있습니다.  
  
그런 다음 데이터는 Integration Services에서 SQL Server PDW 데이터 형식으로 매핑됩니다. 다음 표에서는 각 SQL Server PDW 데이터 형식에 대해 SQL Server PDW 데이터 형식으로 변환할 수 있는 Integration Services 데이터 형식을 보여 줍니다.  
  
|PDW 데이터 형식|PDW 데이터 형식에 매핑되는 Integration Services 데이터 형식|  
|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|  
|BIT|DT_BOOL|  
|BIGINT|DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4|  
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
|SmallInt|DT_I1, DT_I2, DT_UI1|  
|SMALLMONEY|DT_R4|  
|TIME|DT_WSTR|  
|TINYINT|DT_I1|  
|VARBINARY|DT_BYTES|  
|VARCHAR|DT_STR|  
  
**데이터 형식 전체 자릿수에 대 한 제한 된 지원**  
  
DT_NUMERIC 또는 전체 자릿수가 28 보다 큰 값을 포함 하는 DT_DECIMAL 입력 열을 매핑하는 경우 PDW는 유효성 검사 오류를 생성 합니다.  
  
**지원되지 않는 데이터 형식**  
  
SQL Server PDW는 다음 Integration Services 데이터 형식을 지원 하지 않습니다.  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
이러한 형식의 데이터를 포함 하는 열을 SQL Server PDW으로 로드 하려면 데이터를 호환 되는 데이터 형식으로 변환 하기 위해 데이터 흐름에 데이터 변환 업스트림을 추가 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
Integration Services 로드 패키지를 실행 하려면 다음이 필요 합니다.  
  
-   데이터베이스에 대 한 로드 권한  
  
-   대상 테이블에 대해 적용 가능한 INSERT, UPDATE, DELETE 권한입니다.  
  
-   준비 데이터베이스를 사용 하는 경우 준비 데이터베이스에 대 한 CREATE 권한이 필요 합니다. 임시 테이블을 만들기 위한 것입니다.  
  
-   준비 데이터베이스를 사용 하지 않는 경우 대상 데이터베이스에 대 한 CREATE 권한이 필요 합니다. 임시 테이블을 만들기 위한 것입니다.  
  
## <a name="GenRemarks"></a>일반적인 주의 사항  
Integration Services 패키지에 여러 SQL Server PDW 대상이 실행 되 고 있고 연결 중 하나가 종료 되 면 Integration Services 모든 SQL Server PDW 대상에 데이터를 푸시하는 것이 중지 됩니다.  
  
## <a name="Limits"></a>제한 사항  
Integration Services 패키지의 경우 동일한 데이터 원본에 대 한 SQL Server PDW 대상 수는 최대 활성 부하 수에 의해 제한 됩니다. 최대값은 미리 구성되며 사용자가 구성할 수 없습니다. 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
동일한 데이터 원본에 대 한 각 Integration Services 패키지 대상은 패키지가 실행 중일 때 하나의 부하로 계산 됩니다. 예를 들어 최대 활성 로드가 10개인 경우 동일한 데이터 원본의 대상을 11개 이상 열려고 하면 패키지가 실행되지 않습니다.  
  
각 패키지가 최대 활성 로드보다 더 많은 로드를 사용하지 않는 한 여러 패키지를 동시에 실행할 수 있습니다. 예를 들어 최대 활성 로드가 10개인 경우 각각 10개 대상을 사용하는 패키지 2개를 동시에 실행할 수 있습니다. 하나의 패키지가 실행되는 동안 다른 패키지는 로드 큐에서 대기합니다.  
  
로드 큐의 로드 수가 최대 대기 로드 수를 초과하면 패키지가 실행되지 않습니다. 예를 들어 최대 로드 수가 어플라이언스 당 10 개이고 최대 대기 중인 로드 수가 어플라이언스 당 40 인 경우 각각 10 개의 대상을 여는 Integration Services 패키지를 동시에 실행할 수 있습니다. 여섯 번째 패키지를 실행하려고 하면 실행되지 않습니다.  

> [!IMPORTANT]
> 원본 테이블에 SQL 데이터 정렬을 사용 하는 char 및 varchar 열이 포함 되어 있으면 PDW 대상 어댑터를 사용 하 여 SSIS에서 OLE DB 데이터 원본을 사용 하면 데이터가 손상 될 수 있습니다. 원본 테이블에 SQL 데이터 정렬을 사용 하는 char 또는 varchar 열이 포함 된 경우에는 ADO.NET 원본을 사용 하는 것이 좋습니다. 

  
## <a name="Locks"></a>잠금 동작  
Integration Services를 사용 하 여 데이터를 로드 하는 경우 SQL ServerPDW는 행 수준 잠금을 사용 하 여 대상 테이블의 데이터를 업데이트 합니다. 따라서 각 행이 업데이트될 때는 각 행에 대한 읽기 및 쓰기가 잠깁니다. 데이터가 준비 테이블에 로드될 때는 대상 테이블의 행이 잠기지 않습니다.  
  
## <a name="Examples"></a>예  
  
### <a name="Walkthrough"></a>A. 플랫 파일에서 간단히 로드  
다음 연습에서는 Integration Services를 사용 하 여 SQL Server PDW 어플라이언스로 플랫 파일 데이터를 로드 하는 간단한 데이터 로드를 보여 줍니다.  이 예에서는 Integration Services 이미 클라이언트 컴퓨터에 설치 되어 있고 SQL Server PDW 대상이 위에 설명 된 대로 설치 되어 있다고 가정 합니다.  
  
이 예에서는 다음 DDL이 있는 `Orders` 테이블에 로드 합니다. `Orders` 테이블은 `LoadExampleDB` 데이터베이스의 일부입니다.  
  
```sql  
CREATE TABLE LoadExampleDB.dbo.Orders (  
   id INT,  
   city varchar(25),  
   lastUpdateDate DATE,  
   orderDate DATE)  
;  
```  
  
로드 데이터는 다음과 같습니다.  
  
```  
id        city           lastUpdateDate     orderdate  
--------- -------------- ------------------ ----------  
1         Seattle        2010-05-01         2010-01-01  
2         Denver         2002-06-25         1999-01-02  
```  
  
로드 준비 중에 로드 데이터를 포함 하는 `exampleLoad.txt`플랫 파일을 만듭니다.  
  
```  
id,city,lastUpdateDate,orderDate  
1,Seattle,2010-05-01,2010-01-01  
2,Denver,2002-06-25,1999-01-02  
```  
  
먼저 다음 단계를 수행 하 여 Integration Services 패키지를 만듭니다.  
  
1.  SQL Server Data Tools \(SSDT\)에서 **파일**, **새로 만들기**, **프로젝트**를 차례로 선택 합니다. 나열 된 옵션에서 **Integration Services 프로젝트** 를 선택 합니다. 이 프로젝트 `ExampleLoad`의 이름을로, **확인**을 클릭 합니다.  
  
2.  **제어 흐름** 탭을 클릭 한 다음 **도구 상자** 의 **데이터 흐름 태스크** 를 **제어 흐름** 창으로 끌어 놓습니다.  
  
3.  **데이터 흐름** 탭을 클릭 한 다음 **도구 상자** 에서 **데이터 흐름** 창으로 **플랫 파일 원본** 을 끌어 옵니다. 방금 만든 상자를 두 번 클릭 하 여 **플랫 파일 원본 편집기**를 엽니다.  
  
4.  **연결 관리자** 를 클릭 한 다음 **새로 만들기**를 클릭 합니다.  
  
5.  **연결 관리자 이름** 상자에 연결의 이름을 입력 합니다. 이 예에서는 `Example Load Flat File CM`입니다.  
  
6.  **찾아보기** 를 클릭 하 고 `ExampleLoad.txt` 로컬 컴퓨터에서 파일을 선택 합니다.  
  
7.  플랫 파일에는 열 이름이 있는 행이 포함 되어 있으므로 **첫 번째 데이터 행 상자에서 열 이름을** 클릭 합니다.  
  
8.  왼쪽 열에서 **열** 을 클릭 하 고 로드 되는 데이터를 미리 보고 열 이름과 데이터가 올바르게 해석 되었는지 확인 합니다.  
  
9. 왼쪽 열에서 **고급** 을 클릭 합니다. 각 열 이름을 클릭 하 여 데이터와 연결 된 데이터 형식을 검토 합니다. 로드 된 데이터의 데이터 형식이 대상 열 유형과 호환 되도록 상자에 변경 내용을 입력 합니다.  
  
10. **확인** 을 클릭 하 여 연결 관리자를 저장 합니다.  
  
11. **확인** 을 클릭 하 여 **플랫 파일 원본 편집기**를 종료 합니다.  
  
데이터 흐름의 대상을 지정 합니다.  
  
1.  **도구 상자** 에서 **데이터 흐름** 창으로 **SQL Server PDW 대상을** 끌어 옵니다.  
  
2.  방금 만든 상자를 두 번 클릭 하 여 **SQL Server PDW 대상 편집기**를 로드 합니다.  
  
3.  **연결 관리자**옆에 있는 아래쪽 화살표를 클릭 합니다.  
  
4.  **새 연결 만들기를**선택 합니다.  
  
5.  서버, 사용자, 암호 및 대상 데이터베이스에 대 한 정보를 기기와 관련 된 정보로 입력 합니다. 예를 들면 다음과 같습니다. 그런 다음 **확인**을 클릭합니다.  
  
    InfiniBand 연결의 경우 **서버 이름**: <어플라이언스-이름>-SQLCTL01, 17001를 입력 합니다.  
  
    이더넷 연결의 경우 **서버 이름**: 제어 노드 클러스터의 IP 주소, 쉼표, 포트 17001을 입력 합니다. 예: 10.192.63.134, 17001.  
  
    **정의**`user1`  
  
    **암호**`password1`  
  
    **대상 데이터베이스:**`LoadExampleDB`  
  
6.  대상 테이블을 선택 `Orders`합니다.  
  
7.  로드 모드로 **추가** 를 선택 하 고 **확인**을 클릭 합니다.  
  
원본에서 대상으로 데이터 흐름을 지정 합니다.  
  
1.  **데이터 흐름** 창에서 **플랫 파일 원본** 상자의 녹색 화살표를 **SQL Server PDW 대상** 상자로 끌어 옵니다.  
  
2.  **SQL Server PDW 대상 편집기** 를 다시 표시 하려면 **SQL Server PDW 대상** 상자를 두 번 클릭 합니다. **매핑되지 않은 입력 열**아래에 왼쪽에 있는 플랫 파일의 열 이름이 표시 됩니다. **매핑되지 않은 대상 열**아래의 오른쪽에 있는 대상 테이블의 열 이름이 표시 됩니다. **매핑되지 않은 입력 열** 및 **매핑되지 않은 대상 열** 목록에서 일치 하는 열 이름을 끌어서 두 번 클릭 하 여 열을 **매핑된 열** 상자에 매핑합니다. **확인** 을 클릭 하 여 설정을 저장 합니다.  
  
3.  **파일** 메뉴에서 **저장** 을 클릭 하 여 패키지를 저장 합니다.  
  
Integration Services 컴퓨터에서 패키지를 실행 합니다.  
  
1.  Integration Services**솔루션 탐색기** (오른쪽 열)에서 마우스 오른쪽 단추를 클릭 `Package.dtsx` 하 고 **실행**을 선택 합니다.  
  
2.  패키지가 실행 되 고 진행률과 모든 오류가 **진행률** 창에 표시 됩니다. SQL 클라이언트를 사용 하 여 부하를 확인 하거나 SQL Server PDW 관리 콘솔을 통해 부하를 모니터링할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[SSIS PDW 대상 어댑터를 사용 하는 스크립트 태스크 만들기](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
[패키지 디자인 및 구현(Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx)  
[자습서: 마법사를 사용하여 기본 패키지 만들기](https://technet.microsoft.com/library/ms365330\(v=sql11\).aspx)  
[시작 (Integration Services)](https://go.microsoft.com/fwlink/?LinkId=202412)  
[동적 패키지 생성 샘플](https://go.microsoft.com/fwlink/?LinkId=202413)  
[병렬 처리를 위한 SSIS 패키지 디자인(SQL Server 비디오)](https://msdn.microsoft.com/library/dd795221.aspx)  
[Microsoft SQL Server 커뮤니티 예제: Integration Services](https://go.microsoft.com/fwlink/?LinkId=202415)  
[변경 데이터 캡처를 사용하여 증분 로드 개선](../integration-services/change-data-capture/change-data-capture-ssis.md)  
[느린 변경 차원 변환](../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)  
[대량 삽입 태스크](../integration-services/control-flow/bulk-insert-task.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->
