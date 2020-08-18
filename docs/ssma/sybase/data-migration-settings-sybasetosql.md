---
description: 데이터 마이그레이션 설정(SybaseToSQL)
title: 데이터 마이그레이션 설정 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94d7a083-2dbc-4e3d-94dd-92b7ff9d0c2d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1d86fbfceefd3f0a4fba6f3bb86a071736e12c54
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492237"
---
# <a name="data-migration-settings-sybasetosql"></a>데이터 마이그레이션 설정(SybaseToSQL)
  
## <a name="data-migration-settings"></a>데이터 마이그레이션 설정  
**데이터 마이그레이션 설정을** 사용 하면 사용자가 데이터 마이그레이션에 대 한 사용자 지정 쿼리를 작성할 수 있습니다.  
  
-   이 탭은 **확장 데이터 마이그레이션 옵션이** **표시** 로 설정 된 경우에 사용할 수 있으며, 설정이 프로젝트 설정에서 **숨기기** 로 설정 된 경우에는 숨겨집니다. 프로젝트 마이그레이션 설정에 대 한 자세한 내용은 [프로젝트 설정 (마이그레이션)](https://msdn.microsoft.com/82f8857f-7ab1-4738-ab6e-b1e95ea94924) 을 참조 하세요.  
  
-   사용자 지정 SQL 문의 구문 분석은 테이블 노드의 **데이터 마이그레이션 설정** 탭에서 구현 됩니다.  
  
-   **데이터 마이그레이션 설정** 시각화에서 사용할 수 있는 두 가지 확인란은 다음과 같습니다.  
  
    1.  SQL Server 테이블 자르기  
  
    2.  사용자 지정 선택 사용  
  
1.  **SQL Server 테이블 자르기:**  
     이 옵션을 사용 하면 사용자가 대상 데이터베이스에서 마이그레이션된 데이터를 명확 하 게 볼 수 있습니다.  
  
    -   이 텍스트 상자는 기본적으로 선택 되어 있습니다.  
  
    -   이 텍스트 상자를 선택 하지 않으면 마이그레이션되는 데이터가 대상 데이터베이스의 기존 데이터에 추가 됩니다.  
  
2.  **사용자 지정 선택 사용:**  
     이 옵션을 사용 하면 사용자가 **select** 문 표시를 수정할 수 있습니다.**select** 문을 사용 하 여 대상 데이터베이스에 표시할 데이터를 선택할 수 있습니다.  
  
    1.  이 텍스트 상자는 기본적으로 선택 되어 있지 않습니다.  
  
    2.  이 텍스트 상자를 선택 하면 사용자가 **선택** 된 문을 수정할 수 있습니다.  
  
시각화에는 두 가지 단추가 있습니다.  
  
-   **적용:** **적용** 을 클릭 하 여 변경 된 설정을 적용 합니다.  
  
-   **취소:** 변경을 수행 하기 전에 표시 되는 설정을 복원 하려면 **취소** 를 클릭 합니다.  
  
## <a name="see-also"></a>참고 항목  
[Sybase 데이터를 SQL Server/SQL Azure으로 마이그레이션](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811)  
  
