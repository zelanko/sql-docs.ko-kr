---
title: 통계 수정 | Microsoft 문서
description: SQL Server Management Studio 또는 Transact-SQL을 사용하여 SQL Server에서 기존 통계를 수정하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- statistics [SQL Server], modifying
- modifying statistics
ms.assetid: b06299ca-ed52-411a-b245-45eac4628c99
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 590e5e990dc1703ed4e0c4cfefa320cfff7794be
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479164"
---
# <a name="modify-statistics"></a>통계 수정
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 기존 통계를 수정할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 통계를 수정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 다음을 만족해야 합니다.  
  
-   사용자에게 테이블이나 뷰에 대한 ALTER 권한이 있어야 합니다.  
  
-   통계를 만들려면 테이블 또는 인덱싱된 뷰의 소유자이거나 **sysadmin** 고정 서버 역할, **db_owner** 고정 데이터베이스 역할 또는 **db_ddladmin** 고정 데이터베이스 역할 중 하나의 멤버여야 합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-modify-statistics"></a>통계를 수정하려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 통계를 수정할 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 통계를 수정할 테이블을 확장합니다.  
  
4.  더하기 기호를 클릭하여 **통계** 폴더를 확장합니다.  
  
5.  수정하려는 통계 개체를 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택합니다.  
  
6.  **통계 속성 -** *statistics_name* 대화 상자의 **일반** 페이지에서 **추가**, **제거**, **위로 이동**, **아래로 이동** 을 클릭하거나 이를 조합하여 통계 속성을 변경합니다. **통계 열** 표 안에 있는 열의 위치는 통계의 유용성에 큰 영향을 미칠 수 있습니다.  
  
7.  **확인** 을 클릭합니다.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 **통계를 수정하려면**  
  
 이 작업은 Transact-SQL 문을 사용하여 수행할 수 없습니다. Transact-SQL을 사용하여 통계를 수정하려면 먼저 기존 통계를 삭제하고 새로운 특성을 사용하여 다시 만들어야 합니다.  
  
 자세한 내용은 [DROP STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md) 및 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)를 참조하세요.  
  
  
