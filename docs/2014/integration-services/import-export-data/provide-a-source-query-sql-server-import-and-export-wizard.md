---
title: 원본 쿼리 지정(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.providesourcequery.f1
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7a028c880d87e21e1fcc63ffc605e7d375619dbf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767865"
---
# <a name="provide-a-source-query-sql-server-import-and-export-wizard"></a>원본 쿼리 지정(SQL Server 가져오기 및 내보내기 마법사)
  **원본 쿼리 지정** 페이지를 사용하여 데이터 원본에서 대상으로 복사할 데이터를 생성하는 SQL 문을 입력할 수 있습니다.  
  
 이 마법사에 대 한 자세한 내용은 참조 하세요 [SQL Server 가져오기 및 내보내기 마법사](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)합니다. 마법사를 성공적으로 실행 하는 데 필요한 사용 권한 뿐만 아니라 마법사 시작 옵션을 알아보려면 [SQL Server 가져오기 및 내보내기 마법사를 실행](start-the-sql-server-import-and-export-wizard.md)합니다.  
  
 SQL Server 가져오기 및 내보내기 마법사의 목적은 원본에서 대상으로 데이터를 복사하는 것입니다. 이 마법사는 대상 데이터베이스 및 대상 테이블도 만들 수 있습니다. 그러나 여러 개의 데이터베이스 또는 테이블을 복사하거나 다른 종류의 데이터베이스 개체를 복사할 경우 대신 데이터베이스 복사 마법사를 사용해야 합니다. 자세한 내용은 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **SQL 문**  
 원본 데이터베이스의 데이터에서 선택한 행을 검색할 쿼리 문을 입력합니다. 예를 들어 다음 쿼리 문은 AdventureWorks 데이터베이스에서 커미션 비율이 1.5% 이상인 영업 사원에 대한 **SalesPersonID**, **SalesQuota**및 **SalesYTD** 를 검색합니다.  
  
```  
SELECT SalesPersonID, SalesQuota, SalesYTD  
FROM Sales.SalesPerson  
WHERE CommissionPct > 0.015  
```  
  
 **구문 분석**  
 **SQL 문** 입력란에 입력된 SQL 문의 구문을 검사합니다.  
  
> [!NOTE]  
>  이 문의 구문을 검사하는 데 필요한 시간이 제한 시간 값인 30초를 초과하면 구문 분석이 중지되고 오류가 발생합니다. 구문 분석이 성공할 때까지는 이 마법사 페이지를 지나서 이동할 수 없습니다. 한 가지 해결 방법은 쿼리를 기반으로 하는 데이터베이스 뷰를 만든 다음 쿼리 텍스트를 직접 입력하는 대신 마법사에서 이 뷰를 쿼리하는 것입니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 SQL 문이 포함된 파일을 선택합니다. 파일을 선택하면 해당 파일의 텍스트가 **쿼리 문** 의 입력란으로 복사됩니다.  
  
  
