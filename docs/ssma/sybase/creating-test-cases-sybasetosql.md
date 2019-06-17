---
title: 테스트 사례 만들기 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester component,Test Case Wizard
ms.assetid: b52dfd93-95af-4299-bc8f-83f2a7a6a518
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3fd443ff2ad58aa503fac2960016cb55f35b8a7f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298370"
---
# <a name="creating-test-cases-sybasetosql"></a>테스트 사례 만들기(SybaseToSQL)
테스트를 만드는 테스트 사례 마법사를 사용 합니다. 이 마법사를 사용 하면 테스트 매개 변수를 지정 하 고 테스트 하 고 개체를 확인을 선택 하 여 테스트 사례를 만들 수 있습니다.  
  
## <a name="starting-the-test-case-wizard"></a>테스트 사례 마법사 시작  
테스트 사례 마법사를 시작 하려면 **새 테스트 사례는 중...**  에서 합니다 **테스터** 메뉴.  
  
시작 되 면 마법사 데이터베이스 ssmatester2005db 또는 Sybase 원본 서버에서 (프로젝트 유형에 따라) ssmatester2008db 찾습니다. 보조 개체를 저장 하는 데 사용 되는 테스터 확장 스키마 이며 테스트 사례 마법사 ssmatester2005db 또는 ssmatester2008db을 찾지 못하면 테스터 확장 데이터베이스를 만들려고 제안 하는 대화 상자 창이 표시 됩니다. (이 경우 일반적으로 발생 SSMA 테스터의 첫 번째 실행 중입니다.)  
  
대화 상자 창에 표시 되 면 클릭 **예** 원본 서버에서 Sybase 테스터 데이터베이스를 만들려고 합니다. 그런 다음 새 테스터 데이터베이스를 찾을 수 있는 하나 이상의 장치 추가 해야 하는 새 대화 상자 창이 나타납니다. 클릭 **추가** 는 장치를 추가 합니다. 에 **테스터 데이터베이스에 대 한 공간 할당** 대화 장치를 선택 하 고 테스터 데이터베이스에서 사용 되는 크기를 지정 합니다. 또한 데이터베이스 로그에 대 한 별도 장치를 설정할 수 있습니다. Sybase 데이터베이스를 만들 권한이 있어야 하는 참고 합니다.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>마법사를 사용 하 여 테스트 사례 만들기 개요  
테스트 사례를 만드는 프로세스는 5 단계로 구성 됩니다.  
  
1.  [테스트 사례 초기화 &#40;SybaseToSQL&#41;](../../ssma/sybase/initializing-test-cases-sybasetosql.md)합니다.  
  
2.  [테스트할 개체 선택 및 구성 &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)합니다.  
  
3.  [영향을 받는 개체 선택 및 구성 &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)합니다.  
  
4.  [호출 순서 사용자 지정 &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)합니다.  
  
5.  [테스트 사례 준비 완료 &#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
[마이그레이션된 데이터베이스 개체 테스트 &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
