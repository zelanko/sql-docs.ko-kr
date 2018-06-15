---
title: SQL Server Reporting Services(2017 이상)의 변경 로그 | Microsoft Docs
ms.custom: ''
ms.date: 04/25/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: casualoak
ms.author: edugonz
manager: kfile
ms.openlocfilehash: ee37f4445a02925c0017f67d3f25056b047a1f05
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33014200"
---
# <a name="change-log-for-sql-server-reporting-services"></a>SQL Server Reporting Services의 변경 로그

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)] 

이 문서에서는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]의 변경 내용에 대해 설명합니다. 

## <a name="sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services 

- *버전 14.0.600.744, 릴리스됨: 2018년 4월 25일* 
    - 버그 수정:
        - 데이터 기반 구독 페이지는 일단 만들어지면 배달 옵션을 표시하지 않음
        - SSRS 2012를 SSRS 2017로 업그레이드하면 결국 몇 초 마다 예외를 throw하는 RSManagement가 됨
        - IE11에서 다중 값 매개 변수에 대한 기본값을 변경할 수 없음
        - 일정은 공유 일정이 실행될 때마다 빔

- 버전 14.0.600.689, 릴리스 날짜: 2018년 2월 28일 
    - 버그 수정:
        - 링크된 보고서의 보고서 매개 변수 표시 유형이 해당 속성을 편집한 후에 되돌려짐
        - URL 매개 변수 rc:Toolbar=false가 Express Edition에서 작동하지 않음
        - CanGrow 속성을 false로 설정하고 텍스트 상자에서 식을 사용하면 값이 표시되지 않음
        - 설정에서 제품 키에 대한 “자세한 정보” 링크가 추가됨
        - 사용자 지정 폼 인증을 사용하는 웹 포털에서 슬라이딩(sliding) 만료 쿠키를 무시함
        - [Word로 내보내기] 시 행 콘텐츠가 비어 있으면 행 높이가 서로 다름

- *버전 14.0.600.594, 릴리스됨: 2018년 1월 9일*
    - 보안 업데이트

- *버전 14.0.600.490, 릴리스됨: 2017년 11월 1일* 
    - 버그 수정:
        - SKU 업그레이드에서 해결된 문제

- *버전 14.0.600.451, 릴리스됨: 2017년 9월 30일* 
    - 초기 릴리스

## <a name="next-steps"></a>다음 단계

[Reporting Services(SSRS)의 새로운 기능](what-s-new-in-sql-server-reporting-services-ssrs.md)   

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
