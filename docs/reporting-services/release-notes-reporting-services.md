---
title: Reporting Services(2017 이상)의 릴리스 정보 | Microsoft Docs
description: SSRS(SQL Server Reporting Services) 버전 2017 이상의 변경 내용을 자세히 알아봅니다.
ms.date: 10/11/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.reviewer: maggies
author: casualoak
ms.author: rhys
monikerRange: '>=sql-server-2017'
ms.openlocfilehash: 07e8b01d94d1ab9c3b9d19ab28d4ed4b3d595b2b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97425133"
---
# <a name="release-notes-for-sql-server-reporting-services-ssrs-2017-and-later"></a>SSRS(SQL Server Reporting Services)(2017 이상)의 릴리스 정보

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)]

이 문서에서는 [!INCLUDE[ssnoversion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)](SSRS) 버전 2017 이상의 변경 사항을 설명합니다.

보고서 뷰어 제어의 릴리스 정보는 [WebForms 및 WinForms SSRS의 보고서 뷰어 제어 릴리스 정보](application-integration/release-notes-ssrs-application-integration.md)를 참조하세요.

<!--
We are "standardizing" all our 'Release Notes' style articles:

  - File names:   'release-notes-[TechArea-Name].md'


  - Content format:   2-column tables.  No longer using bullet lists.

    - Ideally, the 'Details' column should contain a link to another SSRS documentation article wherein the particular issue fix is discussed in any way.  Or if there is more to say beyond one sentence, the other sentences of elaboration would go into the 'Details' column.


  - H2 header names are kept short, for better display.


  - Try to keep all Release Notes in one .md file.  Avoid having multiple R.N. files whose names differ only by version or date.

    - Seriously consider erasing info about ancient releases that are so old that nobody cares about them anymore.  If you really want to retain ancient info, consider doing so in an HTML comment at the end of the .md file, just in case a Microsoft employee needs to re-examine ancient info.  In any case, this file cannot get ever longer, and some deletion or hiding of oldest info must eventually occur.


  - Do use '::: moniker range=' zones when version 2017 is no longer the only version represented inside this .md file.

    - Use the '=' operator on the moniker, not the '>=' operator.
    - In contrast, in our 'Whats New' articles we do use the '>=', rather than '='.

GeneMi, DevOps = 1467988 (MsEng > TechnicalContent) , 2019/03/19
-->
## <a name="sql-server-2019-reporting-services"></a>SQL Server 2019 Reporting Services

## <a name="15075454810-20200831"></a>15.0.7545.4810, 2020/08/31 
(제품 버전: 15.0.1102.861)

| 해결된 문제 | 세부 정보 |
| :---------- | :------ |
| 보안 업데이트  | &nbsp; |
| PDF 문서를 더 이상 허용하지 않도록 주석 첨부 파일 지원을 제한했습니다.  | &nbsp; |
| 이름에 마침표가 포함된 보고서를 내보낼 때 파일 이름 잘림을 수정했습니다.  | &nbsp; |
| 잘못된 날짜 형식 오류가 발생한 구독 및 zh-TW 문화권 관련 문제를 해결했습니다.  | &nbsp; |
| 특정 보고서에서 매개 변수 옵션에 액세스하면 무한 스핀으로 이어질 수 있는 문제를 해결했습니다.  | &nbsp; |
| 보고서 이름에서 작은따옴표와 관련된 문제를 해결했습니다.  | &nbsp; |
| URL 액세스에서 FindString이 일치 항목을 찾지 못하는 문제를 해결했습니다.  | &nbsp; |
| PDF 내보내기용 대체 텍스트가 멀티 바이트 문자로 올바르게 인코딩되지 않은 문제를 해결했습니다.  | &nbsp; |
| 선형 요소 아래에 원치 않게 표시되는 빈 이미지를 수정했습니다.  | &nbsp; |
| 웹 버전에서 사용자 지정 인증에 대해 잘못된 지원되지 않음 오류를 수정했습니다.  | &nbsp; |
| 화면 판독기가 테이블릭스의 추가 행 및 추가 열을 읽을 때의 문제를 해결했습니다.  | &nbsp; |
| 이미지를 전체 페이지로 확대할 때 크기에 맞추기에서 이미지 잘림 문제를 수정했습니다.  | &nbsp; |
| 명령줄 업그레이드에 더 이상 EULA 플래그가 필요하지 않습니다.  | &nbsp; |

## <a name="150724337714-20191101"></a>15.0.7243.37714, 2019/11/01
(제품 버전: 15.0.1102.675)

초기 릴리스


## <a name="sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services

## <a name="1406001669-20200831"></a>14.0.600.1669, 2020/08/31 

| 해결된 문제 | 세부 정보 |
| :---------- | :------ |
| 보안 업데이트  | &nbsp; |
| PDF 문서를 더 이상 허용하지 않도록 주석 첨부 파일 지원을 제한했습니다.  | &nbsp; |
| 이름에 마침표가 포함된 보고서를 내보낼 때 파일 이름 잘림을 수정했습니다.  | &nbsp; |
| 잘못된 날짜 형식 오류가 발생한 구독 및 zh-TW 문화권 관련 문제를 해결했습니다.  | &nbsp; |

## <a name="1406001572-20200406"></a>14.0.600.1572, 2020/04/06 

| 해결된 문제 | 세부 정보 |
| :---------- | :------ |
| JQuery UI를 1.12로 업데이트했습니다.  | &nbsp; |
| URL 대/소문자 구분을 수정했습니다.  | &nbsp; |
| 매개 변수가 많은 경우 매개 변수 배치를 수정했습니다.  | &nbsp; |
| HTML5 렌더링에서 작동하지 않는 FindString을 수정했습니다.  | &nbsp; |
| TLS 1.0/1.1 사용 중단을 처리하도록 Analysis Services 클라이언트 라이브러리를 업데이트했습니다. | &nbsp; |

## <a name="1406001451-20191113"></a>14.0.600.1451, 2019/11/13 

| 해결된 문제 | 세부 정보 |
| :---------- | :------ |
| 보안 업데이트 | &nbsp; |
| 스냅샷이 사용 설정된 경우에는 페이지 번호를 매긴 보고서가 필터 매개 변수로 올바로 기능하지 않았습니다.  | &nbsp; |
| 브라우저 역할이 할당되고 기본 설정이 된 사용자에게 Excel 파일 다운로드 권한이 없습니다.  | &nbsp; |
| 업그레이드 중에 SQL Server 2016 Reporting Services에서 Power BI Report Server로의 업그레이드가 실패했습니다. | &nbsp; |
| SQL Server 2012 Reporting Services에서의 업그레이드 후 “메일 헤더에 잘못된 문자가 있습니다. ','” 메시지와 함께 구독이 실패했습니다. | &nbsp; |
| 구성 도구: 데이터베이스 섹션의 모달 창 취소로 Reporting Services 서비스가 재시작될 수 있습니다. | &nbsp; |
| TextBox 컨트롤의 BorderStyle 속성 식이 Excel 형식으로 렌더링되지 않습니다.  | &nbsp; |
| 특정 보고서가 최종 페이지까지 도달하지 않고 동일 페이지 렌더링으로 중단되는 페이지 매김 문제가 발생합니다. | &nbsp; |

## <a name="1406001274-20190701"></a>14.0.600.1274, 2019/07/01

| 해결된 문제 | 세부 정보 |
| :---------- | :------ |
| 보안 업데이트 | &nbsp; |
| 공유된 주별 일정 생성 시 요일을 선택할 수 없습니다. | &nbsp; |
| 보고서가 캐리지 리턴을 Word 형식으로 올바로 표시하지 않습니다. | &nbsp; |
| SCOM(System Center Operations Manager) 2019가 최신 SSRS 2017 업그레이드로 더 이상 작동하지 않습니다. | &nbsp; |
| 공유 데이터 집합의 권한 부여 확장 호출 중 오류가 발생합니다. | &nbsp; |
| SSRS 2017 및 PBIRS의 저장 프로시저 GetAllProperties에서 논리가 변경되어 웹 서비스 엔드포인트 ReportingService2010.GetProperties 메서드가 링크된 보고서의 모든 데이터를 받을 수 없습니다. | &nbsp; |
| 표 안의 항목 클릭하면 모바일 보고서의 단순 표 열이 사라집니다. | &nbsp; |
| 데이터 기반 구독 매개 변수의 데이터 필드를 사용할 수 없습니다. | &nbsp; |
| SSRS 2016 이상의 중첩된 테이블릭스에 표시되는 폰트가 작거나 불완전합니다. | &nbsp; |
| DateTime 매개 변수가 있는 구독이 다른 로캘의 수정 이후 오류가 발생합니다. | &nbsp; |
| Null 제공 확장으로 데이터 기반 구독 생성 시 "배달 오류가 발생했습니다" 메시지와 함께 실패합니다. | &nbsp; |
| Excel\Word 형식의 값으로 설정 시 URL 인코딩이 부정확합니다. | &nbsp; |

## <a name="1406001109-20190212"></a>14.0.600.1109, 2019/02/12

| 해결된 문제 | 세부 정보 |
| :---------- | :------ |
| 캐시 보고서 스냅샷 일정이 구독을 수정한 후 "보고서별 일정"으로 변경됨 | &nbsp; |
| rc:Toolbar=false가 Express Edition에서 작동하지 않습니다. | &nbsp; |
| 페이지를 매긴 보고서를 PDF로 내보낼 때 특정 태국어 문자가 잘못 렌더링됩니다. | &nbsp; |
| 완료된 데이터 기반 구독을 알리는 동안 교착 상태가 발생합니다. | &nbsp; |
| rc:Toolbar=False 매개 변수가 사용될 때 특정 환경에서 포함된 이미지가 표시되지 않습니다. | &nbsp; |
| 연속 매개 변수를 사용하는 보고서에 대한 데이터 기반 구독을 만들 수 없습니다. | &nbsp; |
| 잘못된 간격으로 구성된 구독을 편집할 수 없습니다. | &nbsp; |
| 보안 업데이트 | &nbsp; |
| 연결된 보고서 UI가 표시되지 않습니다. | &nbsp; |
| 중첩된 테이블릭스 컨트롤이 있는 특정 페이지를 매긴 보고서의 글꼴이 잘못됨 | &nbsp; |
| 테이블릭스 데이터 영역이 포함되고 페이지를 매긴 특정 보고서에 공백이 잘못 추가됩니다. | &nbsp; |
| 모바일 보고서 단순 데이터 표를 확장할 때 머리글 행이 나타나지 않습니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600906-20180912"></a>14.0.600.906, 2018/09/12

다음 문제가 수정되었습니다.

| 해결된 문제 | 세부 정보 |
| :---------- | :------ |
| 사용자 지정 인증이 올바른 쿠키 정보를 반환하지 않습니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600892-20180831"></a>14.0.600.892, 2018/08/31

| 해결된 문제 | 세부 정보 |
| :---------- | :------ |
| 텍스트 상자가 rc:Toolbar=False이고 긴 텍스트를 포함할 때 직사각형 내부의 텍스트 상자가 직사각형의 세로 확장을 차단합니다. | &nbsp; |
| pageHeight가 0.5인치 미만일 때 텍스트 크기가 조절되지 않습니다. | &nbsp; |
| CRM에서 사용 시 SSRS 카탈로그 데이터베이스에서 교착 상태가 발생합니다. | &nbsp; |
| 보고서에서 스크롤할 때 세로로 정렬된 열 머리글이 잘못 표시됩니다. | &nbsp; |
| System Center Operations Manager Reporting 역할에 추가된 사용자가 SSRS 웹 포털에 액세스할 수 없습니다. | &nbsp; |
| 태국어 문자를 PDF로 올바르게 내보낼 수 없습니다. | &nbsp; |
| 브라우저 역할 동작이 변경됩니다. | &nbsp; |
| rc:Toolbar=false가 Express Edition에서 작동하지 않습니다. | &nbsp; |
| 매개 변수 프롬프트 영역에 수직 스크롤 막대가 없습니다. | &nbsp; |
| 모바일 보고서 런타임이 업데이트됩니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600744-20180425"></a>14.0.600.744, 2018/04/25

| 해결된 문제 | 세부 정보 |
| :---------- | :------ |
| 데이터 기반 구독 페이지는 일단 만들어지면 배달 옵션을 표시하지 않습니다. | &nbsp; |
| SSRS 2012를 SSRS 2017로 업그레이드하면 결국 몇 초 마다 예외를 throw하는 RSManagement가 됩니다. | &nbsp; |
| IE11에서 다중 값 매개 변수에 대한 기본값을 변경할 수 없습니다. | &nbsp; |
| 일정은 공유 일정이 실행될 때마다 빕니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600689-20180228"></a>14.0.600.689, 2018/02/28

| 해결된 문제 | 세부 정보 |
| :---------- | :------ |
| 링크된 보고서의 보고서 매개 변수 표시 유형이 해당 속성을 편집한 후에 되돌려집니다. | &nbsp; |
| URL 매개 변수 rc:Toolbar=false가 Express Edition에서 작동하지 않습니다. | &nbsp; |
| CanGrow 속성을 false로 설정하고 텍스트 상자에서 식을 사용하면 값이 표시되지 않습니다. | &nbsp; |
| 설정에서 제품 키에 대한 _자세한 정보_ 링크가 추가됩니다. | &nbsp; |
| 사용자 지정 폼 인증을 사용하는 웹 포털에서 슬라이딩(sliding) 만료 쿠키를 무시합니다. | &nbsp; |
| Word로 내보내기 시 행 콘텐츠가 비어 있으면 행 높이가 서로 다릅니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600594-20180109"></a>14.0.600.594, 2018/01/09

일부 보안 업데이트가 구현되었습니다.

### <a name="140600490-20171101"></a>14.0.600.490, 2017/11/01

SKU 업그레이드에서 해결된 문제입니다.

## <a name="140600451-20170930"></a>14.0.600.451, 2017/09/30

초기 릴리스

## <a name="next-steps"></a>다음 단계

[Reporting Services(SSRS)의 새로운 기능](what-s-new-in-sql-server-reporting-services-ssrs.md)

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하세요](https://go.microsoft.com/fwlink/?LinkId=620231).
