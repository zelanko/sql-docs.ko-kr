---
title: 테스트 사례 보고서 보기 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Case Reports
ms.assetid: cb75d281-43ef-4f4a-b754-2c4ee3b62ae7
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 99bad46468ff0138c07f531c9e32cdecc4fda5be
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934527"
---
# <a name="viewing-test-case-reports-sybasetosql"></a>테스트 사례 보고서 보기(SybaseToSQL)
테스트 사례 보고서는 테스트 확인 결과 및 일반 테스트 정보를 표시 합니다. 테스트에 실패 하는 경우 확인 된 개체의 일치 하지 않는 데이터에 대 한 정보도 표시 됩니다.  
  
## <a name="report-structure"></a>보고서 구조  
보고서 맨 위에는 다음과 같은 통계가 표시 됩니다.  
  
-   테스트 된 개체의 총 수와 테스트가 성공한 개체의 수입니다.  
  
-   확인 된 테이블 및 외래 키의 총 수와 성공적으로 일치 시킨 테이블 및 외래 키의 수입니다.  
  
-   테스트 사례의 시작 시간, 종료 시간 및 실행에 소요 된 총 시간입니다.  
  
보고서의 나머지 부분에서는 다음 네 가지 범주로 정보를 표시 합니다.  
  
**필수 조건 오류**  
**필수 조건** 단계에서 발생 한 모든 오류를 표시 합니다. 일반적으로 건너뜁니다.  
  
**초기화**  
실행 상태를 **성공** 또는 **실패로**표시 합니다.  
  
**테스트 개체 결과**  
결과 (성공 또는 실패)와 오류 발생 시 SSMA 테스터가 감지한 불일치를 비교한 결과입니다.  
  
**종료**  
실행 상태를 **성공** 또는 **실패로**표시 합니다.  
  
## <a name="see-also"></a>참고 항목  
[테스트 사례 실행 &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[마이그레이션된 데이터베이스 개체 테스트 &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
