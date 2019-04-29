---
title: SQL 모드 (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d840ee51-b863-4e77-84aa-37d3f094bfed
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6965d67b6dae484b3fa72f215446682f9aa6760c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028370"
---
# <a name="sql-modes-mysqltosql"></a>SQL 모드(MySQLToSQL)
MySQL 용 SSMA 다른 SQL 모드로 작동할 수 있으며 다른 클라이언트에 대 한 이러한 모드를 다르게 적용할 수 있습니다.  
  
모드 MySQL 지원 해야 하는 SQL 구문 정의 및 종류의 데이터 유효성 검사 확인 수행 해야 합니다. 그러면 다양 한 환경에서 MySQL을 사용 하 고 MySQL을 사용 하 여 SQL Server를 사용 하 여 더 쉽습니다.  
  
## <a name="sql-modes-grid"></a>SQL 모드 표:  
  
-   루트 수준에서 SQL 모드 표에 다음 열을 있습니다. **SQL 모드 이름**, **SQL 모드 로드**, 및 **효과적인 SQL 모드**합니다.  
  
-   SQL 모드 표에 데이터베이스 범주, 데이터베이스, 테이블 범주, 문 범주, 범주 뷰, 테이블, 뷰, 함수, 프로시저, UDF 및 이벤트 개체 수준에서 다음 열을 있습니다. **SQL 모드 이름**, **SQL 모드를 상속**, 및 **효과적인 SQL 모드**합니다.  
  
-   저장 프로시저, 저장 된 함수 및 트리거 수준에서 SQL 모드 표에 다음 열을 있습니다. **SQL 모드 이름**, **원래 SQL 모드**, 및 **효과적인 SQL 모드**합니다.  
  
> [!NOTE]  
> 그룹 모드에서 표시할 열 아래에 있는 'SQL 모드 Name' 굵게입니다.  
  
## <a name="loaded-sql-modes"></a>로드 된 SQL 모드  
이들은 세션 또는 루트 수준에서 설정 되는 SQL 모드입니다. 대상 데이터베이스에 로드 된 후 SQL 모드를 편집 하거나 수정할 수 없습니다.  
  
## <a name="inherited-sql-modes"></a>상속 된 SQL 모드  
이 해당 부모 노드에서 상속 된 SQL 모드입니다.  
  
함수 범주, Procedures 범주, 이벤트 범주 및 트리거를 제외 하 고 이러한 SQL 모드는 모든 수준 (데이터베이스, 테이블 범주, 문 범주, 보기 범주, 테이블, 뷰, 함수, 프로시저, UDF 및 이벤트 개체)에서 제공 합니다.  
  
> [!NOTE]  
> 선택 하 여 합니다 **부모에서 상속** 부모 노드에서 상속 SQL 모드 확인란을 상속할 수 있습니다. 기본적으로이 확인란이 선택 되어 있습니다.  
  
## <a name="original-sql-modes"></a>원래 SQL 모드  
이 함수, 프로시저 및 트리거 수준에 있는 SQL 모드입니다.  
  
> [!NOTE]  
> 선택 하 여 합니다 **사용 하 여 원래** 확인 상자에 해당 하는 함수에 원래 사용 된 SQL 모드 또는 프로시저 또는 트리거를 사용할 수 있습니다. 기본적으로이 확인란이 선택 되어 있습니다.  
  
## <a name="effective-sql-modes"></a>유효한 SQL 모드  
유효한 SQL 모드는 다음과 같이 다양 한 수준에서 정의할 수 있습니다.  
  
-   **세션 수준:**  
  
    1.  모든 SQL 로드 모드를 호출할 수 있습니다, "유효 SQL 모드"입니다.  
  
    2.  이 수준에서는 효과적인 SQL 모드 직접 및 명시적으로 수정할 수 있습니다.  
  
    3.  명시적으로 설정 된 SQL 모드를 효과적으로 SQL 모드 로드 반영 되지 않으며 마지막으로 개체에 적용 됩니다.  
  
-   **수준 함수 또는 프로시저 또는 트리거:**  
  
    1.  원래 모든 SQL 모드 호출할 수 있습니다, "유효 SQL 모드".  
  
    2.  이 수준에서는 효과적인 SQL 모드를 명시적으로 수정할 수 경우에만 합니다 **사용 하 여 원래** 확인란이 선택 되지 않습니다.  
  
    3.  명시적으로 설정 되는 유효한 SQL 모드는 원래 SQL 모드로 반영 되지 않으며 개체에 마지막으로 적용 됩니다.  
  
-   **함수 또는 프로시저 또는 트리거 수준이 아닌 노드에서:**  
  
    1.  모든 SQL 상속 모드를 호출할 수 있습니다, "유효 SQL 모드"입니다.  
  
    2.  이 수준에서는 효과적인 SQL 모드를 명시적으로 수정할 수 경우에만 합니다 **부모에서 상속** 확인란이 선택 되지 않습니다.  
  
    3.  명시적으로 설정 된 SQL 모드를 효과적으로 SQL 모드 상속 반영 되지 않으며 마지막으로 개체에 적용 됩니다.  
  
