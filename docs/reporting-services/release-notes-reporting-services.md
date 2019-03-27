---
title: 릴리스 정보 (SSRS)에 대 한 2017 이상 | Microsoft Docs
ms.date: 09/01/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.reviewer: maghan
author: casualoak
ms.author: RhysSchmidtke
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: c85d3811fc467d94dc1841b871964e3bb594e2df
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58283300"
---
# <a name="release-notes-for-sql-server-reporting-services-ssrs-2017-and-later"></a>SSRS(SQL Server Reporting Services)(2017 이상)의 릴리스 정보

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)]

이 문서에서는 설명의 변경 내용을 [!INCLUDE[ssnoversion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS) 2017 이상 버전에 대 한 합니다.

보고서 뷰어 컨트롤에 대 한 릴리스 정보를 참조 하세요 [WebForms 및 WinForms의 SSRS에 대 한 보고서 뷰어에 대 한 릴리스 제어](application-integration/release-notes-ssrs-application-integration.md)입니다.

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

## <a name="1406001109-20190212"></a>14.0.600.1109, 2019/02/12

| 문제 해결된 | 세부 정보 |
| :---------- | :------ |
| 캐시 보고서 스냅숏 일정이 구독을 수정한 후 "보고서별 일정"으로 변경됨 | &nbsp; |
| rc:Toolbar=false가 Express Edition에서 작동하지 않습니다. | &nbsp; |
| 페이지를 매긴 보고서를 PDF로 내보낼 때 특정 태국어 문자가 잘못 렌더링됩니다. | &nbsp; |
| 완료된 데이터 기반 구독을 알리는 동안 교착 상태가 발생합니다. | &nbsp; |
| rc:Toolbar=False 매개 변수가 사용될 때 특정 환경에서 포함된 이미지가 표시되지 않습니다. | &nbsp; |
| 연속 매개 변수를 사용하는 보고서에 대한 데이터 기반 구독을 만들 수 없습니다. | &nbsp; |
| 잘못된 간격으로 구성된 구독을 편집할 수 없습니다. | &nbsp; |
| 보안 업데이트 | &nbsp; |
| 연결된 보고서 UI가 표시되지 않습니다. | &nbsp; |
| 중첩된 테이블릭스 컨트롤이 있는 특정 페이지를 매긴 보고서의 글꼴이 잘못됨 | &nbsp; |
| 공백이 테이블 릭 스 데이터 영역을 포함 하는 특정 페이지 매긴된 보고서에 올바르게 추가 됩니다. | &nbsp; |
| 모바일 보고서 단순 데이터 표를 확장할 때 머리글 행이 나타나지 않습니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600906-20180912"></a>14.0.600.906, 2018/09/12

다음 문제가 수정되었습니다.

| 문제 해결된 | 세부 정보 |
| :---------- | :------ |
| 사용자 지정 인증이 올바른 쿠키 정보를 반환하지 않습니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600892-20180831"></a>14.0.600.892, 2018/08/31

| 문제 해결된 | 세부 정보 |
| :---------- | :------ |
| 텍스트 상자가 rc:Toolbar=False이고 긴 텍스트를 포함할 때 직사각형 내부의 텍스트 상자가 직사각형의 세로 확장을 차단합니다. | &nbsp; |
| pageHeight가 0.5인치 미만일 때 텍스트 크기가 조절되지 않습니다. | &nbsp; |
| CRM 함께 사용 하는 SSRS 카탈로그 데이터베이스에서 교착 상태가 발생 합니다. | &nbsp; |
| 보고서에서 스크롤할 때 세로로 정렬된 열 머리글이 잘못 표시됩니다. | &nbsp; |
| SCOM Reporting 역할에 추가된 사용자가 SSRS 웹 포털에 액세스할 수 없습니다. | &nbsp; |
| 태국어 문자는 PDF로 올바르게 내보내지지 않습니다. | &nbsp; |
| 브라우저 역할 동작이 변경됩니다. | &nbsp; |
| rc:Toolbar=false가 Express Edition에서 작동하지 않습니다. | &nbsp; |
| 매개 변수 프롬프트 영역에 세로 스크롤 막대가 없습니다. | &nbsp; |
| 모바일 보고서 런타임이 업데이트됩니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600744-20180425"></a>14.0.600.744, 2018/04/25

| 문제 해결된 | 세부 정보 |
| :---------- | :------ |
| 데이터 기반 구독 페이지는 일단 만들어지면 배달 옵션을 표시하지 않습니다. | &nbsp; |
| SSRS 2012를 SSRS 2017로 업그레이드하면 결국 몇 초 마다 예외를 throw하는 RSManagement가 됩니다. | &nbsp; |
| IE11에서 다중 값 매개 변수에 대한 기본값을 변경할 수 없습니다. | &nbsp; |
| 일정은 공유 일정이 실행될 때마다 빕니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600689-20180228"></a>14.0.600.689, 2018/02/28

| 문제 해결된 | 세부 정보 |
| :---------- | :------ |
| 링크된 보고서의 보고서 매개 변수 표시 유형이 해당 속성을 편집한 후에 되돌려집니다. | &nbsp; |
| URL 매개 변수 rc:Toolbar=false가 Express Edition에서 작동하지 않습니다. | &nbsp; |
| 속성의 CanGrow 사용 하 여 텍스트 상자에 식을 사용 하면 표시 되지 않는 값에 false 결과로 설정 합니다. | &nbsp; |
| 설정에서 제품 키에 대한 _자세한 정보_ 링크가 추가됩니다. | &nbsp; |
| 사용자 지정 폼 인증을 사용하는 웹 포털에서 슬라이딩(sliding) 만료 쿠키를 무시합니다. | &nbsp; |
| Word로 내보내기 시 행 콘텐츠가 비어 있으면 행 높이가 서로 다릅니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600594-20180109"></a>14.0.600.594, 2018/01/09

일부 보안 업데이트 구현 되었습니다.

### <a name="140600490-20171101"></a>14.0.600.490, 2017/11/01

SKU 업그레이드에서 해결된 문제입니다.

## <a name="140600451-20170930"></a>14.0.600.451, 2017/09/30

초기 릴리스

## <a name="next-steps"></a>다음 단계

[Reporting Services(SSRS)의 새로운 기능](what-s-new-in-sql-server-reporting-services-ssrs.md)

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하세요](https://go.microsoft.com/fwlink/?LinkId=620231).
