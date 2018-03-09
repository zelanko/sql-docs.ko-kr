---
title: "SQL 모드 (MySQLToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: d840ee51-b863-4e77-84aa-37d3f094bfed
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e3f9271008c9633a5266d2171e7724d259ebae37
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sql-modes-mysqltosql"></a>SQL 모드 (MySQLToSQL)
MySQL 용 SSMA 다른 SQL 모드에서 작동할 수 있습니다 및 다른 클라이언트에 대 한 이러한 모드를 다르게 적용할 수 있습니다.  
  
모드 MySQL 지원 해야 하는 SQL 구문을 정의 하 고 데이터 유효성 검사 유형의 검사 수행 해야 합니다. 이렇게 하면 보다 쉽게 서로 다른 환경에서 MySQL을 사용 하 고 SQL Server와 MySQL을 사용 합니다.  
  
## <a name="sql-modes-grid"></a>SQL 모드 눈금:  
  
-   다음 열을 포함 하는 루트 수준에서 SQL 모드 표: **SQL 모드 이름**, **SQL 모드 로드**, 및 **효과적인 SQL 모드**합니다.  
  
-   SQL 모드 모눈 데이터베이스 범주, 데이터베이스, 테이블 범주, 문 범주, 범주 뷰, 테이블, 뷰, 함수, 프로시저, UDF 및 개체 수준 이벤트에 같은 열이 포함: **SQL 모드 이름**, **SQL 모드 상속**, 및 **효과적인 SQL 모드**합니다.  
  
-   다음 열을 포함 하는 저장 프로시저, 저장 된 함수 및 트리거 수준에서 SQL 모드 표: **SQL 모드 이름**, **원래 SQL 모드**, 및 **효과적인 SQL 모드**합니다.  
  
> [!NOTE]  
> 그룹 모드에 표시 될 열 아래에서 'SQL 모드 Name' 굵게 합니다.  
  
## <a name="loaded-sql-modes"></a>로드 된 SQL 모드  
이들은 세션 또는 루트 수준에서 설정 되는 SQL 모드입니다. 대상 데이터베이스에 로드 된 후 SQL 모드 편집 또는 수정 수 없습니다.  
  
## <a name="inherited-sql-modes"></a>상속 된 SQL 모드  
다음은 해당 부모 노드에서 상속 되는 SQL 모드입니다.  
  
함수 범주, 프로시저 범주, 이벤트 범주 및 트리거를 제외 하 고 이러한 SQL 모드는 모든 수준 (데이터베이스, 테이블 범주, 문 범주, 뷰 범주, 테이블, 뷰, 함수, 프로시저, UDF 및 이벤트 개체)에서 존재 합니다.  
  
> [!NOTE]  
> 선택 하 여는 **부모에서 상속** 부모 노드에서 확인란을 상속 SQL 모드는 상속 될 수 있습니다. 기본적으로이 확인란 선택 되어 있습니다.  
  
## <a name="original-sql-modes"></a>원래 SQL 모드  
이들은 함수, 프로시저 및 트리거 수준에 있는 SQL 모드입니다.  
  
> [!NOTE]  
> 선택 하 여는 **사용 하 여 원래** 확인 상자를 원래 해당 함수에 사용 된 SQL 모드 또는 프로시저 또는 트리거를 사용할 수 있습니다. 기본적으로이 확인란 선택 되어 있습니다.  
  
## <a name="effective-sql-modes"></a>효과적인 SQL 모드  
효과적인 SQL 모드는 다음과 같이 다양 한 수준에서 정의할 수 있습니다.  
  
-   **세션 수준:**  
  
    1.  모든 SQL 로드 모드와 호출할 수 있는 "SQL 모드 효과적인".  
  
    2.  이 수준에서 유효한 SQL 모드 수정할 수 있습니다 직접 하 고 명시적으로.  
  
    3.  명시적으로 설정 하는 유효한 SQL 모드 SQL 모드로 로드 반영 되지 않으며 마지막으로 개체에 적용 됩니다.  
  
-   **수준 함수 또는 프로시저 또는 트리거:**  
  
    1.  원래 모든 SQL 모드와 호출할 수 있는 "효과적인 SQL 모드"입니다.  
  
    2.  이 수준에서 적용 되는 SQL 모드가 수정할 수 있는 명시적으로 경우에만 **사용 하 여 원래** 확인란을 선택 취소 합니다.  
  
    3.  명시적으로 설정 하는 유효한 SQL 모드 원래 SQL 모드도 반영 되지 않으며 마지막으로 개체에 적용 됩니다.  
  
-   **함수 또는 프로시저 또는 트리거 수준이 아닌 노드:**  
  
    1.  모든 상속 SQL 모드와 호출할 수 있는 "SQL 모드 효과적인"입니다.  
  
    2.  이 수준에서 적용 되는 SQL 모드가 수정할 수 있는 명시적으로 경우에만 **부모에서 상속** 확인란을 선택 취소 합니다.  
  
    3.  명시적으로 설정 하는 유효한 SQL 모드 SQL 모드 상속으로 반영 되지 않으며 마지막으로 개체에 적용 됩니다.  
  
