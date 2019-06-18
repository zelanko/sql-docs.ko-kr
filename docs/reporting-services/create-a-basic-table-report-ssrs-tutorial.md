---
title: 기본 테이블 보고서 만들기(SSRS 자습서) | Microsoft Docs
ms.date: 04/16/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- walkthroughs [Reporting Services]
- tutorials [Reporting Services]
- reports [Reporting Services], creating
ms.assetid: 3b539b4b-26f2-4c0b-b506-80f175679a46
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: af41da75d553794019f1d01c8b8f5bb6aba80622
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65103309"
---
# <a name="create-a-basic-table-report-ssrs-tutorial"></a>기본 테이블 보고서 만들기(SSRS 자습서)

이 자습서에서는 Visual Studio/SSDT(SQL Server Data Tools)의 ‘보고서 디자이너’ 도구를 사용합니다.  SSRS(SQL Server Reporting Services) 페이지를 매긴 보고서를 만듭니다. 보고서에는 AdventureWorks2016 데이터베이스의 데이터로 만든 쿼리 테이블이 포함됩니다.

이 자습서를 진행하면서 다음 작업을 수행하는 방법을 알아보겠습니다.
  
- 보고서 프로젝트 만들기
- 데이터 연결 설정
- 쿼리 정의
- 테이블 데이터 영역 추가
- 보고서 서식 지정
- 필드 그룹화 및 합산
- 보고서 미리 보기
- 필요에 따라 보고서 게시

## <a name="requirements"></a>요구 사항

이 자습서를 수행하려면 시스템에 다음 구성 요소가 설치되어 있어야 합니다.

- [!INCLUDE[msconame-md](../includes/msconame-md.md)] SQL Server 데이터베이스 엔진.  
- SQL Server 2016 Reporting Services 이상(SSRS)
- AdventureWorks2016 데이터베이스.  자세한 내용은 [Adventure Works 샘플 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases)를 참조하세요.
- Visual Studio용 [SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md) 및 ‘보고서 디자이너’에 액세스하기 위한 Reporting Services 확장. 
  
또한 AdventureWorks2016 데이터베이스에서 데이터를 검색하려면 읽기 전용 권한이 있어야 합니다.

**자습서에 소요되는 예상 시간:** 30분

## <a name="next-steps"></a>다음 단계

[1단원: 보고서 서버 프로젝트 만들기&#40;Reporting Services&#41;](lesson-1-creating-a-report-server-project-reporting-services.md)

[2단원: 연결 정보 지정&#40;Reporting Services&#41;](lesson-2-specifying-connection-information-reporting-services.md)

[3단원: 테이블 보고서에 대한 데이터 세트 정의&#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)

[4단원: 보고서에 테이블 추가&#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md)

[5단원: 보고서 서식 지정&#40;Reporting Services&#41;](lesson-5-formatting-a-report-reporting-services.md)

[6단원: 그룹화 및 합계 추가&#40;Reporting Services&#41;](lesson-6-adding-grouping-and-totals-reporting-services.md)

## <a name="see-also"></a>관련 항목:

[Reporting Services 자습서](reporting-services-tutorials-ssrs.md) 추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
