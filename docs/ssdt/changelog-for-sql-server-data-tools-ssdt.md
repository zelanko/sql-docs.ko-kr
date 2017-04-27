---
title: "SSDT(SQL Server Data Tools)에 대한 변경 로그 | Microsoft 문서"
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b071f8b8-c8e5-44e0-bbb6-04804dd1863a
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8798c5319cdce7b68f71868722aacfbf4cb34d9f
ms.lasthandoff: 04/11/2017

---
# <a name="changelog-for-sql-server-data-tools-ssdt"></a>SSDT(SQL Server Data Tools)에 대한 변경 로그
다음은 [SQL Server 2016](https://msdn.microsoft.com/library/ms130214.aspx)과 함께 출시된 [Visual Studio 2015용 SSDT(SQL Server Data Tools)](https://msdn.microsoft.com/library/mt204009.aspx)에 대한 변경 로그입니다.  
  
새로운 기능과 변경된 기능에 대한 자세한 게시물은 [SSDT 팀 블로그](https://blogs.msdn.microsoft.com/ssdt/)를 참조하세요.  

## <a name="ssdt-165-for-sql-server-2016"></a>SSDT 16.5(SQL Server 2016용)
릴리스됨: 2016년 10월 20일

빌드 번호: 14.0.61021.0

**새로운 기능**


### <a name="connection-improvements"></a>향상된 연결 기능

* **찾아보기** 탭의 새로운 검색 상자를 사용하면 로컬 서버, 네트워크 서버 및 Azure SQL Database를 필터링할 수 있습니다. 이 기능은 이러한 목록에 다수의 서버 또는 데이터베이스가 표시되는 경우에 유용합니다.
* **기록** 탭에는 즐겨찾기를 고정/고정 해제하는 마우스 오른쪽 단추 클릭 메뉴 옵션과 기록에서 연결을 제거하는 새 옵션이 있습니다.

### <a name="sqlpackage-and-dacfx-api-improvements"></a>SqlPackage 및 DacFx API 개선 사항

이제 SqlPackage.exe 및 DacFx API를 사용하여 배포 스크립트 및 배포 보고서를 생성한 다음 한 번에 모두 데이터베이스에 게시할 수 있습니다. 이 기능을 통해 배포 중 게시된 내용에 대한 보고서를 유지하려는 모든 사용자가 시간을 절약할 수 있습니다. 또 다른 이점은 Azure 시나리오에서 master 데이터베이스와 배포 대상 데이터베이스에 대해 별도 스크립트가 생성된다는 것입니다. 지금까지는 단일 스크립트가 생성되었으며 반복 배포에 효율적이지 않았습니다.

SqlPackage의 게시 및 스크립트 작업에 대해 새 인수 두 개가 추가되었습니다.

* DeployScriptPath(짧은 이름: dsp). 배포 스크립트를 작성할 선택적 경로입니다. Azure 배포의 경우 DB를 만들거나 수정하는 TSQL 명령이 있을 경우 마스터 스크립트가 동일한 경로에 작성되지만 "Filename_Master.sql"을 출력 파일 이름으로 사용합니다.
* DeployReportPath(짧은 이름: drp). 배포 보고서를 작성할 선택적 경로입니다.

스크립트 작업의 경우 기존 출력 경로 인수 또는 새 스크립트/보고서별 인수 중 하나를 사용해야 하며 둘 다 사용하면 안 됩니다.

사용법 예제:

**게시 작업**

```Sqlpackage.exe /a:Publish /tsn:(localdb)\ProjectsV13 /tdn:MyDatabase /deployscriptpath:”My\DeployScript.sql” /deployreportpath:”My\DeployReport.xml”```

**스크립트 작업**

```Sqlpackage.exe /a:Script /tsn:(localdb)\ProjectsV13 /tdn:MyDatabase /deployscriptpath:”My\DeployScript.sql” /deployreportpath:”My\DeployReport.xml”```

DacFx에서 DacServices.Publish() 및 DacServices.Script()라는 새 API 두 개가 추가되었습니다. 이러한 API를 통해 게시 + 스크립트 + 보고서 작업의 동시 수행도 지원합니다. 사용법 예제:

```
DacServices service = new DacServices(connectionString);
using(DacPackage package = DacPackage.Load(@"C:\My\db.dacpac")) {
var options = new PublishOptions() {
    GenerateDeploymentScript = true, // Should a deployment script be created?
    GenerateDeploymentReport = true, // Should an xml deploy report be created?
    DatabaseScriptPath = @"C:\My\OutputScript.sql", // optional path to save script to
    MasterDbScriptPath = @"C:\My\OutputScript_Master.sql", // optional path to save master script to
    DeployOptions = new DacDeployOptions()
};

// Call publish and receive deployment script & report in the results
PublishResult result = service.Publish(package, "TargetDb", options);
Console.WriteLine(result.DatabaseScript);
Console.WriteLine(result.MasterDbScript);
Console.WriteLine(result.DeploymentReport);

// Call script and receive deployment script & report in results
result = service.Script(package, "TargetDb", options);
Console.WriteLine(result.DatabaseScript);
Console.WriteLine(result.MasterDbScript);
Console.WriteLine(result.DeploymentReport);
```

**Analysis Services 및 Reporting Services**

SSAS 테이블 형식 디자이너 DAX 파서에서 큰 DAX 식으로 작업할 때 성능이 향상되었습니다.
자세한 내용은 [Analysis Services 블로그 게시물](https://blogs.msdn.microsoft.com/analysisservices/2016/09/20/introducing-integrated-workspace-mode-for-sql-server-data-tools-for-analysis-services-tabular-projects-ssdt-tabular/)을 참조하세요.

### <a name="fixed--improved-this-month"></a>이번 달 수정/향상됨

**데이터베이스 도구**

* [연결 버그 3055711](https://connect.microsoft.com/SQLServer/feedback/details/3055711/columns-cannot-be-selected-from-cross-apply-openjson-with-explicit-schema) – 명시적 스키마를 사용하여 CROSS APPLY OPENJSON에서 열을 선택할 수 없습니다.
* 수정됨 - 재배포 시 DacFx에서 인덱스가 삭제되는 자동 생성 기록 테이블 인덱스 문제
* 수정됨 – DacFx 일괄 처리 파서에서 이스케이프된 대괄호 ']' 문자를 구문 분석하지 않아 게시에 실패하는 문제
* 향상됨 – 이제 SqlPackage의 도움말 출력에 각 작업에 대한 설명이 포함되어 있음
* 수정됨 - 고급 옵션을 편집할 때와 게시, 스키마 비교 및 기타 파일에 저장된 연결 문자열을 편집할 때 연결 대화 상자의 "암호 저장" 옵션이 유지되지 않았음
* 수정됨 – IntegratedAuthentication=true인, 기록 탭에 표시된 연결의 경우 연결 속성의 인증 필드가 비어 있었음. 이제 "Windows 인증"이 예상대로 표시됨
* 수정됨 – 도구 -> 옵션 -> 텍스트 편집기 아래의 SQL Server Tools Intellisense 설정에 대한 변경 내용이 유지되지 않았음
* 향상됨 - 이제 연결 대화 기록 탭의 고정/고정 해제 단추가 더 간단해져 스크롤 막대가 나타날 가능성이 감소함
* 수정됨 - 연결 대화 상자의 여러 접근성 문제가 수정됨

**Analysis Services 및 Reporting Services**

* 데이터 표에서 스크롤 막대 위치 조정 컨트롤을 클릭할 경우 특정 상황에서 작동이 중단되는 SSDT AS 테이블 형식 디자이너의 문제가 수정됨
* SSDT AS 테이블 형식에서 현재 사용자로 연결을 가장하는 옵션을 사용할 수 없는 문제가 수정됨
* 수식 입력줄을 너무 멀리 확장할 경우 프로젝트를 다시 열 수 없는 SSDT AS 테이블 형식 디자이너의 문제가 수정됨
* 테이블 탭이 선택된 경우 키를 누를 때 발생하는 SSDT AS 테이블 형식 디자이너의 작동 중단이 수정됨
* Excel의 분석 기능이 하위 수준 AS 서버 버전에 연결하지 못하는 SSDT AS 프로젝트의 문제가 수정됨

**통합 서비스**

* 연결 버그 [1608896](https://connect.microsoft.com/SQLServer/feedback/details/1608896/move-multiple-integration-service-package-tasks) 수정됨: 여러 통합 서비스 패키지 작업 이동





## <a name="ssdt-164-for-sql-server-2016"></a>SSDT 16.4(SQL Server 2016용)
릴리스됨: 2016년 9월 20일

빌드 번호: 14.0.60918

**새로운 기능**

이제 스키마 비교가 SqlPackage.exe 및 DacFx(데이터 계층 응용 프로그램 프레임워크) API에서 지원됩니다. 자세한 내용은 [SqlPackage 및 데이터 계층 응용 프로그램 프레임워크의 스키마 비교](https://blogs.msdn.microsoft.com/ssdt/2016/09/20/schema-compare-in-sqlpackage-and-the-data-tier-application-framework-dacfx/)를 참조하세요.

**Analysis Services – SSDT 테이블 형식에 대한 통합 작업 영역 모드(SSAS)**

이제 SSDT 테이블 형식에 통합 작업 영역 모드를 사용할 경우 SSDT 테이블 형식이 백그라운드에서 자동으로 시작되는 내부 SSAS 인스턴스가 포함되어 있으므로 외부 작업 영역 서버 인스턴스를 제공할 필요 없이 모델 디자이너에서 테이블, 열 및 데이터를 추가하고 볼 수 있습니다. 통합 작업 영역 모드에서는 SSDT 테이블 형식이 작업 영역 서버 및 데이터베이스에서 작동하는 방식은 변경하지 않습니다. SSDT 테이블 형식이 작업 영역 데이터베이스를 호스트하는 위치만 변경합니다. 통합 작업 영역 모드를 사용하려면 새 테이블 형식 프로젝트를 만들 때 표시되는 테이블 형식 모델 디자이너 대화 상자에서 통합 작업 영역 옵션을 선택합니다. 현재 명시적 작업 영역 서버를 사용하는 기존 테이블 형식 프로젝트의 경우 솔루션 탐색기에서 Model.bim 파일을 선택할 때 표시되는 속성 창에서 통합 작업 영역 모드 매개 변수를 True로 설정하여 통합 작업 영역 모드로 전환할 수 있습니다. 자세한 내용은 [Analysis Services 블로그 게시물](https://blogs.msdn.microsoft.com/analysisservices/2016/09/20/introducing-integrated-workspace-mode-for-sql-server-data-tools-for-analysis-services-tabular-projects-ssdt-tabular/)을 참조하세요.

**업데이트 및 수정**
**데이터베이스 도구:**

- [연결 문제 3087775](https://connect.microsoft.com/SQLServer/feedback/details/3087775): VS Data Tools 7월 업데이트 14.0.60629.0에서 임시 테이블이 손상됨, "값은 null일 수 없습니다. 매개 변수 이름: reportedElement"
- [연결 문제 1026648](https://connect.microsoft.com/SQLServer/feedback/details/1026648): IsPersistedNullable이 SSDT 비교에서 서로 다른 것으로 표시됨
- [연결 문제 2054735](https://connect.microsoft.com/SQLServer/feedback/details/2054735): BACPAC를 가져올 때 ID가 다시 설정됨
- [연결 문제 2900167](https://connect.microsoft.com/SQLServer/feedback/details/2900167): SSDT 단위 테스트를 실행할 경우 임시 파일이 남겨짐
- [연결 문제 1807712](https://connect.microsoft.com/SQLServer/feedback/details/1807712): 이전 버전과의 호환성 중단 - AppLocal 및 Nugetization

**Analysis Services 및 Reporting Services**

* DirectQuery 계산된 열에 대한 DAX를 편집할 때 오류 팁 팝업이 방해가 되었던 SSDT의 문제가 수정되었습니다.
* Windows 배율 인수가 높은 DPI 200% 이상으로 설정된 경우 KPI 아이콘이 측정값 표에 표시되지 않는 SSDT AS 테이블 형식 표의 문제가 수정되었습니다.
* 큰 테이블 데이터를 붙여넣을 경우 테이블 형식 프로젝트가 응답을 중단할 수 있는 SSDT AS의 문제가 수정되었습니다.
* 연결 이름을 바꿀 때 변경 내용 저장 필요로 모델을 표시하기 위한 SSDT AS 테이블 형식 모델 편집기의 문제가 수정되었습니다.
* 관계 관리 대화 상자의 열 너비 크기를 조정할 수 없는 SSDT AS 테이블 형식 프로젝트의 문제가 수정되었습니다.
* 독일어 등의 로캘 설정으로 Excel에서 데이터를 붙여넣을 경우 쉼표가 소수 구분 기호로 제대로 처리되지 않는 SSDT AS 테이블 형식 1200 수준 모델의 문제가 수정되었습니다.
* SSDT AS 프로젝트에서 "이 시각적 개체에 대한 데이터를 검색할 수 없습니다." 오류가 발생할 수 있는 몇 가지 KPI 아이콘 집합과 관련된 문제가 수정되었습니다.
* 높은 DPI 배율에서 크기를 조정할 때 SSDT AS 프로젝트 속성 대화 상자를 제대로 고정하기 위한 문제가 수정되었습니다.
* 붙여넣은 테이블이 포함된 특정 모델을 업그레이드할 때 오류를 초래할 수 있는 SSDT AS 프로젝트의 문제가 수정되었습니다.
* Excel에서 전체 시트 행을 붙여넣을 경우 속도가 느려지고 원치 않는 열이 많이 생성되는 SSDT AS의 문제가 수정되었습니다.
* 큰 정적 DataTable 식을 구문 분석하고 강조 표시할 경우 속도가 느려지거나 중단된 것처럼 보이는 SSDT AS의 문제가 수정되었습니다.
* 편집기에서 선택한 현재 큐브 뷰에 측정값 및 KPI 값을 추가하기 위한 SSDT AS의 문제가 수정되었습니다.
* SQL Azure에서 AS 프로젝트로 데이터를 가져올 때 "dbo" 이외의 스키마 형식이 지원되지 않는 SSDT의 문제가 수정되었습니다.



## <a name="ssdt-163-for-sql-server-2016"></a>SSDT 16.3(SQL Server 2016용)
릴리스됨: 2016년 8월 15일

빌드 번호: 14.0.60812.0  

**새로운 기능**

- **릴리스 버전 관리 및 번호 매기기:** 이제 릴리스에 월별이 아니라 번호로 태그가 지정됩니다. 이 변경 내용은 새 SSMS 정책에 부합하며 한 달에 여러 개의 릴리스 또는 핫픽스가 있는 경우를 간소화합니다. 이 릴리스는 16.3으로, RTM 릴리스 후 세 번째 업데이트를 의미합니다. 모든 핫픽스는 16.3.1 등으로 지정되며, 다음 달에 계획된 다음 업데이트는 16.4가 됩니다.
- **Analysis Services - 테이블 형식 모델 탐색기:** 테이블 형식 모델 탐색기를 사용하면 데이터 원본, 테이블, 측정값, 관계 등 모델의 다양한 메타데이터 개체를 편리하게 탐색할 수 있습니다. Visual Studio에서 보기 메뉴를 열고 다른 창을 가리킨 다음 테이블 형식 모델 탐색기를 클릭하면 표시할 수 있는 별도 도구 창으로 구현됩니다. 테이블 형식 모델 탐색기는 기본적으로 솔루션 탐색기 영역의 별도 탭에 표시됩니다. 테이블 형식 모델 탐색기는 테이블 형식 1200 모델의 스키마와 매우 비슷한 트리 구조로 메타데이터 개체 및 많은 새로운 기능을 구성합니다.
- **데이터베이스 도구 – Always Encrypted**: 이 릴리스에서는 데이터베이스 프로젝트 또는 SQL Server 개체 탐색기의 라이브 데이터베이스에 열 마스터 키 열 또는 열 암호화 키를 쉽게 추가할 수 있도록 새로운 [Always Encrypted 키 관리](https://msdn.microsoft.com/library/mt708953.aspx) 대화 상자를 제공합니다. 이 릴리스에서는 Windows 인증서 저장소의 인증서를 지원합니다. 이후 릴리스에서는 Azure Key Vault 및 CNG 공급자가 지원될 예정입니다.
    - 열 마스터 키 또는 열 암호화 키를 만드는 동안 데이터베이스 업데이트를 클릭한 후 즉시 변경 내용이 SQL Server 개체 탐색기에 반영되지 않을 수도 있습니다. 문제를 해결하려면 SQL Server 개체 탐색기에서 데이터베이스 노드를 새로 고칩니다.
    - SQL Server 개체 탐색기에서 데이터가 포함된 테이블의 열을 암호화하려는 경우 오류가 발생할 수 있습니다. 이 기능은 현재 SSDT 데이터베이스 프로젝트 및 SSMS에서만 지원됩니다. SQL Server 개체 탐색기에 대한 지원은 이후 릴리스에서 사용할 수 있습니다.


**업데이트 및 수정**
* **데이터베이스 도구**
    - **SSDT:**
        - 연결 버그 1898001 [128자까지만 입력할 수 있는 열 설명 문제가 수정](https://connect.microsoft.com/SQLServer/feedback/details/1898001/column-description-limited-to-128-characters)되었습니다.
        - VS에서 데이터베이스를 게시할 경우 게시 프로필 xml의 DatabaseServiceObjective 속성이 적용되지 않는 문제가 수정되었습니다.
        - 연결 버그 2900167 [임시 파일이 잘못 남겨지는 단위 테스트 문제가 수정](http://connect.microsoft.com/SQLServer/feedback/details/2900167/running-ssdt-unit-tests-leaves-temp-files-behind)되었습니다.
        - 데이터베이스 설정의 보존 기간 콤보 상자가 잘리는 문제가 수정되었습니다.
        - 암호를 변경하는 동안 SQL CLR 프로젝트 속성의 빈 기존 암호가 확인되지 않는 문제가 수정되었습니다.
    - **DACFx:**
        - SqlAzureV12 오류에 대해 DACFx 호환성 수준이 업데이트되지 않는 문제가 수정되었습니다.
        - IsAutoGeneratedHistoryTable 속성이 모델 비교에서 잘못 제외되는 문제가 수정되었습니다.

- **Analysis Services 및 Reporting Services**
    - **SSDT:**
        - 서버 연결이 끊어진 경우 테이블 형식 모델을 저장할 수 없는 문제가 수정되었습니다.
        - AS의 가능한 무한 루프 문제로 인해 SSDT가 응답하지 않는 문제가 수정되었습니다.
        - 식을 커밋하는 방법에 따라 일관성 없는 동작이 발생하는 DAX 식 문제가 수정되었습니다.
        - KPI를 만들 때 VS 작동이 중단되는 문제가 수정되었습니다.
        - SQL Server 2008 R2, 2012 및 2014에 대해 잘못된 보고서를 생성하는 문제가 수정되었습니다.
        - .dwpro 프로젝트에 대해 무한 루프 오류를 발생시키는 계층 구조 순서 문제가 수정되었습니다.
        - RDL 다운그레이드 시 전체를 다시 빌드해야 해서 사용자에게 혼동을 주는 RS RDL 문제가 수정되었습니다.
        - 클라이언트 도구에서 숨기기가 적용되지 않는 KPI 문제가 수정되었습니다.
        

 
  
## <a name="ssdt-july-for-sql-server-2016"></a>SSDT 7월(SQL Server 2016용)  
릴리스됨: 2016년 6월 30일  
  
빌드 번호: 14.0.60629.0  
  
**새로운 기능**  
* **Always Encrypted 지원:** Always Encrypted 열이 포함된 데이터베이스의 경우 이 릴리스에서는 핵심 API 및 명령줄 도구(SqlPackage.exe)를 통해 Always Encrypted가 완전히 지원됩니다. 모든 Always Encrypted 기능을 완전히 지원하는 데이터베이스 프로젝트를 빌드하고 게시할 수 있습니다.  
* **임시 테이블 지원 향상:** 변경 전에 임시 테이블을 연결 해제하고 완료된 후 다시 연결하여 환경을 간소화했습니다. 즉, 지원되는 작업의 경우 임시 테이블에 다른 테이블 형식(표준, 메모리 내)의 패리티가 있습니다. 
* **SqlPackage.exe 및 설치 변경 내용:** SQL Server 엔진 및 SSMS 업데이트에서 SSDT를 격리하는 변경 내용입니다. 자세한 내용은 [SSDT와 SqlPackage.exe 설치 및 업데이트에 대한 변경 내용](https://blogs.msdn.microsoft.com/ssdt/2016/06/30/changes-to-ssdt-and-sqlpackage-exe-installation-and-updates/)을 참조하세요.

 

**업데이트 및 수정**
* **데이터베이스 도구**
    * 이제 SSDT에서 데이터베이스의 TDE(투명한 데이터 암호화)를 해제하지 않습니다. 이전에는 프로젝트 데이터베이스 설정의 기본 암호화 옵션이 사용하지 않도록 설정되었으므로 암호화가 꺼졌습니다. 이 수정을 통해 게시 중에 암호화를 사용하도록 설정할 수 있지만 해제할 수는 없습니다. 
    * 초기 연결 중 Azure SQL DB 연결에 대한 다시 시도 횟수와 복원력이 증가되었습니다.
    * 기본 파일 그룹이 PRIMARY가 아닌 경우 Azure V12로 가져오기/게시에 실패했습니다. 이제 게시할 때 이 설정이 무시됩니다.
    * 따옴표 붙은 식별자가 설정된 개체를 포함하는 데이터베이스를 내보낼 경우 일부 인스턴스에서 내보내기 유효성 검사에 실패할 수 있는 문제가 수정되었습니다.
    * TEXTIMAGE_ON 옵션이 이 옵션을 사용할 수 없는 Hekaton 테이블 생성에 대해 잘못 추가되는 문제가 수정되었습니다.
    * 대량 데이터를 내보내는 경우 데이터 단계가 완료된 후 model.xml 파일에 쓸 때 .bacpac 파일의 내용이 다시 작성되어 내보내는 데 시간이 오래 걸리는 문제가 수정되었습니다.
    * 사용자가 Azure SQL DW 및 APS 연결에 대한 보안 폴더에 표시되지 않는 문제가 수정되었습니다.


 * **Analysis Services 및 Reporting Services**
    * 32비트 공급자만 설치되어 SQL Server 2014에 연결하는 64비트 Excel 2016에 영향을 주는 MSOLAP OLEDB 공급자 관련 SxS 문제가 수정되었습니다(Office365의 ClickOnce 설치에서는 재현되지 않고 MSI Excel 설치에서만 재현됨).
    * 비정상적인 상황이 더 안정적으로 처리되도록, 붙여넣은 테이블이 있는 AS 모델을 1103에서 1200 호환성 수준으로 업그레이드할 경우 "관계에서 잘못된 열 ID를 사용합니다." 오류가 발생할 수 있는 문제가 수정되었습니다.
    * SSDT 2015(카트리지 공유 레지스트리 설정)를 제거한 후 동일한 컴퓨터의 SSDT-BI 2013이 AS 모델의 데이터를 더 이상 가져올 수 없는 SxS 문제가 수정되었습니다.
    * AS 엔진에 대한 연결이 끊어진 문제\작동 중단(즉, SSDT가 야간에 계속 열려 있었으며 AS 서버가 재활용된 경우 또는 연결이 일시적으로 끊어진 다른 경우)이 더 안정적으로 처리되도록 향상되었습니다. 
    * 다중 모니터 시나리오에서 대화 상자가 VS가 아닌 다른 화면에서 열리는 문제가 수정되었습니다. 
    * AS 모델 붙여넣은 테이블에서, HTML 테이블(표 형태 데이터)에서 붙여넣기 지원이 수정/활성화되었습니다. 
    * 업그레이드 시 빈 붙여넣은 테이블을 1200으로 업그레이드하지 못하는 문제가 해결되었습니다(측정값에 대한 컨테이너 테이블로만 사용됨). 
    * CalcTable(1200에서 붙여넣은 테이블에 사용됨)과 관련된 AS 엔진 문제를 해결하여 업그레이드 후 새 계산된 테이블에서 전체 프로세스를 수행하기 위해 붙여넣은 테이블이 포함된 AS 테이블 형식 모델을 1200으로 업그레이드하는 경우와 관련된 문제가 수정되었습니다. 
    * 불완전한 DAX 식을 사용하여 새 AS 1200 모델 계산된 테이블을 만드는 작업을 취소할 경우 작동이 중단될 수 있는 문제가 수정되었습니다. 
    * DB 이름과 테이블 이름이 같을 때 AS 서버에서 SSDT AS 프로젝트로 1200 모델을 가져오는 경우와 관련된 문제가 수정되었습니다. 
    * 1103 테이블 형식 모델에서 KPI 측정값을 편집하는 경우와 관련된 문제가 수정되었습니다. 
    * AS 1200 모델에 대한 표에 KPI 측정값을 붙여넣는 동안 발생하는 개체 참조가 설정되지 않음 예외가 수정되었습니다. 
    * 1200 모델의 다이어그램 보기에서 계산된 테이블의 열을 삭제할 수 없는 문제가 수정되었습니다. 
    * 코드 보기에서 model.bim 프로젝트 파일 속성을 볼 때 발생하는 개체 참조가 설정되지 않음 예외가 수정되었습니다. 
    * 테이블을 만들기 위해 AS 모델 그리드에 데이터를 붙여넣을 경우 쉼표를 소수 구분 기호로 사용하는 국제 로캘에서 잘못된 값이 생성되는 문제가 수정되었습니다. 
    * SSDT에서 2008 RS 프로젝트를 열고 업그레이드하지 않도록 선택하는 경우와 관련된 문제가 수정되었습니다. 
    * UI에서 서식 유형을 변경할 수 있도록 열 형식에 기본 서식을 사용하는 경우 1200 호환성 수준 모델 계산된 테이블 UI의 문제가 수정되었습니다. 
    

## <a name="ssdt-june-for-sql-server-2016"></a>SSDT 6월(SQL Server 2016용)  
릴리스됨: 2016년 6월 1일  
  
빌드 번호: 14.0.60525.0 

이제 SSDT GA(일반 공급)가 릴리스되었습니다. 2016년 6월의 SSDT GA 업데이트에서는 SQL Server 2016 RTM의 최신 업데이트 및 다양한 버그 수정 프로그램에 대한 지원이 추가되었습니다. 자세한 내용은 [2016년 6월의 SQL Server Data Tools GA 업데이트](https://blogs.msdn.microsoft.com/ssdt/2016/06/01/sql-server-data-tools-ga-update-for-june-2016/)를 참조하세요.

      

## <a name="ssdt-april-for-sql-server-2016-rc3"></a>SSDT 4월(SQL Server 2016 RC3용)  
릴리스됨: 2016년 4월 15일  
  
빌드 번호: 14.0.60413.0  
  
**SQL Server 데이터베이스**  
* **Always Encrypted 지원:** Always Encrypted 열이 포함된 데이터베이스의 경우 SSDT 및 DacFx를 통해 이러한 데이터베이스를 보고 편집한 후 데이터베이스 프로젝트에서 데이터베이스에 게시할 수 있습니다. 열 암호화를 사용하는 열의 변경 지원은 이후 릴리스에서 제공될 예정입니다.  
* **연결 대화 상자 및 SQL Server 개체 탐색기:** 여러 가지 사항이 수정 및 향상되었습니다.  
    * 고급 연결 속성을 나열하는 세부 정보 페이지를 검사하여 여러 줄 상자에 전체 연결 문자열을 표시하고 높은 DPI 컴퓨터에 대한 지원을 향상했습니다.  
    * 자세한 연결 오류가 포함된 기존의 오류 대화 상자가 다시 제공됩니다. 이 대화 상자는 DBA 또는 CSS가 문제를 진단하는 데 필요한 정보를 얻을 수 있도록 보다 명확한 오류 메시지 및 스택 추적으로 로그인 정보를 진단할 때 도움이 됩니다.  
    * 최소한의 권한을 가진 사용자를 위해 연결 대화 상자 및 SQL Server 개체 탐색기에 데이터베이스 나열, 보안 폴더 보기 등과 관련된 많은 문제가 수정되었습니다.  
    * 모든 DB를 나열하기 위해 데이터베이스 노드를 확장하는 경우 Azure SQL DB 성능이 향상되었습니다.  
* **SSDT 설치 관리자:**  
    * 제거 시 .Net가 다운로드되는 문제가 수정되었습니다.  
    * 이제 설치 관리자 크기가 높은 DPI 컴퓨터에서 올바르게 설정됩니다.  
    * 최신 SQL Server 버전이 있는 경우 SSDT 설치를 차단하는 버전 확인이 제거되었습니다.  
    * 스키마 비교: Visual Studio에서 여러 항목을 선택/선택 취소하는 데 시간이 오래 걸리는 성능 문제가 수정되었습니다.  
    * SQL Server 2016의 x86 버전이 없으므로 x86 컴퓨터에서 LocalDB 2014를 사용할 수 있도록 지원됩니다.  
* **빌드 및 배포:**  
    * 계산된 열이 임시 테이블에서 지원되지 않는 문제가 수정되었습니다.  
    * Azure V12에 배포하는 경우 "단일 사용자 모드에서 배포 스크립트 실행" 옵션은 클라우드 시나리오에서 지원되지 않으므로 무시됩니다.  
  
  
## <a name="ssdt-hotfix-for-sql-server-2016-rc2"></a>SSDT 핫픽스(SQL Server 2016 RC2용)  
릴리스됨: 2016년 4월 5일  
  
빌드 번호: 14.0.60329.0  
  
이 빌드에는 SQL Server Integration Services에 대한 기능을 제공하는 SSDT 버전의 핫픽스가 포함되어 있습니다. SQL Server 2016의 Analysis Services 및 Reporting Services에서 빌드 14.0.60316.0을 사용할 수도 있습니다.   
  
이 핫픽스를 가져오려면 [이 블로그 게시물의 다운로드 링크](https://blogs.msdn.microsoft.com/ssdt/2016/04/05/ssdt-preview-update-rc2/)를 사용합니다.  
  
이 빌드의 SSDT를 사용하여 새 보고서를 작성하는 경우 보고서 개발자는 이 핫픽스에만 있는 SSRS 보고서의 일시적인 문제에 대한 [해결 방법 및 알려진 문제를 확인](https://blogs.msdn.microsoft.com/ssdt/2016/04/05/ssdt-preview-update-rc2/)합니다.  
  
## <a name="ssdt-hotfix-for-sql-server-2016-rc0"></a>SSDT 핫픽스(SQL Server 2016 RC0용)  
릴리스됨: 2016년 3월 18일  
  
빌드 번호: 14.0.60316.0  
  
이 빌드에는 SQL Server 2016 RC0에 대한 기능을 제공하는 SSDT 버전의 핫픽스가 포함되어 있습니다. 지금은 SSDT의 RC1 버전이 없습니다. SQL Server 2016의 RC0 또는 RC1에서 빌드 14.0.60316.0을 사용할 수 있습니다.  
      
## <a name="ssdt-february-2016-preview-for-sql-server-2016-rc0"></a>SSDT 2016년 2월 Preview(SQL Server 2016 RC0용)  
릴리스됨: 2016년 3월 7일  
  
빌드 번호: 14.0.60305.0  
  
-   **SQL Server 프로젝트 템플릿**  
  
    이 SSDT Preview 릴리스에 대한 알림이 없습니다. 이 릴리스의 다른 기능에 대해 알아보려면 [데이터베이스 엔진의 새로운 기능](https://msdn.microsoft.com/library/bb510411.aspx)을 참조하세요.  
  
-   **SSIS 패키지 프로젝트 템플릿**  
  
    SSIS 디자이너는 SQL Server 2016, 2014 또는 2012용 패키지를 만들고 유지 관리합니다. 새 템플릿의 이름이 파트로 바뀌었습니다. SSIS Hadoop 커넥터에서 ORC 형식을 지원합니다. 자세한 내용은 [Integration Services의 새로운 기능](https://msdn.microsoft.com/library/bb522534.aspx)을 참조하세요.  
  
-   **SSAS 프로젝트 템플릿(테이블 형식 모델 프로젝트)**  
  
    Analysis Services에 대한 이번 달 업데이트는 테이블 형식 모델의 표시 폴더를 지원하며, 이제 새 SQL Server 2016 호환성 수준으로 생성된 모든 모델이 SSIS 패키지에서 지원됩니다. 자세한 내용은 [Analysis Services의 새로운 기능(블로그 게시물)](http://blogs.msdn.com/b/analysisservices/archive/2016/01/28/what-s-new-for-sql-server-2016-analysis-services-in-ctp3-3.aspx)을 참조하세요.  
  
-   **SSRS 보고서 프로젝트 템플릿**  
  
    이 SSDT Preview 릴리스에 대한 알림이 없습니다. 이 릴리스의 다른 기능에 대해 알아보려면 [Reporting Services의 새로운 기능](https://msdn.microsoft.com/library/ms170438.aspx)을 참조하세요.  
  
## <a name="ssdt-january-2016-preview"></a>SSDT 2016년 1월 Preview  
릴리스됨: 2016년 2월 4일  
  
빌드 번호: 14.0.60203.0  
  
-   **SQL Server 프로젝트 템플릿**  
  
    이 SSDT Preview 릴리스에 대한 알림이 없습니다. 이 CTP의 다른 기능에 대해 알아보려면 [데이터베이스 엔진의 새로운 기능](https://msdn.microsoft.com/library/bb510411.aspx)을 참조하세요.  
  
-   **SSIS 패키지 프로젝트 템플릿**  
  
    ODBC 원본 및 대상 구성 요소, CDC 제어 작업,  
      CDC 원본 및 분할자 구성 요소, Microsoft Connector for SAP BW 및 Azure용 Integration Services 기능 팩에 대한 지원을 추가합니다. 자세한 내용은 [Integration Services의 새로운 기능](https://msdn.microsoft.com/library/bb522534.aspx)을 참조하세요.  
  
-   **SSAS 프로젝트 템플릿**  
  
    1200 호환성 수준의 표 형식 모델에 대한 향상된 기능, DirectQuery 모드의 모델에 대한 계산 열 및 행 수준 보안, 모델 메타데이터에 대한 변환, SSIS Analysis Services DDL 실행 태스크의 TMSL 스크립트 실행 및 많은 버그 수정을 포함합니다.  
    자세한 내용은 [Analysis Services의 새로운 기능(msdn)](https://msdn.microsoft.com/library/bb522628.aspx) 또는 [Analysis Services의 새로운 기능(블로그 게시물)](http://blogs.msdn.com/b/analysisservices/archive/2016/01/28/what-s-new-for-sql-server-2016-analysis-services-in-ctp3-3.aspx)을 참조하세요.  
  
-   **SSRS 보고서 프로젝트 템플릿**  
  
    이 SSDT Preview 릴리스에 대한 알림이 없습니다. 이 CTP의 다른 기능에 대해 알아보려면 [Reporting Services의 새로운 기능](https://msdn.microsoft.com/library/ms170438.aspx)을 참조하세요.  
  
## <a name="ssdt-december-2015-preview"></a>SSDT 2015년 12월 Preview  
  
-   **SQL Server 프로젝트 템플릿**은 연결 대화 상자, 최근 기록 목록, 데이터베이스 목록 로드 시 연결 속성에서 인증 컨텍스트 설정의 적절한 사용을 위한 버그 수정을 포함합니다.  
  
    -   테스트 연결 제한 시간 값이 15초로 변경됨  
  
    -   데이터베이스 목록을 로드할 때 클라이언트 IP가 등록되지 않은 경우 Azure SQL 데이터베이스 서버 방화벽 규칙 만들기  
  
    -   SQL Server 2016 CTP3.2에서 프로그래밍 지원 제공  
  
-   **SSAS 프로젝트 템플릿**은 모델에 이미 정의된 DAX 식 및 기타 개체를 기반으로 계산된 테이블을 만들 수 있는 기능을 추가합니다.  
  
-   **SSIS 패키지 프로젝트 템플릿** 추가 기능에는 Avro 파일 형식에 대한 SSIS Hadoop 커넥터 지원 및 Kerberos 인증이 포함됩니다.   
    SSIS 2012 및 2014에 대한 SSIS 디자이너 지원은 이 업데이트에 아직 포함되지 않았습니다.  
  
## <a name="ssdt-november-2015-preview"></a>SSDT 2015년 11월 Preview  
  
-   **SQL Server 프로젝트 템플릿** SQL Server 및 Azure SQL Database에 대한 연결 환경을 개선하는 Preview  
  
-   **SSIS 패키지 프로젝트 템플릿** SSIS 카탈로그 성능 향상: SSIS 관리자가 아닌 사용자를 위한 대부분의 대부분 SSIS 카탈로그 뷰의 성능에 대한 성능이 향상되었습니다.  
  
-   **SSAS 프로젝트 템플릿**은 Analysis Services의 표 형식 모델 프로젝트에 대한 향상된 기능을 포함합니다. **코드 보기** 명령을 사용하여 JSON에서 모델 정의를 볼 수 있습니다. 전체 기능을 갖춘 Visual Studio 2015 버전을 사용 중이지 않은 경우 JSON 편집기를 사용하려면 해당 버전이 필요합니다. [Visual Studio Community Edition](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)을 무료로 다운로드할 수 있습니다.  
  
## <a name="ssdt-october-2015-preview"></a>SSDT 2015년 10월 Preview  
  
-   BI용 새 프로젝트 템플릿(Analysis Services 모델, Reporting Services 보고서 및 Integration Services 패키지) 이제 모든 SQL Server 프로젝트 템플릿이 하나의 SSDT에 있음  
  
-   Hadoop 커넥터, 제어 흐름 템플릿, 데이터 흐름 작업의 최대 버퍼 크기 완화 등을 비롯한 새로운 SSIS 기능  
  
-   SQL Server 2016 CTP 3.0에서 관계형 데이터베이스 프로젝트에 대한 지원 제공  
  
-   SSIS의 다양한 버그 수정 및 Windows 7 OS 지원  
  
## <a name="ssdt-september-2015-preview"></a>SSDT 2015년 9월 Preview  
  
-   다중 언어 지원이 이 Preview에 새로 추가됨  
  
## <a name="ssdt-august-2015-preview"></a>SSDT 2015년 8월 Preview  
  
-   SSDT를 설치하기 위한 새로운 독립 실행형 Setup.exe 프로그램.  더 이상 SQL Server 설치 프로그램의 수정된 버전을 사용할 필요가 없습니다. 이 버전의 SSDT에는 SQL Server 또는 Azure SQL Database에 배포하는 관계형 데이터베이스를 구축하기 위한 프로젝트 템플릿이 포함되어 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server Data Tools 다운로드 &#40;SSDT&#41;](../ssdt/download-sql-server-data-tools-ssdt.md)  
[SQL Server Data Tools&#40;SSDT 및 SSDT-BI&#41;의 이전 릴리스](../ssdt/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md)  
[데이터베이스 엔진의 새로운 기능](https://msdn.microsoft.com/library/bb510411.aspx)  
[Analysis Services의 새로운 기능](https://msdn.microsoft.com/library/bb522628.aspx)  
[Integration Services의 새로운 기능](https://msdn.microsoft.com/library/bb522534.aspx)  
  

