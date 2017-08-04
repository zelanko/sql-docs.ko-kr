---
title: "변환 설정 (MySQLToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: f551cf6e-1575-4206-9cca-975b5b43a6b8
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b83e86ce201343d624974244a9d551fb1016d3e7
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="conversion-settings-mysqltosql"></a>변환 설정 (MySQLToSQL)
**'설정'** 탭 노드 수준 설정을 지정 하려면 사용자 수 있습니다. 탭에서 메타 베이스에 있는 다음 노드에서 사용할 수 있습니다.  
  
-   데이터베이스 노드  
  
-   함수 범주  
  
-   노드 함수  
  
-   테이블 범주  
  
-   테이블 노드  
  
## <a name="specifications"></a>사양:  
**설정을** 탭에는 두 개의 사용자 설정 viz.:  
  
1.  함수 변환  
  
2.  테이블 변환  
  
메타 베이스 노드 형식에 따라 이러한 설정을 사용할 수는 있습니다. 예를 들어 설정 관련 함수 변환 테이블 노드의에서 사용할 수는  
  
> [!NOTE]  
> -   사용자가 변경한 프로젝트 작업 영역에서 별도 기본 설정 파일로 저장 됩니다.  
> -   이 파일의 확장명이 됩니다 **ccprefs**합니다.  
  
1.  **함수 변환 설정입니다.**  
  
    1.  이 탭에 **'함수 변환을 강제 실행'** 옵션입니다. 옵션은 다음 네 가지 값 중 하나일 수 있습니다.  
  
        -   프로젝트 설정 [상속]에 따라 변환  
  
        -   함수에 항상 변환  
  
        -   프로시저에 항상 변환  
  
        -   프로젝트 설정에 따라 변환  
  
    2.  설정에 따라 함수 변환 됩니다. 함수 또는 저장된 프로시저.  
  
    3.  사용자가 변경한 설정을 클릭 하면 종속 연결 된 기본 설정 파일에 저장 됩니다 **적용** 단추입니다.  
  
2.  **테이블 변환 설정입니다.**  
  
    1.  이 탭에 **'ROWID 표시 하지 않는 보조 열 생성'** 옵션입니다. 옵션은 다음 네 가지 값 중 하나일 수 있습니다.  
  
        -   프로젝트 설정 [상속]에 따라 변환  
  
        -   예  
  
        -   아니요  
  
        -   프로젝트 설정에 따라 변환  
  
    2.  경우 **'예'**,이 설정은 대상 테이블에 ROWID 보조 열 작성 만들기를 사용할 수 없습니다.  
  
    3.  사용자가 지정한 설정을 클릭 종속 연결 된 기본 설정 파일에 저장 됩니다 **적용** 단추입니다.  
  
## <a name="see-also"></a>참고 항목  
[프로젝트 설정 (변환) (MySQL to SQL)](http://msdn.microsoft.com/en-us/7ad5fe44-6445-4ba8-a457-5af792631f11)  
  

