---
title: SSRS(SQL Server Reporting Services)(2017 이상)의 변경 로그 | Microsoft Docs
ms.date: 08/31/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
author: casualoak
ms.author: edugonz
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 0ec82a6808b7591603154b7831192598cac34243
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50030130"
---
# <a name="change-log-for-sql-server-reporting-services-ssrs-2017-and-later"></a>SSRS(SQL Server Reporting Services)(2017 이상)의 변경 로그

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)] 

이 문서에서는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 변경 내용에 대해 설명합니다. 

## <a name="sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services 

### <a name="version-140600906-released-september-12-2018"></a>버전 14.0.600.906, 릴리스: 2018년 9월 12일

다음 버그가 수정되었습니다.

- 사용자 지정 인증이 올바른 쿠키 정보를 반환하지 않음

### <a name="version-140600892-released-august-31-2018"></a>버전 14.0.600.892, 릴리스: 2018년 8월 31일

다음 버그가 수정되었습니다.

- 텍스트 상자가 rc:Toolbar=False이고 긴 텍스트를 포함할 때 직사각형 내부의 텍스트 상자가 직사각형의 세로 확장을 차단함 
- pageHeight가 0.5인치 미만일 때 텍스트 크기가 조절되지 않음 
- CRM에서 사용될 때 SSRS 카탈로그 데이터베이스에서 교착 상태 발생 
- 보고서에서 스크롤할 때 세로로 정렬된 열 머리글이 잘못 표시됨 
- SCOM Reporting 역할에 추가된 사용자가 SSRS 웹 포털에 액세스할 수 없음 
- 태국어 문자를 PDF에서 올바르게 내보낼 수 없음 
- 브라우저 역할 동작 변경 
- rc:Toolbar=false가 Express Edition에서 작동하지 않음 
- 매개 변수 프롬프트 영역에 수직 스크롤 막대가 없음 
- 모바일 보고서 런타임이 업데이트됨 

### <a name="version-140600744-released-april-25-2018"></a>버전 14.0.600.744, 릴리스 날짜: 2018년 4월 25일 

다음 버그가 수정되었습니다.

- 데이터 기반 구독 페이지는 일단 만들어지면 배달 옵션을 표시하지 않음
- SSRS 2012를 SSRS 2017로 업그레이드하면 결국 몇 초 마다 예외를 throw하는 RSManagement가 됨
- IE11에서 다중 값 매개 변수에 대한 기본값을 변경할 수 없음
- 일정은 공유 일정이 실행될 때마다 빔

### <a name="version-140600689-released-february-28-2018"></a>버전 14.0.600.689, 릴리스 날짜: 2018년 2월 28일

다음 버그가 수정되었습니다.

- 링크된 보고서의 보고서 매개 변수 표시 유형이 해당 속성을 편집한 후에 되돌려짐
- URL 매개 변수 rc:Toolbar=false가 Express Edition에서 작동하지 않음
- CanGrow 속성을 false로 설정하고 텍스트 상자에서 식을 사용하면 값이 표시되지 않음
- 설정에서 제품 키에 대한 “자세한 정보” 링크가 추가됨
- 사용자 지정 폼 인증을 사용하는 웹 포털에서 슬라이딩(sliding) 만료 쿠키를 무시함
- [Word로 내보내기] 시 행 콘텐츠가 비어 있으면 행 높이가 서로 다름

### <a name="version-140600594-released-january-9-2018"></a>버전 14.0.600.594, 릴리스 날짜: 2018년 1월 9일

보안 업데이트

### <a name="version-140600490-released-november-1-2017"></a>버전 14.0.600.490, 릴리스 날짜: 2017년 11월 1일

다음 버그가 수정되었습니다.

- SKU 업그레이드에서 해결된 문제

### <a name="version-140600451-released-september-30-2017"></a>버전 14.0.600.451, 릴리스 날짜: 2017년 9월 30일 

초기 릴리스

## <a name="next-steps"></a>다음 단계

[Reporting Services(SSRS)의 새로운 기능](what-s-new-in-sql-server-reporting-services-ssrs.md)   

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
