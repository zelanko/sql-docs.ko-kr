---
title: SSDT(SQL Server Data Tools)에 대한 변경 로그 | Microsoft 문서
ms.custom: ''
ms.date: 09/27/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: b071f8b8-c8e5-44e0-bbb6-04804dd1863a
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 57e4a453952dc67bdb572697b0d20de2c15fa034
ms.sourcegitcommit: 5d6e1c827752c3aa2d02c4c7653aefb2736fffc3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "49072177"
---
# <a name="changelog-for-sql-server-data-tools-ssdt"></a>SSDT(SQL Server Data Tools)에 대한 변경 로그
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
다음은 [SSDT(SQL Server Data Tools)](download-sql-server-data-tools-ssdt.md)에 대한 변경 로그입니다.  
  
새로운 기능과 변경된 기능에 대한 자세한 게시물은 [SSDT 팀 블로그](https://blogs.msdn.microsoft.com/ssdt/)를 참조하세요.


## <a name="ssdt-for-visual-studio-2017-1581"></a>Visual Studio 2017용 SSDT(15.8.1)
빌드 번호: 14.0.16179.0  
릴리스 날짜: 2018년 9월 27일  

### <a name="whats-new"></a>새로운 기능

**SSIS:**

1. [!INCLUDE[sql-server-2019](..\includes\sssqlv15-md.md)]에 대한 지원을 추가합니다.
2. SQL Server 2012 지원을 제거합니다.

### <a name="known-issues"></a>알려진 문제:

- SSIS 패키지 실행 태스크는 ExecuteOutOfProcess가 True로 설정되었을 때 디버깅을 지원하지 않습니다. 이 문제는 디버깅에만 적용됩니다. DTExec.exe 또는 SSIS 카탈로그를 통한 저장, 배포 및 실행은 영향을 받지 않습니다.
- SSDT 15.8.1은 현재 Windows 7 SP1을 지원하지 않으므로 Windows 7 SP1을 사용 중인 경우 15.8.0을 계속 사용하세요.


## <a name="ssdt-for-visual-studio-2017-158"></a>Visual Studio 2017용 SSDT(15.8)
빌드 번호: 14.0.16174.0  
릴리스 날짜: 2018년 9월 5일  

### <a name="whats-new"></a>새로운 기능

**SSIS:**

1. VS 15.8에서 스크립트 작업/구성 요소 저장으로 컴파일 오류가 발생하는 재발을 수정합니다.
1. VS 15.8에서 배포 마법사가 작동하지 않는 재발을 수정합니다.
1. ADO.NET 연결 관리자가 타사 ADO.NET 공급자를 지원하지 않는 문제를 수정합니다.

**설치 관리자:**

- Windows 10에서 SSDT를 설치할 때 도중에 다시 부팅을 실행합니다.


### <a name="known-issues"></a>알려진 문제:

- SSIS 패키지 실행 태스크는 ExecuteOutOfProcess가 True로 설정되었을 때 디버깅을 지원하지 않습니다. 이 문제는 디버깅에만 적용됩니다. DTExec.exe 또는 SSIS 카탈로그를 통한 저장, 배포 및 실행은 영향을 받지 않습니다.




## <a name="ssdt-for-visual-studio-2017-1571"></a>Visual Studio 2017용 SSDT(15.7.1)
빌드 번호: 14.0.16167.0  
릴리스 날짜: 2018년 7월 2일  
  
### <a name="whats-new"></a>새로운 기능

**SSIS:**

- AS 작업에 사용할 새 Azure Government AAD 권한(login.microsoftonline.us)에 대한 지원을 추가합니다.
- AS 처리 작업 UI에 대상 서버 버전이 SQLServer2016인 경우 “메서드를 찾을 수 없음”이 표시되는 문제를 수정합니다.
- 대상 서버 버전이 SQLServer2012인 경우 일부 파이프라인 구성 요소를 실행할 수 없는 문제를 수정합니다.

**설치 관리자:**

- VS 인스턴스 목록을 필터링하여 SSDT를 설치할 수 없는 인스턴스를 제외합니다.

### <a name="known-issues"></a>알려진 문제:

- SSIS 패키지 실행 태스크는 ExecuteOutOfProcess가 True로 설정되었을 때 디버깅을 지원하지 않습니다. 이 문제는 디버깅에만 적용됩니다. DTExec.exe 또는 SSIS 카탈로그를 통한 저장, 배포 및 실행은 영향을 받지 않습니다.
- Windows 10에 SSDT를 설치하고 “Visual Studio 2017 인스턴스용 새 SQL Server Data Tools 설치”를 선택하면 “요청된 메타파일 작업이 지원되지 않는 경우” 설치가 실패합니다. 설치를 계속하려면 컴퓨터를 다시 부팅하고 SSDT 설치 관리자를 다시 시작하세요.



## <a name="ssdt-for-visual-studio-2017-1570"></a>Visual Studio 2017용 SSDT(15.7.0)
빌드 번호: 14.0.16165.0  
릴리스 날짜: 2018년 6월 4일  
  
### <a name="whats-new"></a>새로운 기능

**SSIS:**

- 옵션 대화 상자에서 *Integration Services 디자이너* 페이지를 올바르게 표시할 수 없는 문제를 해결합니다.  
- *정렬 변환 편집기* 편집기에서 표시되는 텍스트에 대한 명도 비율 문제를 해결합니다.  
- 콤보 상자를 편집하려고 할 때 *참조 확인* 대화 상자가 사라지는 문제를 해결합니다.  
- *Hadoop 연결 관리자*의 F1 도움말 링크가 작동하지 않는 문제를 해결합니다.  
- 스크립트 작업 코드가 SQL Server 2016을 대상으로 할 때 컨테이너에 있는 경우 손실되는 문제를 해결합니다.  


**설치 관리자:**

- SSRS 및 SSIS가 VS 15.7.2에 설치되기 전에 SSAS를 설치할 수 없는 문제를 해결합니다.

### <a name="known-issues"></a>알려진 문제:

- SSIS 패키지 실행 태스크는 *ExecuteOutOfProcess*가 *True*로 설정되었을 때 디버깅을 지원하지 않습니다. 이 문제는 디버깅에만 적용됩니다. DTExec.exe 또는 SSIS 카탈로그를 통한 저장, 배포 및 실행은 영향을 받지 않습니다.


## <a name="ssdt-for-visual-studio-2017-1560"></a>Visual Studio 2017용 SSDT(15.6.0)
빌드 번호: 14.0.16162.0  
릴리스 날짜: 2018년 4월 10일
  
### <a name="whats-new"></a>새로운 기능

**SSIS:**

- SQLServer2016 및 SQLServer2017을 대상으로 할 때 AS 처리 작업이 처리 단계를 기록하지 않는 문제를 해결합니다.
- SSDT에서 매우 긴 영어 외 작업 이름으로 dtsx를 열 때 액세스 위반이 발생하는 문제를 해결합니다.
- 작업 UI에서 간혹 ScriptTask 변수 목록이 사라지는 문제를 해결합니다.
- 패키지 위치가 SQL Server일 때 기존 패키지 사본 추가가 실패하는 문제 해결
- 일부 편집기 대화 상자에서 콤보 상자에 액세스할 때 포커스가 멈추는 문제를 해결합니다.
- VS 테마를 전환하는 동안 배경이 변경되지 않는 문제를 해결합니다.
- 어두운 테마에서 주석 및 로드 레이블이 보이지 않는 문제 해결
- SSIS 도구 상자 항목에 대해 상태 속성이 올바르게 정의되지 않는 문제를 해결합니다.
- WebServiceTask 실행에 항상 실패하는 문제를 해결합니다.
- 연결 문자열이 프로젝트 매개 변수에 종속적인 변수로 설정된 경우 패키지 배포가 실패하는 문제를 해결합니다.

**설치 관리자:**

- 개인정보 보호 고지 사항에 "SQL Server Data Tools에 대한 사용자 환경 개선 프로그램" 링크를 추가합니다.
- "Visual Studio 2017 인스턴스에 대한 새 SQL Server Data Tools 설치"를 선택할 때 VS 설치 관리자 창이 표시되는 문제를 해결합니다.

### <a name="known-issues"></a>알려진 문제:
- SSIS 패키지 실행 태스크는 ExecuteOutOfProcess가 True로 설정되었을 때 디버깅을 지원하지 않습니다. 이 문제는 디버깅에만 적용됩니다. DTExec.exe 또는 SSIS 카탈로그를 통한 저장, 배포 및 실행은 영향을 받지 않습니다.



## <a name="ssdt-for-visual-studio-2017-1552"></a>Visual Studio 2017용 SSDT(15.5.2)
빌드 번호: 14.0.16156.0
  
### <a name="whats-new"></a>새로운 기능

**SSIS**
- SSAS와 SSIS가 동일한 VS 2017 인스턴스에 설치된 경우 SSIS 2008 프로젝트 마이그레이션이 실패하는 문제를 수정합니다.
- Rdlc 보고서 디자이너와 SSIS가 동일한 VS 2017 인스턴스에 설치된 경우 Rdlc 프로젝트를 작성할 수 없는 문제를 수정합니다.
- 주석 색을 업데이트할 수 없는 문제를 수정합니다.
- Hadoop 연결 관리자 편집기의 일부 문자열이 다른 언어에서 잘리는 문제를 수정합니다.
- OData 연결 관리자 편집기에서 일부 문자열이 잘리는 문제를 수정합니다.
- Integration Services 가져오기 프로젝트 마법사 창에서 일부 문자열이 잘리는 문제를 수정합니다.
- SSIS 도구 상자 정보 창의 제목 문제를 수정합니다.
- Integration Services 배포 마법사 창에서 일부 문자열이 잘리는 문제를 수정합니다. 

**설치 관리자**
- 가끔씩 "지정한 파일을 찾을 수 없습니다(0x80070002)" 오류와 함께 페이로드 다운로드가 실패하는 문제를 해결합니다.  

### <a name="known-issues"></a>알려진 문제
- SSIS 패키지 실행 태스크는 *ExecuteOutOfProcess*가 *True*로 설정되었을 때 디버깅을 지원하지 않습니다. 이 문제는 디버깅에만 적용됩니다. DTExec.exe 또는 SSIS 카탈로그를 통한 저장, 배포 및 실행은 영향을 받지 않습니다.




## <a name="ssdt-for-visual-studio-2017-1551"></a>Visual Studio 2017용 SSDT(15.5.1)
빌드 번호: 14.0.16148.0
  
### <a name="whats-new"></a>새로운 기능

Visual Studio 2017(15.5.1)은 설치 관리자에 대한 다음과 같은 버그 수정을 제외하고 15.5.0 버전과 동일한 릴리스입니다.

1.  SQL Server Integration Services 사후 설치 시 설치 관리자가 응답하지 않는 문제를 수정했습니다.
2.  "요청된 메타 파일 작업이 지원되지 않습니다(0x800707D3)" 오류 메시지와 함께 설치가 실패하는 문제를 수정했습니다.

이러한 두 가지 버그 수정 외에도 15.5.0에 대한 다음과 같은 세부 사항이 15.5.1에 적용됩니다.

## <a name="ssdt-for-visual-studio-2017-1550"></a>Visual Studio 2017용 SSDT(15.5.0)
빌드 번호: 14.0.16146.0
  
### <a name="whats-new"></a>새로운 기능

Visual Studio 2017용 SSDT(15.5.0)가 미리 보기에서 GA(일반 공급)로 전환됩니다.

**설치 관리자**
1. 설치 UI가 지역화됩니다.
1. 아이콘이 더 높은 품질 버전으로 바뀝니다.

**IS(Integration Services)**
1. ADF에서 Azure SSIS IR에 배포할 때 사용하는 배포 마법사에서, Azure SSIS IR에서 실행되는 SSIS 패키지의 잠재적 호환성 문제를 검색하는 패키지 유효성 검사 단계가 추가되었습니다. 자세한 내용은 [Azure에 배포된 SSIS 패키지 유효성 검사](..\integration-services\lift-shift\ssis-azure-validate-packages.md)를 참조하세요.
1. SSIS 확장이 지역화됩니다.

### <a name="bug-fixes"></a>버그 수정

**IS(Integration Services)**
1. OLEDB 및 ADO.NET 연결 관리자의 레이아웃이 손상되는 문제를 수정했습니다.
2. 차원 처리 작업을 편집하려고 할 때 어셈블리를 찾을 수 없는 오류가 발생하는 문제를 수정했습니다.

### <a name="known-issues"></a>알려진 문제

**IS(Integration Services)** SSIS 패키지 실행 태스크는 ExecuteOutOfProcess가 True로 설정되었을 때 디버깅을 지원하지 않습니다. 이 문제는 디버깅에만 적용됩니다. DTExec.exe 또는 SSIS 카탈로그를 통한 저장, 배포 및 실행은 영향을 받지 않습니다.



## <a name="ssdt-174-for-visual-studio-2015"></a>Visual Studio 2015용 SSDT 17.4
빌드 번호: 14.0.61712.050

### <a name="whats-new"></a>새로운 기능

**AS(Analysis Services) 프로젝트**
- 테이블 형식 프로젝트에 세 개의 새로운 옵션이 추가되었습니다.(옵션 > Analysis Services 테이블 형식 > 데이터 가져오기).
  - 레거시 데이터 원본 사용 - 사용자가 최신 호환성 모드에서 이전 "1200 호환 모드" 데이터 원본을 만들 수 있습니다.
  - 자동 형식 검색 - 사용하도록 설정할 경우 최신 데이터 원본에 대한 쿼리 편집기는 구조화되지 않은 쿼리가 로드되면 이러한 쿼리의 데이터 형식을 검색하려고 시도합니다. 검색에 성공하면 쿼리에 새 단계가 추가될 수 있습니다.
  - 백그라운드 분석 실행 - 사용하도록 설정할 경우 최신 데이터 원본에 대한 쿼리 편집기는 쿼리의 출력 스키마를 분석하기 위해 쿼리가 로드되면 데이터 원본에 대해 쿼리를 실행합니다.

**IS(Integration Services)**
- ADF에서 Azure SSIS IR에 배포할 때 사용하는 배포 마법사에서, Azure SSIS IR에서 실행되는 SSIS 패키지의 잠재적 호환성 문제를 검색하는 패키지 유효성 검사 단계가 추가되었습니다. 자세한 내용은 [Azure에 배포된 SSIS 패키지 유효성 검사](..\integration-services\lift-shift\ssis-azure-validate-packages.md)를 참조하세요.


### <a name="bug-fixes"></a>버그 수정

**AS(Analysis Services) 프로젝트:**
- TFS로의 모델 변경을 확인할 때 처리되지 않은 예외가 발생할 수 있는 문제를 수정했습니다.
- 복잡한 M 식을 사용하여 1400 모델에 테이블을 추가할 때 예외가 발생하는 문제를 수정했습니다.
- 모델 다이어그램 보기에서 메타데이터를 검색할 때 Visual Studio에서 크래시가 발생할 수 있는 문제를 수정했습니다.
- 파티션 M 쿼리에 변경 내용을 저장하면 테이블 정의에서 계산 열이 제거되는 1400 모델 관련 문제를 수정했습니다.
- 데이터 가져오기/테이블 편집기 UI에서 1400 모델에 쿼리 이름 바꾸기를 사용할 때 현재 데이터 모델과의 호환성에 대한 유효성을 검사하는 중 동결되는 문제를 수정했습니다.
- Azure Analysis Service에 1400 모델을 배포할 때 Newtonsoft 어셈블리 참조가 누락되는 문제를 수정했습니다.
- 특정 상황에서 PQ를 통해 1400 모델로 데이터 가져오기 오류가 발생하는 문제를 수정했습니다.
- 창 크기 조정을 설정하면 나타나는 PowerQuery 사용자 인터페이스 대화 상자의 크기 조정 문제를 수정했습니다.
- 이름 바꾸기 관련 문제를 수정했습니다.
- 경우에 따라 변경 내용이 올바르게 저장/동기화되지 않는 프로젝트 구성 관련 문제를 수정했습니다.
- "형식 변경" 단계가 자동으로 추가되는 PowerQuery 편집기 문제를 수정했습니다.
- 통합 작업 영역 모드로 전환 후 BIM 파일을 열 때 오류가 발생하는 문제를 수정했습니다.
- 이제 MaxConnections 속성이 테이블 형식 모델의 데이터 원본에 대해 표시됩니다.
- PowerQuery 편집기 창의 초기 크기를 늘렸습니다.
- PowerQuery 편집기의 "Source" 같은 M 쿼리 키워드가 이제 지역화됩니다.
- 테이블을 편집할 때마다 동일한 자격 증명을 입력할 필요가 없도록 1400 모델 및 구조화된 데이터 원본을 작업할 때 자격 증명이 캐시됩니다.

**RS 프로젝트:**
- 다중 보고서 프로젝트에 단일 보고서를 배포할 수 없는 문제를 수정했습니다.
- 배포 시 문제를 일으킬 수 있는 공유 데이터 원본 관련 문제를 수정했습니다.
- 코드 보기, 디자인 보기 및 쿼리 편집기 창 사이에서 전환할 때 실행 취소 관리자에서 크래시가 발생하는 문제를 수정했습니다.
- 런타임 오류 이후 매개 변수 창이 사라지는 문제를 수정했습니다.
- 보고서 프로젝트의 원본 제어 매핑이 손실되는 문제를 수정했습니다.

**Integration Services:**
- Analysis Services 프로세스 작업에서 연결을 전환할 때 발생하는 문제를 수정했습니다.
- 일부 작업/구성 요소가 올바르게 지역화되지 않은 문제를 수정했습니다.
- \__$command\_id 열을 추가하는 CDC에 대한 SQL 픽스를 적용한 후 CDC 구성 요소가 중단되는 문제를 수정했습니다.


## <a name="ssdt-for-visual-studio-2017-1540-preview"></a>Visual Studio 2017용 SSDT(15.4.0 미리 보기)
빌드 번호: 14.0.16134.0
  
### <a name="whats-new"></a>새로운 기능

이 릴리스에서는 Visual Studio 2017 15.4 이상의 SQL Server Database, Analysis Services, Reporting Services 및 Integration Services 프로젝트에 대한 독립 실행형 웹 설치 관리자를 제공합니다.

### <a name="installer"></a>설치 관리자

- 사용자가 VS2017 인스턴스에 대한 새로운 SSDT를 설치할 때 애칭을 설정하도록 허용합니다.
- VS 인스턴스가 선택되지 않는 경우 설치 관리자의 기능 선택 확인란을 숨깁니다.
- 고객 의견에 따라 설치 관리자의 일부 메시지를 구체화합니다.
- 설치 관리자가 업그레이드를 지원하지 않는 문제를 해결했습니다.


### <a name="ssis"></a>SSIS

- Azure 기능 팩을 설치할 때 가져오기/내보내기 마법사에서 데이터 원본을 나열할 수 없는 문제를 해결했습니다.
- 연결을 변환하는 동안 SSIS Analysis 프로세스 태스크를 편집하면 예외가 throw되는 문제를 해결했습니다.
- __$command_id 열을 추가하는 SQL 수정 프로그램을 적용한 후 CDC 구성 요소가 손상되는 문제를 해결했습니다.
- 이전 SQL Server를 대상으로 타사 패키지를 편집 및 실행할 수 없는 문제를 해결했습니다.
- DTSWizard.exe를 두 번 클릭하고 플랫 파일 원본을 선택하면 플랫 파일 원본 구성 대화 상자가 올바르게 표시되지 않는 문제를 해결했습니다.
- SQL Server 2017을 대상으로 Azure 기능 팩 태스크/구성 요소가 포함된 패키지를 실행할 수 없는 문제를 해결했습니다.


**알려진 문제**

- 설치 프로그램이 지역화되지 않았습니다.
- SSIS 패키지 실행 태스크는 *ExecuteOutOfProcess*가 True로 설정되었을 때 디버깅을 지원하지 않습니다. 이 문제는 디버깅에만 적용됩니다. DTExec.exe 또는 SSIS 카탈로그를 통한 저장, 배포 및 실행은 영향을 받지 않습니다.


## <a name="ssdt-173-for-visual-studio-2015"></a>Visual Studio 2015용 SSDT 17.3
빌드 번호: 14.0.61709.290

### <a name="whats-new"></a>새로운 기능

**AS(Analysis Services)**

- Cosmos DB 및 HDI Spark는 1400 모델에서 활성화됩니다.
- 표 형식 데이터 원본 속성
- 이제 "빈 쿼리"는 1400 호환성 수준인 모델의 쿼리 편집기에서 새 쿼리를 만들기 위해 지원되는 옵션입니다.
- 이제 1400 모드 모델의 쿼리 편집기를 사용하면 새 테이블을 자동으로 처리하지 않고 쿼리를 저장할 수 있습니다.

**RS(Reporting Services)**

- 이제 프로젝트가 빌드하고 배포하는 데 MSBuild를 사용하도록 지원하는 업그레이드된 형식으로 열 때 메시지를 표시합니다.

### <a name="known-issues"></a>알려진 문제

**AS(Analysis Services)**

- 큐브 뷰를 가진 직접 쿼리 모드에서 1400 호환성 수준의 모델은 메타데이터를 쿼리하고 검색하는 데 실패합니다.

**RS(Reporting Services)**

- 새 보고서 프로젝트 형식은 소스 제어 바인딩을 유지하지 않고 메시지와 유사한 오류를 발생시킵니다.

   *프로젝트 파일 C:\path는 소스 제어에 바인딩되지 않지만 솔루션은 소스 제어 바인딩 정보를 포함합니다.*
 
   이 문제를 해결하려면 솔루션을 열 때마다 **솔루션 바인딩 사용**을 클릭합니다.

- 프로젝트를 새 MSBuild 형식으로 업그레이드한 후에 다음과 같은 메시지가 표시되며 저장에 실패합니다.

   *"매개 변수 "unevaluatedValue"는 null일 수 없습니다."*

   이 문제를 해결하려면 *프로젝트 구성*을 업데이트하고 *플랫폼* 속성을 채웁니다.

### <a name="bug-fixes"></a>버그 수정

**AS(Analysis Services)**

- 표 형식 모델 다이어그램 보기를 로드할 때 성능이 크게 향상되었습니다.
- 1400 호환성 수준 모델에서 PowerQuery 통합 및 환경을 향상하기 위해 다양한 문제를 해결했습니다.
   - 파일 원본에 편집 사용 권한을 방지하는 문제를 해결했습니다.
   - 파일 원본의 원본을 변경할 수 없는 문제를 해결했습니다.
   - 파일 원본에 잘못된 UI를 표시하는 문제를 해결했습니다.
- "날짜에 조인" 관계를 비활성 상태로 만들 때 "JoinOnDate" 속성을 제거하는 문제를 해결했습니다.
- 이제 쿼리 작성기에서 새 쿼리 옵션을 사용하면 비어 있는 새 쿼리를 만들 수 있습니다.
- 1400 호환성 수준에서 테이블의 모델 정의를 업데이트하지 않도록 기존 데이터 원본 쿼리를 편집하는 문제를 해결했습니다.
- 예외를 일으킬 수 있는 사용자 지정 컨텍스트 식과 관련된 문제를 해결했습니다.
- 이제 1400 표 형식 모델에서 중복된 이름을 가진 새 테이블을 가져올 때 이름 충돌이 발생했고 이름을 고유하게 조정했음을 사용자에게 알립니다.
- 현재 사용자 가장 모드는 지원되는 시나리오가 아니기 때문에 가져오기 모드인 모델에서 삭제되었습니다.
- 이제 PowerQuery 통합 추가 데이터 원본에 대한 옵션을 지원합니다(OData.Feed, Odbc.DataSource, Access.Database, SapBusinessWarehouse.Cubes).
- 이제 데이터 원본의 PowerQuery 옵션 문자열은 클라이언트 로캘에 따라 지역화된 텍스트를 정확히 표시합니다.
- 이제 다이어그램 보기는 1400 호환성 수준 모델의 M 쿼리 편집기에서 새로 만든 열을 표시합니다.
- 이제 파워 쿼리 편집기는 데이터를 가져오지 않는 옵션을 제공합니다.
- VS2017의 다차원 모델에서 Oracle의 테이블을 가져오는 데 사용되는 데이터 카트리지 설치와 관련된 문제를 해결했습니다.
- 드문 경우지만 마우스 커서가 표 형식 수식 표시줄을 그대로 두면 충돌이 발생할 수 있는 문제를 해결했습니다.
- 테이블 속성 편집 대화 상자에서 테이블 이름을 올바르지 않게 변경하면 원본 테이블 이름도 변경되어 예기치 않은 오류가 발생하는 문제를 해결했습니다.
- 다차원 프로젝트의 역할 디자이너 셀 데이터 탭 디자이너에서 큐브 보안 테스트를 호출하려고 할 때 VS2017에서 발생할 수 있는 충돌을 해결했습니다.
- SSDT: 표 형식 데이터 원본에 대한 속성은 편집할 수 없습니다.
- 솔루션 파일을 가진 경우에 MSBuild 및 DevEnv 빌드가 올바르게 작동하지 않을 수 있는 문제를 해결했습니다.
- 표 형식 모델이 더 큰 메타데이터를 포함하는 경우 모델 변경 내용(측정값, 계산된 열에 대한 DAX 편집)을 커밋할 때 성능을 크게 향상시켰습니다.
- 1400 호환성 수준 모델에서 PowerQuery를 사용하여 데이터를 가져오는 다양한 문제를 해결했습니다.
   - 가져오기를 클릭한 후에 가져오기는 시간이 오래 걸리고 UI는 상태 없음을 표시합니다.
   - 가져올 테이블을 천천히 선택하려고 할 때 탐색기 보기에서 테이블의 대규모 목록
   - 쿼리 편집기 뷰에서 35개의 쿼리 목록을 사용하는 쿼리 편집기 성능 저하(PBI desktop의 문제이기도 함)
   - 여러 테이블을 가져오면 도구 모음을 사용하지 않도록 설정하고 특정한 상황에서 완료하지 않습니다. 
   - PQ를 사용하여 테이블을 가져온 후에 모델 디자이너는 비활성으로 표시되고 데이터를 표시하지 않습니다.
   - PQ UI에서 "새 테이블 만들기"의 선택을 취소하면 만든 새 테이블에 여전히 적용됩니다.
   - 자격 증명에 대한 메시지를 표시하지 않는 폴더 데이터 원본 
   - 개체 참조는 구조화된 데이터 원본에서 업데이트된 자격 증명을 가져올 수 있는 예외를 설정하지 않습니다.
   - M 식을 사용하여 파티션 관리자를 여는 작업은 매우 느렸습니다.
   - PQ 편집기의 테이블에서 속성을 선택하면 속성을 표시하지 않았습니다.
- 최상위 예외를 catch하고 출력 창에 표시하도록 파워 쿼리 UI 통합의 강력합을 향상시켰습니다.
- 컨텍스트 식의 경우 구조 데이터 원본에서 ChangeSource가 변경 재용을 유지하지 않는 문제를 해결했습니다.
- M 식 오류로 인해 오류 메시지를 표시하지 않고 모델을 업데이터하는 데 실패할 수 있는 문제를 해결했습니다.
- "빌드는 솔루션을 닫기 전에 중지되어야 합니다."라는 오류와 함께 SSDT를 닫는 문제를 해결했습니다.
- 1400 호환성 수준 모델에서 잘못된 가장 모드를 설정할 때 VS가 중단될 수 있는 문제를 해결했습니다. 
- 이제 세부 정보 행 속성이 비어 있지 않으면 JSON으로만 직렬화됩니다(기본값에서 변경됨).
- 이제 Oracle OLEDB 드라이버를 표 형식 직접 쿼리 모드에서 사용할 수 있습니다.
- 이제 1400 호환성 표 형식 모델에서 M 식을 추가하면 TME(표 형식 모델 탐색기)에서 표시/다시 고침이 됩니다.
- 1400 호환성 수준 이전 모델에서 "다른" 데이터 원본을 사용하여 가져오려고 할 때 MSOLAP 공급자를 VS2017에서 표시하지 않는 문제를 해결했습니다.
- TME를 통한 번역을 추가하여 문제가 발생할 수 있는 문제를 해결했습니다. 
- 특정 경우에 올바르지 않게 탭을 나타내거나 숨기는 개체 수준 보안 인터페이스에서 문제를 해결했습니다.
- 데이터베이스 대화 상자를 사용하여 이전에 로드된 다차원 모델을 열 때 실패 오류가 발생할 수 있는 문제를 해결했습니다.
- 다차원 모델에 사용자 지정 어셈블리를 추가할 때 오류를 발생시키는 문제를 해결했습니다.

**RS(Reporting Services)**

- VS 2017에서 RDLC의 빌드 및 컴파일과 관련된 문제를 해결했습니다.

## <a name="ssdt-for-visual-studio-2017-1530-preview"></a>Visual Studio 2017용 SSDT(15.3.0 미리 보기)
빌드 번호: 14.0.16121.0
  
### <a name="whats-new"></a>새로운 기능

이 미리 보기는 Visual Studio 2017용 SSDT의 첫 번째 버전입니다. 이 릴리스에서는 Visual Studio 2017 15.3 이상의 SQL Server Database, Analysis Services, Reporting Services 및 Integration Services 프로젝트에 대한 독립 실행형 웹 설치 환경을 소개합니다.


**알려진 문제**

- 설치 프로그램이 지역화되지 않았습니다.
- SSIS가 지역화되지 않았습니다.
- SSIS 패키지 실행 태스크는 *ExecuteOutofProcess*가 *True*로 설정되었을 때 디버깅을 지원하지 않습니다. 이 문제는 디버깅에만 적용됩니다. DTExec.exe 또는 SSIS 카탈로그를 통한 저장, 배포 및 실행은 영향을 받지 않습니다.
- 전체 변경 내용 목록은 [변경 로그](changelog-for-sql-server-data-tools-ssdt.md)를 참조하세요.
- 타사 확장을 포함하는 SSIS 패키지는 다른 서버 버전을 대상으로 하도록 전환할 수 없습니다.


## <a name="ssdt-172-for-visual-studio-2015"></a>Visual Studio 2015용 SSDT 17.2
빌드 번호: 14.0.61707.300

### <a name="whats-new"></a>새로운 기능


**AS 프로젝트:**
- 이제 1400 호환성 수준에서 표 형식 모델의 고급 보안을 위한 *역할* 대화 상자에서 개체 수준 보안을 구성할 수 있습니다.
- VS2017용 SSDT AS 프로젝트의 AS Azure 모델에서 메일 주소가 없는 사용자에 대한 새 AAD 역할 멤버 선택.
- ADAL 자격 증명 캐싱의 동작을 사용자 지정하기 위한 SSDT AS 테이블 형식 프로젝트의 새 AS Azure "항상 확인" 프로젝트 속성.


### <a name="bug-fixes"></a>버그 수정

**일반**
- SQL Server 2017에 대한 브랜딩 참조가 업데이트됨.

**AS 프로젝트:**
- DAX 측정값 변경 내용 및 기타 모델 편집 내용을 커밋할 때 환경 개선을 위해 중대한 성능을 수정함.
- Analysis Services 프로젝트에서 1400 호환성 수준의 테이블 형식 모델을 사용하여 파워 쿼리 통합과 관련된 여러 가지 문제를 해결함.
- VS2017의 다차원 프로젝트에서 디자인 집계 디자이너가 로드에 실패할 수 있는 문제를 해결함.
- Analysis Services 다차원 DSV 다이어그램에 항목을 끌어 올 때 VS 2017 작동이 중단될 수 있는 문제를 해결함.
- AS 프로젝트에서 [배포] 대화 상자가 항상 Visual Studio 위의 전경에 표시되지 않았던 문제를 해결함.
- 서비스가 해제되었으므로 Data Marketplace에서 데이터 원본으로 Analysis Services 가져오기를 제거함.
- 테이블 형식 모델 탐색기를 통해 기존 데이터 원본에서 새 테이블 가져오기 이후 테이블 디자이너가 비활성 상태로 유지되는 문제를 해결함.
- 데이터 원본에서 가져오기/데이터 원본 추가 모델 메뉴 항목이 잘못된 컨텍스트에 계속 숨겨져 있는 문제를 해결함.
- 측정값을 만드는 데 사용되는 열로 포커스를 다시 전환하지 않기 위해 테이블 형식 모델 탐색기에서 측정값을 만드는 경우의 환경 개선함.
- AS 테이블 형식 프로젝트에서 통합된 작업 영역을 명시적 작업 영역 서버로 전환하면 이제는 이전 데이터베이스 파일이 정리됨.
- AS 테이블 형식 1400 모델 프로젝트에서 실제 기본 개체 상태와 관계없이 행 수준 보안 확인란 UI 상태가 처음에는 선택 취소된 상태로 표시되는 문제를 해결함.
- 파워 쿼리 및 처리되지 않은 throw된 예외를 사용하여 텍스트 파일 또는 Excel 파일을 1400-compat 모드 테이블 형식 모델에 가져올 때 발생할 수 있는 충돌 해결함.
- AS 테이블 형식 모델 디자이너에서 DAX 수식 편집 컨트롤의 스크롤 막대에 발생할 수 있는 문제를 해결함.
- 사용자 이름/암호 인증을 포함하는 경우 PowerQuery 매시업 데이터 원본을 수정할 수 없는 문제를 해결함.
- 연결 문자열에 추가 속성이 설정된 경우 데이터 원본을 연결할 수 없는 문제를 해결함.
- 여러 개의 AS 테이블 형식 모델 프로젝트가 로드되고 디자이너의 어떤 항목과도 먼저 상호 작용하지 않은 채 두 번째 모델 디자이너를 닫을 때 VS와 충돌할 수 있는 문제를 해결함.
- KPI 서식에 대해 편집한 항목이 일부 경우에 지속되지 않는 문제를 해결함.
- PowerQuery UI에서 수식 입력줄이 표시되었는지에 따라 잘못된 메뉴 확인됨 상태를 보여 주는 문제를 해결함.
- PowerQuery 데이터 원본을 포함한 AS 테이블 형식 1400-compat 수준 프로젝트에서 테이블 형식 모델 탐색기에서 데이터 소스 변경 메뉴를 선택할 때 VS와 충돌할 수 있는 문제를 해결함.
- 1400 테이블 형식 모델을 로드할 때 ‘파일이나 어셈블리 'Microsoft.ProBI.MashupLibrary를 로드할 수 없음’ 오류가 나타날 수 있는 간헐적 문제를 해결함.

**RS 프로젝트**
- RS 눈금자 및 매개 변수 상자 설정 선택 상태에 대한 사용자 기본 설정은 세션 간에 올바로 기억됩니다.

**IS 프로젝트**
- ADO/ADO.NET ForEachLoop 컨테이너가 올바로 표시되지 않는 문제를 해결함
- 일부 작업/구성 요소/마법사가 현지화되지 않은 문제를 해결함
- 최신 *TargetServerVersion*이 "SQL Server vNext"에서 "SQL Server 2017"로 변경됨


## <a name="ssdt-171-for-visual-studio-2015"></a>Visual Studio 2015용 SSDT 17.1
빌드 번호: 14.0.61705.170

### <a name="whats-new"></a>새로운 기능
**AS 프로젝트:**
- 사용자가 UI 1400 모델의 UI에서 열에 인코딩 힌트를 설정할 수 있음
- 모델과 관계없이 IntelliSense를 이제 오프라인으로 사용할 수 있음
- 이제 테이블 형식 모델 탐색기에 모델(1400 호환성 수준 테이블 형식 모델) 전반에서 사용 가능한 명명된 M 식을 나타내는 노드가 포함되어 있음
- 테이블 형식 모델에서 역할 멤버를 설정할 때 이제 Microsoft Azure Portal의 IAM과 유사한 Azure Active Directory 사용자 선택을 사용할 수 있음

**데이터베이스 프로젝트:**
- DacFx 17.1로 업데이트됨

### <a name="bug-fixes"></a>버그 수정
- VS2017의 Visual Studio 옵션에서 비즈니스 인텔리전스 디자이너 그룹 이름이 잘못 표시되던 문제를 해결함
- 보고서 프로젝트 또는 AS 프로젝트를 사용하여 솔루션에 대한 코드 맵을 생성할 때 충돌이 발생할 수 있는 문제를 해결함
- Analysis Services 1400 호환성 수준 테이블 형식 모델에 대한 PowerQuery 통합과 관련된 여러 문제를 해결함
- 측정값을 정의할 때 대입 연산자를 별도의 줄에 지정할 수 없는 새 DAX 편집기 도구 창의 문제를 해결함
- 큐브 뷰에서 측정값 이름을 바꿀 때 테이블 형식 측정값 표시가 업데이트되지 않는 문제를 해결함
- Analysis Services 통합 작업 영역 엔진 및 테이블 형식 개체 모델을 업데이트하여 번역이 포함된 1200 테이블 형식 프로젝트가 SQL Server 2016 Analysis Services 서버에 배포되지 않게 하는 회귀를 해결함
- 새 1400 테이블 형식 데이터 원본의 만들기 및 삭제를 아주 느리게 만드는 성능 문제를 해결함
- 다른 DSV 간에 뷰를 빠르게 변경할 경우 다차원 모델에서 DSV 다이어그램의 렌더링이 중지될 수 있는 문제를 해결함

## <a name="dacfx-171"></a>DacFx 17.1
- 다른 ID 열이 있는 메모리 액세스에 최적화된 테이블을 사용하여 열을 암호화할 때 발생하는 문제를 해결함
- SQLDOM에서 CREATE DATABASE에 대한 CATALOG_COLLATION 옵션 지원

## <a name="dacfx-1701"></a>DacFx 17.0.1 
- EKM 공급자를 사용하는 HSM의 비대칭 키가 포함된 데이터베이스와 관련된 문제에 대한 수정 [Connect 항목](https://connect.microsoft.com/SQLServer/feedback/details/3132749/sqlpackage-exe-fails-when-extracting-a-database-which-contains-an-asymmetric-key-using-an-ekm-provider)

## <a name="ssdt-170-for-visual-studio-2015-supports-up-to-sql-server-2017"></a>Visual Studio 2015용 SSDT 17.0(SQL Server 2017까지 지원)
빌드 번호: 14.0.61704.140

### <a name="whats-new"></a>새로운 기능
**데이터베이스 프로젝트:**
- 뷰의 클러스터형 인덱스 수정에서 더 이상 배포를 차단하지 않음
- 열 암호화와 관련된 스키마 비교 문자열에서 인스턴스 이름 대신 적절한 이름을 사용함.   
- SqlPackage에 새 명령줄 옵션 ModelFilePath를 추가함.  이 옵션을 사용하면 고급 사용자가 가져오기, 게시 및 스크립팅 작업에 사용할 외부 model.xml 파일을 지정할 수 있습니다.   
- DacFx API가 Azure AD 유니버설 인증 및 MFA(Multi-Factor Authentication)를 지원하도록 확장됨

**IS 프로젝트:**
- 이제 SSIS OData 원본 및 OData 연결 관리자가 Microsoft Dynamics AX Online 및 Microsoft Dynamics CRM Online의 OData 피드에 연결할 수 있음
- 이제 SSIS 프로젝트에서 “SQL Server 2017”의 대상 서버 버전을 지원함 
- SQL Server 2017을 대상으로 할 경우 CDC 제어 태스크, CDC 분할자 및 CDC 원본 지원 

**AS 프로젝트:**
- Analysis Services PowerQuery 통합(1400 호환성 수준 테이블 형식 모델):
    - DirectQuery를 SQL Oracle에 사용할 수 있으며, 사용자가 타사 드라이버를 설치한 경우 Teradata에도 사용할 수 있음
    - PowerQuery의 예제별 열 추가
    - 1400 모델의 데이터 액세스 옵션(M 엔진에서 사용하는 모델 수준 속성)
        - 빠른 결합 사용(기본값은 false. true로 설정할 경우 데이터를 결합할 때 매시업 엔진이 데이터 원본 개인 정보 보호 수준을 무시함)
        - 레거시 리디렉션 사용(기본값은 false. true로 설정할 경우 매시업 엔진이 안전하지 않을 수 있는 HTTP 리디렉션을 추적함.  예: HTTPS에서 HTTP URI로 리디렉션)  
        - 오류 값을 Null로 반환(기본값은 false. true로 설정할 경우 셀 수준 오류가 null로 반환됨. false인 경우 셀에 오류가 포함되어 있으면 예외가 발생함)  
    - PowerQuery를 사용하는 추가 데이터 원본(파일 데이터 원본)
        - 내보내기 
        - Text/CSV 
        - Xml 
        - Json 
        - Folder 
        - Access 데이터베이스 
        - Azure Blob Storage 
    - 지역화된 PowerQuery 사용자 인터페이스
- DAX 편집기 도구 창
    - SSDT의 보기, 다른 창 메뉴를 통해 사용 가능한 측정값, 계산 열 및 세부 정보 열 식에 대한 DAX 편집 환경 개선
    - DAX 파서\Intellisense 개선


**RS 프로젝트:**
- 포함 가능한 RVC 제어를 SSRS 2016을 지원하는 데 사용할 수 있음

### <a name="bug-fixes"></a>버그 수정
**AS 프로젝트:**
- BI 프로젝트가 VS에서 [New Projects]\(새 프로젝트) 범주 맨 위에 표시되지 않도록 템플릿 우선 순위를 수정함
- SSIS, SSAS 또는 SSRS 솔루션을 열 때 간혹 발생할 수 있는 VS 충돌 문제를 해결함
- 테이블 형식: DAX 구문 분석 및 수식 입력줄에 대한 여러 개선 사항 및 성능 수정.
- 테이블 형식: SSAS 테이블 형식 프로젝트가 열려 있지 않은 경우 테이블 형식 모델 탐색기가 더 이상 표시되지 않음.
- 다차원: 고해상도(High-DPI) 컴퓨터에서 처리 대화 상자를 사용할 수 없는 문제를 해결함.
- 표 형식: SSMS가 이미 열려 있을 때 BI 프로젝트를 여는 경우 SSDT 오류가 발생하는 문제를 해결함. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3100900/ssdt-faults-when-opening-any-bi-project-when-ssms-is-already-open)
- 테이블 형식: 1103 모델에서 계층이 bim 파일로 올바르게 저장되지 않는 문제를 해결함. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3105222/vs-2015-ssdt)
- 테이블 형식: 통합 작업 영역 모드가 지원되지 않는데도 32비트 컴퓨터에서 허용되는 문제를 해결함.
- 테이블 형식: 부분 선택 모드에서 항목을 클릭하는 경우(예를 들어, DAX 식을 입력하지만 측정값을 클릭함) 작동이 중단될 수 있는 문제를 해결함.
- 테이블 형식: 배포 마법사에서 모델의 .Name 속성을 "Model"로 다시 설정하는 문제를 해결함. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3107018/ssas-deployment-wizard-resets-modelname-to-model)
- 테이블 형식: [다이어그램 뷰]를 선택하지 않았는데도 TME에서 계층을 선택할 때 속성이 표시되는 문제를 해결함.
- 테이블 형식: 특정 응용 프로그램에서 붙여넣을 때 DAX 수식 입력줄에 붙여넣으면 텍스트 대신 이미지나 기타 콘텐츠를 붙여넣는 문제를 해결함.
- 테이블 형식: 특정 정의가 포함된 측정값이 있어서 1103의 일부 이전 모델을 열 수 없는 문제를 해결함.
- 테이블 형식: XEvent 세션을 삭제할 수 없는 문제를 해결함.
- Devenv.com이 포함된 AS "smproj" 파일을 빌드하지 못하는 문제를 해결함
- AS 테이블 형식 모델 시트 탭 제목에서 한국어 IME를 사용할 경우 텍스트 변경 내용을 너무 자주 종료하는 문제를 해결함
- DAX Related() 함수에 대한 Intellisense가 제대로 작동하지 않아 다른 테이블의 열을 표시하는 문제를 해결함
- 데이터베이스 대화 상자에서 AS 데이터베이스 목록을 정렬하여 AS 테이블 형식 프로젝트 가져오기를 개선함
- AS 테이블 형식 모델에서 계산된 테이블을 만들 때 테이블이 식에서 제안된 개체로 나열되지 않는 문제를 해결함
- 미리 보기 1400 AS 모델에서 코드를 본 후 통합 작업 영역 서버를 사용하여 열려고 할 때 발생하는 문제를 해결함
- 특정 상황에서 초기 카탈로그를 지원하지 않는 일부 데이터 원본이 제대로 작동하지 않는 문제를 해결함 
- 파티션을 유지하는 옵션을 사용하도록 설정한 경우에도 배포 마법사에서 계산된 테이블에 변경 내용을 적용해야 함
- 기존 AC 연결에 대한 [고급 속성] 대화 상자에 다시 선택할 때까지 전체 목록이 표시되지 않는 문제를 해결함
- 일부 지역화된 빌드에서 표시되는 잘린 UI 문자열 관련 몇 가지 문제를 해결함
- 1400 호환성 수준 AS 테이블 형식 모델에서 PowerQuery 통합과 관련된 여러 문제를 해결함
- 보고서 마법사 스타일 템플릿이 올바로 표시되지 않는 문제를 해결함
- 보고서 마법사에서 SQL AS로 변경할 때 데이터 원본 설정이 잘못될 수 있는 문제를 해결함
- 명령줄(devenv.com\exe)에서 Analysis Services(테이블 형식) 프로젝트 빌드 오류를 일으키는 문제를 해결함
- DAX 측정값 파서에서 := 앞에 문자로 시작할 때 강조 표시된 올바른 텍스트 색을 표시하는 문제를 해결함
- 통합 작업 영역 모드에서 테이블 형식 프로젝트에 대한 모든 파일을 표시하려고 할 때 경로가 너무 길어지는 경우 ObjectRefException을 트리거하는 문제를 해결함
- Compact 4.0 클라이언트 데이터 공급자용 데이터 원본 디자이너가 사용할 수 없는 것으로 보이는 문제를 해결함
- VS2017에서 AS 마이닝 모델을 검색하는 동안 오류가 발생하는 문제를 해결함
- VS2017의 AS 다차원 모델에서 뷰를 변경한 후 DSV 다이어그램의 렌더링이 중지된 다음 예외가 적중되는 문제를 해결함
- VS2017에서 보고서를 미리 보는 동안 AS 연결에 실패하는 문제를 해결함
 

**RS 프로젝트:**
- SSDT에서 보고서를 디자인할 때 대부분의 변경 작업 중 매개 변수, 데이터 원본 및 데이터 집합의 트리 뷰가 축소되는 문제를 해결함 
- [저장]을 누를 때 최신 버전이 아니라 RDL 버전이 저장되는 문제를 해결함.
- 백업이 꺼져 있을 때 SSDT RS가 파일을 백업하는 문제와 여러 다른 문제를 해결함.
- "셀 분할"을 클릭할 때 오류가 표시되는 보고서 작성기의 문제를 해결함. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3101818/ssdt-2015-ssrs-designer-error-by-matrix-cell-split)
- 캐싱으로 인해 보고서의 데이터가 잘못될 수 있는 문제를 해결함. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3102158/ssdtbi-14-0-60812-report-preview-data-is-frequently-wrong-due-to-bad-caching)

**IS 프로젝트:**
- run64bitruntime 설정이 유지되지 않는 문제를 해결함.
- DataViewer에서 표시된 열을 저장하지 않는 문제를 해결함.
- 패키지 파트에서 주석을 숨기는 문제를 해결함. [Connect 항목](https://connect.microsoft.com/SQLServer/feedback/details/3106624/package-parts-hide-annotations)
- 패키지 파트에서 데이터 흐름 레이아웃 및 주석을 무시하는 문제를 해결함. [Connect 항목](https://connect.microsoft.com/SQLServer/feedback/details/3109241/package-parts-discard-data-flow-layouts-and-annotations)
- SQL Server에서 프로젝트를 가져올 때 SSDT 작동이 중단되는 문제를 해결함
- 저장한 SSIS 패키지를 연 후와 런타임에 Hadoop 파일 시스템 태스크 TimeoutInMinutes가 기본적으로 10으로 지정되는 문제를 해결함

**데이터베이스 프로젝트:**
- SSDT DACPAC 배포에서 IgnoreColumnOrder에 대한 설정 다시 추가. [Connect 항목](https://connect.microsoft.com/SQLServer/feedback/details/1221587/ssdt-dacpac-deploy-add-setting-back-in-for-ignorecolumnorder)
- STRING_SPLIT를 사용하는 경우 SSDT가 컴파일하지 못함. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/2906200/ssdt-failing-to-compile-if-string-split-is-used)
- DeploymentContributors에서 공개 모델에 액세스할 수 있지만 지원 스키마가 초기화되지 않는 문제를 해결함. [Github 문제](https://github.com/Microsoft/DACExtensions/issues/8)
- 파일 그룹 배치에 대한 DacFx 임시 수정
- 외부 동의어에 대한 "확인되지 않은 참조" 오류에 대한 수정 
- Always Encrypted: 온라인 암호화가 취소 시 변경 내용 추적을 사용하지 않도록 설정하지 않으며 암호화 시작 전에 변경 내용 추적이 정리되지 않은 경우 올바로 작동하지 않음


## <a name="ssdt-165-for-visual-studio-2015-supports-up-to-sql-server-2016"></a>Visual Studio 2015용 SSDT 16.5(SQL Server 2016까지 지원)
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
* 테이블 탭이 선택된 경우 키를 누를 때 발생하는 SSDT AS 테이블 형식 디자이너의 작동이 중단되는 문제가 해결됨
* Excel의 분석 기능이 하위 수준 AS 서버 버전에 연결하지 못하는 SSDT AS 프로젝트의 문제가 수정됨

**통합 서비스**

* 연결 버그 [1608896](https://connect.microsoft.com/SQLServer/feedback/details/1608896/move-multiple-integration-service-package-tasks) 수정됨: 여러 통합 서비스 패키지 작업 이동





## <a name="ssdt-164-for-visual-studio-2015-for-sql-server-2016"></a>Visual Studio 2015용(SQL Server 2016용) SSDT 16.4
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



## <a name="ssdt-163-for-visual-studio-2015-for-sql-server-2016"></a>Visual Studio 2015용(SQL Server 2016용) SSDT 16.3
릴리스됨: 2016년 8월 15일

빌드 번호: 14.0.60812.0  

**새로운 기능**

- **릴리스 버전 관리 및 번호 매기기:** 이제 릴리스에 월별이 아니라 번호로 태그가 지정됩니다. 이 변경 내용은 새 SSMS 정책에 부합하며 한 달에 여러 개의 릴리스 또는 핫픽스가 있는 경우를 간소화합니다. 이 릴리스는 16.3으로, RTM 릴리스 후 세 번째 업데이트를 의미합니다. 모든 핫픽스는 16.3.1 등으로 지정되며, 다음 달에 계획된 다음 업데이트는 16.4가 됩니다.
- **Analysis Services - 테이블 형식 모델 탐색기:** 테이블 형식 모델 탐색기를 사용하면 데이터 원본, 테이블, 측정값, 관계 등 모델의 다양한 메타데이터 개체를 편리하게 탐색할 수 있습니다. Visual Studio에서 보기 메뉴를 열고 다른 창을 가리킨 다음 테이블 형식 모델 탐색기를 클릭하면 표시할 수 있는 별도 도구 창으로 구현됩니다. 테이블 형식 모델 탐색기는 기본적으로 솔루션 탐색기 영역의 별도 탭에 표시됩니다. 테이블 형식 모델 탐색기는 테이블 형식 1200 모델의 스키마와 매우 비슷한 트리 구조로 메타데이터 개체 및 많은 새로운 기능을 구성합니다.
- **데이터베이스 도구 – Always Encrypted**: 이 릴리스에서는 데이터베이스 프로젝트 또는 SQL Server 개체 탐색기의 라이브 데이터베이스에 열 마스터 키 열 또는 열 암호화 키를 쉽게 추가할 수 있도록 새로운 [Always Encrypted 키 관리](../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md) 대화 상자를 제공합니다. 이 릴리스에서는 Windows 인증서 저장소의 인증서를 지원합니다. 이후 릴리스에서는 Azure Key Vault 및 CNG 공급자가 지원될 예정입니다.
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
        - .dwpro 프로젝트에 대해 무한 루프 오류를 발생시키는 계층 구조 순서 문제가 해결되었습니다.
        - RDL 다운그레이드 시 전체를 다시 빌드해야 해서 사용자에게 혼동을 주는 RS RDL 문제가 수정되었습니다.
        - 클라이언트 도구에서 숨기기가 적용되지 않는 KPI 문제가 수정되었습니다.
        

 
  
## <a name="ssdt-july-for-visual-studio-2015-for-sql-server-2016"></a>Visual Studio 2015용(SQL Server 2016용) SSDT 7월  
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
    * 비정상적인 상황이 더 안정적으로 처리되도록, 붙여넣은 테이블이 있는 AS 모델을 1103에서 1200 호환성 수준으로 업그레이드할 경우 “관계에서 잘못된 열 ID를 사용합니다.” 오류가 발생할 수 있는 문제가 해결되었습니다.
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
    * UI에서 서식 유형을 변경할 수 있도록 열 형식에 기본 서식을 사용하는 경우 1200 호환성 수준 모델 계산된 테이블 UI의 문제가 해결되었습니다. 
    

## <a name="ssdt-june-for-visual-studio-2015-for-sql-server-2016"></a>Visual Studio 2015용(SQL Server 2016용) SSDT 6월  
릴리스됨: 2016년 6월 1일  
  
빌드 번호: 14.0.60525.0 

이제 SSDT GA(일반 공급)가 릴리스되었습니다. 2016년 6월의 SSDT GA 업데이트에서는 SQL Server 2016 RTM의 최신 업데이트 및 다양한 버그 수정 프로그램에 대한 지원이 추가되었습니다. 자세한 내용은 [2016년 6월의 SQL Server Data Tools GA 업데이트](https://blogs.msdn.microsoft.com/ssdt/2016/06/01/sql-server-data-tools-ga-update-for-june-2016/)를 참조하세요.

  
  
## <a name="additional-resources"></a>추가 리소스
  
[SQL Server Data Tools 다운로드 &#40;SSDT&#41;](../ssdt/download-sql-server-data-tools-ssdt.md)  
[SQL Server Data Tools&#40;SSDT 및 SSDT-BI&#41;의 이전 릴리스](../ssdt/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md)  
[데이터베이스 엔진의 새로운 기능](https://msdn.microsoft.com/library/bb510411.aspx)  
[Analysis Services의 새로운 기능](../analysis-services/what-s-new-in-analysis-services.md)  
[Integration Services의 새로운 기능](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
