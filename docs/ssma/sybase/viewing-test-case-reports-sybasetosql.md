---
title: "테스트 사례 보고서 (SybaseToSQL) 보기 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Test Case Reports
ms.assetid: cb75d281-43ef-4f4a-b754-2c4ee3b62ae7
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6ac96a35ea5f97ef58be45b2fbd2a04980f8b4cb
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="viewing-test-case-reports-sybasetosql"></a>테스트 사례 (SybaseToSQL) 보고서 보기
테스트 사례 보고서에서는 테스트 확인 결과 및 일반 테스트 정보를 보여 줍니다. 테스트 실패 시 확인 된 개체의 모든 일치 하지 않는 데이터에 대 한 정보가 표시 됩니다.  
  
## <a name="report-structure"></a>보고서 구조  
보고서의 위쪽이이 통계를 보여 줍니다.  
  
-   테스트 된 개체 및 테스트에 성공 하는 개체 수의 총 수입니다.  
  
-   확인 된 테이블과 외래 키의 총 수 및 테이블과 성공적으로 일치 하는 외래 키의 수입니다.  
  
-   시작 시간, 테스트 사례의 종료 시간 및 실행에 걸린 총 시간입니다.  
  
보고서의 나머지 4 개 범주로 정보가 표시 됩니다.  
  
**필수 구성 요소 오류**  
발생 한 오류 표시는 **필수 구성 요소** 단계입니다. 일반적으로 것은 생략 됩니다.  
  
**초기화**  
으로 실행의 상태를 표시 **성공** 또는 **오류**합니다.  
  
**테스트 결과 개체**  
결과 (성공 또는 실패) 및 오류 발생 시 SSMA 테스터 검색 불일치 비교 합니다.  
  
**종료**  
으로 실행의 상태를 표시 **성공** 또는 **오류**합니다.  
  
## <a name="see-also"></a>관련 항목:  
[테스트 사례 &#40; 실행 SybaseToSQL &#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[데이터베이스 개체 &#40; 마이그레이션 테스트 SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  

