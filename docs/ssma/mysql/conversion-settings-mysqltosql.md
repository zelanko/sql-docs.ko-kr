---
description: 변환 설정(MySQLToSQL)
title: 변환 설정 (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f551cf6e-1575-4206-9cca-975b5b43a6b8
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1652913173dcd7427515db8c74d15afc75077820
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988639"
---
# <a name="conversion-settings-mysqltosql"></a>변환 설정(MySQLToSQL)
사용자는 **' 설정 '** 탭에서 노드 수준 설정을 지정할 수 있습니다. 이 탭은 다음 메타 베이스 노드에서 사용할 수 있습니다.  
  
-   데이터베이스 노드  
  
-   함수 범주  
  
-   Function 노드  
  
-   테이블 범주  
  
-   테이블 노드  
  
## <a name="specifications"></a>조건  
**설정** 탭에는 시각화 라는 두 개의 사용자 설정이 있습니다.  
  
1.  함수 변환  
  
2.  테이블 변환  
  
이러한 설정은 메타 베이스 노드의 유형에 따라 사용할 수 있습니다. 예를 들어 함수 변환 관련 설정은 테이블 노드에서 사용할 수 없습니다.  
  
> [!NOTE]  
> -   사용자가 변경한 내용은 별도의 기본 설정 파일로 프로젝트 작업 영역에 저장 됩니다.  
> -   이 파일의 확장명은 **ccprefs**이 됩니다.  
  
1.  **함수 변환 설정:**  
  
    1.  이 탭에는 **' 함수 변환 강제 '** 옵션이 포함 되어 있습니다. 옵션은 다음 네 가지 값 중 하나를 사용할 수 있습니다.  
  
        -   프로젝트 설정에 따라 변환 [상속 됨]  
  
        -   항상 함수로 변환  
  
        -   항상 프로시저로 변환  
  
        -   프로젝트 설정에 따라 변환  
  
    2.  설정에 따라 함수는 함수 또는 저장 프로시저 중 하나로 변환 됩니다.  
  
    3.  적용 단추를 클릭 하면 사용자가 **적용** 한 설정이 종속 된 기본 설정 파일에 저장 됩니다.  
  
2.  **테이블 변환 설정:**  
  
    1.  이 탭에는 **' ROWID 보조 열 생성 무시 '** 옵션이 포함 되어 있습니다. 옵션은 다음 네 가지 값 중 하나를 사용할 수 있습니다.  
  
        -   프로젝트 설정에 따라 변환 [상속 됨]  
  
        -   예  
  
        -   아니요  
  
        -   프로젝트 설정에 따라 변환  
  
    2.  **' 예 '** 이면이 설정으로 인해 대상 테이블에 대해 ROWID 보조 열 만들기가 생성 되지 않습니다.  
  
    3.  사용자가 적용 한 설정은 **적용** 단추를 클릭 하면 종속 된 기본 설정 파일에 저장 됩니다.  
  
## <a name="see-also"></a>참고 항목  
[프로젝트 설정 (변환) (MySQL에서 SQL로)](./project-settings-conversion-mysqltosql.md)  
