---
title: SQL 모드 (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d840ee51-b863-4e77-84aa-37d3f094bfed
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 4bc4b59984cc9e2e1f7a6c358f24e3fc0d2e86be
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935102"
---
# <a name="sql-modes-mysqltosql"></a>SQL 모드(MySQLToSQL)
MySQL 용 SSMA는 서로 다른 SQL 모드에서 작동할 수 있으며 클라이언트 마다 이러한 모드를 다르게 적용할 수 있습니다.  
  
모드는 MySQL에서 지원 해야 하는 SQL 구문과 이러한 구문이 수행 해야 하는 데이터 유효성 검사의 종류를 정의 합니다. 이렇게 하면 다양 한 환경에서 MySQL을 보다 쉽게 사용할 수 있고 SQL Server에 MySQL을 사용할 수 있습니다.  
  
## <a name="sql-modes-grid"></a>SQL 모드 표:  
  
-   루트 수준의 SQL 모드 표는 **Sql 모드 이름**, **로드 된 Sql 모드**및 **유효 sql 모드**열을 포함 합니다.  
  
-   데이터베이스 범주, 데이터베이스, 테이블 범주, 문 범주, 뷰 범주, 테이블, 뷰, 함수, 프로시저, UDF 및 이벤트 개체 수준의 SQL 모드 표는 **Sql 모드 이름**, **상속 된 Sql 모드**및 **유효 sql 모드**열을 포함 합니다.  
  
-   저장 프로시저, 저장 된 함수 및 트리거 수준의 SQL 모드 표는 **Sql 모드 이름**, **원본 Sql 모드**및 **유효 sql 모드**열을 포함 합니다.  
  
> [!NOTE]  
> 그룹 모드는 ' SQL 모드 이름 ' 열 아래에 굵게 표시 됩니다.  
  
## <a name="loaded-sql-modes"></a>로드 된 SQL 모드  
이러한 모드는 세션 또는 루트 수준에서 설정 되는 SQL 모드입니다. 대상 데이터베이스에 로드 된 SQL 모드를 편집 하거나 수정할 수 없습니다.  
  
## <a name="inherited-sql-modes"></a>상속 된 SQL 모드  
이러한 항목은 해당 부모 노드에서 상속 되는 SQL 모드입니다.  
  
함수 범주, 프로시저 범주, 이벤트 범주 및 트리거를 제외 하 고 이러한 SQL 모드는 모든 수준 (데이터베이스, 테이블 범주, 문 범주, 뷰 범주, 테이블, 뷰, 함수, 프로시저, UDF 및 이벤트 개체)으로 제공 됩니다.  
  
> [!NOTE]  
> **부모 로부터 상속** 확인란을 선택 하 여 상속 된 SQL 모드를 부모 노드에서 상속할 수 있습니다. 기본적으로이 확인란은 선택 된 상태로 유지 됩니다.  
  
## <a name="original-sql-modes"></a>원본 SQL 모드  
함수, 프로시저 및 트리거 수준 에서만 제공 되는 SQL 모드입니다.  
  
> [!NOTE]  
> **원래 사용** 확인란을 선택 하면 해당 함수나 프로시저 또는 트리거에서 원래 사용 된 SQL 모드를 사용할 수 있습니다. 기본적으로이 확인란은 선택 된 상태로 유지 됩니다.  
  
## <a name="effective-sql-modes"></a>유효한 SQL 모드  
유효한 SQL 모드는 다음과 같은 방식으로 다양 한 수준에서 정의 될 수 있습니다.  
  
-   **세션 수준:**  
  
    1.  로드 된 모든 SQL 모드를 "유효한 SQL 모드" 라고 할 수 있습니다.  
  
    2.  이 수준에서 유효 SQL 모드는 직접 및 명시적으로 수정할 수 있습니다.  
  
    3.  명시적으로 설정 된 유효한 SQL 모드는 로드 된 SQL 모드로 반영 되지 않으며 마지막으로 개체에 적용 됩니다.  
  
-   **함수, 프로시저 또는 트리거 수준에서:**  
  
    1.  모든 원본 SQL 모드를 "유효한 SQL 모드" 라고 할 수 있습니다.  
  
    2.  이 수준에서 유효 SQL 모드는 **원래 대로 사용** 확인란의 선택을 취소 한 경우에만 명시적으로 수정할 수 있습니다.  
  
    3.  명시적으로 설정 된 유효한 SQL 모드는 원래 SQL 모드로 반영 되지 않으며 마지막으로 개체에 적용 됩니다.  
  
-   **함수, 프로시저 또는 트리거 수준 이외의 노드에서:**  
  
    1.  모든 상속 된 SQL 모드를 "유효 SQL 모드" 라고 합니다.  
  
    2.  이 수준에서 유효한 SQL 모드는 **부모 로부터 상속** 확인란이 선택 취소 된 경우에만 명시적으로 수정할 수 있습니다.  
  
    3.  명시적으로 설정 된 유효한 SQL 모드는 상속 된 SQL 모드로 반영 되지 않으며 마지막으로 개체에 적용 됩니다.  
  
