---
title: 애플리케이션 역할 만들기 | Microsoft 문서
description: SQL Server Management Studio 또는 Transact-SQL을 사용하여 애플리케이션을 통한 데이터베이스 액세스를 제한하는 애플리케이션 역할을 SQL Server에서 만듭니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.approle.general.f1
helpviewer_keywords:
- application roles [SQL Server], creating
ms.assetid: 6b8da1f5-3d8e-4f88-b111-b915788b06f1
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: df42c1651d460b0be7b0e2900338982168ebd597
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468564"
---
# <a name="create-an-application-role"></a>애플리케이션 역할 만들기
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 애플리케이션 역할을 만드는 방법에 대해 설명합니다. 애플리케이션 역할은 특정 애플리케이션을 통한 경우를 제외하고 데이터베이스에 대한 사용자 액세스를 제한합니다. 애플리케이션 역할에 사용자가 없으므로 **애플리케이션 역할** 을 선택하면 **역할 멤버** 목록이 표시되지 않습니다.  
  
> [!IMPORTANT]  
>  애플리케이션 역할 암호가 설정된 경우 암호 복잡성이 검사됩니다. 애플리케이션 역할을 호출하는 애플리케이션은 해당 암호를 저장해야 합니다. 애플리케이션 역할 암호는 항상 암호화된 상태로 저장되어야 합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 애플리케이션 역할을 만듭니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 데이터베이스에 대한 ALTER ANY APPLICATION ROLE 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
##### <a name="to-create-an-application-role"></a>애플리케이션 역할을 만들려면  
  
1.  개체 탐색기에서 애플리케이션 역할을 만들 데이터베이스를 확장합니다.  
  
2.  **보안** 폴더를 확장합니다.  
  
3.  **역할** 폴더를 확장합니다.  
  
4.  **애플리케이션 역할** 폴더를 마우스 오른쪽 단추로 클릭한 다음, **새 애플리케이션 역할...** 을 선택합니다.  
  
5.  **애플리케이션 역할 – 신규** 대화 상자의 **일반 페이지** 에서 **역할 이름** 상자에 새 애플리케이션 역할의 새 이름을 입력합니다.  
  
6.  **기본 스키마** 상자에 개체 이름을 입력하여 이 역할로 만든 개체를 소유할 스키마를 지정합니다. 또는 줄임표 **(…)** 를 클릭하여 **스키마 찾기** 대화 상자를 엽니다.  
  
7.  **암호** 상자에 새 역할의 암호를 입력합니다. **암호 확인** 상자에 암호를 다시 입력합니다.  
  
8.  **이 역할에서 소유한 스키마** 에서 이 역할이 소유할 스키마를 선택하거나 봅니다. 각 스키마는 한 개의 스키마 또는 역할에서만 소유할 수 있습니다.  
  
9. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

### <a name="additional-options"></a>추가 옵션  
 **애플리케이션 역할 - 신규** 대화 상자는 또한 **보안 개체** 및 **확장 속성** 의 두 추가 페이지에 옵션을 제공합니다.  
  
-   **보안 개체** 페이지에는 사용 가능한 모든 보안 개체와 이러한 보안 개체에서 로그인에 부여할 수 있는 권한이 나열됩니다.  
  
-   **확장 속성** 페이지에서는 데이터베이스 사용자에 사용자 지정 속성을 추가할 수 있습니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-an-application-role"></a>애플리케이션 역할을 만들려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    -- Creates an application role called "weekly_receipts" that has the password "987Gbv876sPYY5m23" and "Sales" as its default schema.  
  
    CREATE APPLICATION ROLE weekly_receipts   
        WITH PASSWORD = '987G^bv876sPY)Y5m23'   
        , DEFAULT_SCHEMA = Sales;  
    GO  
    ```  
  
 자세한 내용은 [CREATE APPLICATION ROLE&#40;Transact-SQL&#41;](../../../t-sql/statements/create-application-role-transact-sql.md)을 참조하세요.  
  
  
