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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 146e6975dd8880f750e7bb449e8d42ca3e6a4e62
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87931917"
---
# <a name="creating-test-cases-sybasetosql"></a>테스트 사례 만들기(SybaseToSQL)
테스트 사례 마법사를 사용 하 여 테스트를 만듭니다. 이 마법사를 사용 하면 테스트 되 고 확인 된 개체를 선택 하 고 테스트 매개 변수를 지정 하 여 테스트 사례를 만들 수 있습니다.  
  
## <a name="starting-the-test-case-wizard"></a>테스트 사례 마법사 시작  
테스트 사례 마법사를 시작 하려면 **테스터** 메뉴에서 **새 테스트 사례 ...** 를 클릭 합니다.  
  
시작 하면 마법사가 원본 Sybase 서버에서 데이터베이스 ssmatester2005db 또는 ssmatester2008db (프로젝트 형식에 따라 다름)를 찾습니다. 보조 개체를 저장 하는 데 사용 되는 테스터 확장 스키마입니다. 테스트 사례 마법사에서 ssmatester2005db 또는 ssmatester2008db를 찾을 수 없는 경우 테스터 확장 데이터베이스를 만들 것을 제안 하는 대화 상자 창이 표시 됩니다. 이 상황은 일반적으로 SSMA 테스터를 처음 실행 하는 동안 발생 합니다.  
  
대화 상자가 나타나면 **예** 를 클릭 하 여 원본 서버에 Sybase 테스터 데이터베이스를 만듭니다. 그러면 새 테스터 데이터베이스를 찾을 장치를 하나 이상 추가 해야 하는 새 대화 상자 창이 표시 됩니다. **추가** 를 클릭 하 여 장치를 추가 합니다. **테스터 데이터베이스 할당 공간** 대화 상자에서 장치를 선택 하 고 테스터 데이터베이스에 사용 되는 크기를 지정 합니다. 또한 데이터베이스 로그에 대 한 별도의 장치를 설정할 수 있습니다. 데이터베이스를 만들려면 Sybase 권한이 있어야 합니다.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>마법사를 사용 하 여 테스트 사례 만들기 개요  
테스트 사례를 만드는 프로세스는 다음 5 단계로 구성 됩니다.  
  
1.  [테스트 사례 &#40;SybaseToSQL&#41;를 초기화 ](../../ssma/sybase/initializing-test-cases-sybasetosql.md)합니다.  
  
2.  [&#40;SybaseToSQL&#41;를 테스트할 개체 선택 및 구성 ](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)  
  
3.  [영향을 받는 개체를 선택 하 고 구성 &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)합니다.  
  
4.  [호출 순서 사용자 지정 &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md).  
  
5.  [테스트 사례 준비 &#40;SybaseToSQL&#41;를 완료 ](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
[마이그레이션된 데이터베이스 개체 테스트 &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
