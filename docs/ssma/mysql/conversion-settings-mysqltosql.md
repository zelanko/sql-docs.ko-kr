---
title: 변환 설정 (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f551cf6e-1575-4206-9cca-975b5b43a6b8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: fee221caf91d5d70f291f9351d05a00352e7cc00
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63253256"
---
# <a name="conversion-settings-mysqltosql"></a>변환 설정(MySQLToSQL)
합니다 **'설정'** 탭 노드 수준 설정을 설정할 수 있습니다. 탭은 다음 메타 베이스 노드에서 사용할 수 있습니다.  
  
-   데이터베이스 노드  
  
-   함수 범주  
  
-   노드 함수  
  
-   테이블 범주  
  
-   테이블 노드  
  
## <a name="specifications"></a>사양:  
합니다 **설정을** 탭, 두 개의 사용자 설정이 보도.:  
  
1.  함수 변환  
  
2.  테이블 변환  
  
메타 베이스 노드 유형에 따라 이러한 설정을 사용할 수는 있습니다. 예를 들어, 함수 변환 관련 설정 테이블 노드에 사용할 수는  
  
> [!NOTE]  
> -   사용자가 변경한 프로젝트 작업 영역에서 별도 기본 설정 파일으로 저장 됩니다.  
> -   이 파일의 확장명이 됩니다 **ccprefs**합니다.  
  
1.  **함수 변환 설정:**  
  
    1.  이 탭에 **'강제 함수 변환'** 옵션입니다. 옵션은 다음 네 가지 값 중 하나일 수 있습니다.  
  
        -   프로젝트 설정 [상속]에 따라 변환  
  
        -   항상 함수 변환  
  
        -   프로시저에 항상 변환  
  
        -   프로젝트 설정에 따라 변환  
  
    2.  설정에 따라, 함수는 변환 함수 또는 저장된 프로시저.  
  
    3.  사용자가 변경한 설정을 클릭 하 여 종속 연결 된 기본 설정 파일에 저장 됩니다 **적용** 단추입니다.  
  
2.  **테이블 변환 설정:**  
  
    1.  이 탭에 **'표시 안 함 ROWID 보조 열 생성'** 옵션입니다. 옵션은 다음 네 가지 값 중 하나일 수 있습니다.  
  
        -   프로젝트 설정 [상속]에 따라 변환  
  
        -   사용자 계정 컨트롤  
  
        -   아니요  
  
        -   프로젝트 설정에 따라 변환  
  
    2.  하는 경우 **'예'**,이 설정은 ROWID 보조 열 작성 대상 테이블 만들기를 금지 합니다.  
  
    3.  사용자가 변경한 설정을 클릭 하 여 종속 연결 된 기본 설정 파일에 저장 됩니다 **적용** 단추입니다.  
  
## <a name="see-also"></a>관련 항목  
[프로젝트 설정 (변환) (MySQL to SQL)](https://msdn.microsoft.com/7ad5fe44-6445-4ba8-a457-5af792631f11)  
  
