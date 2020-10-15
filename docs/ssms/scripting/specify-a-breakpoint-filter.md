---
title: 중단점 필터 지정
description: 지정된 컴퓨터, 운영 체제 프로세스 및 스레드에 디버깅이 설정된 경우에만 중단점이 작동하도록 중단점을 제한하는 중단점 필터를 구현하는 방법을 알아봅니다.
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoint filter
ms.assetid: 7bf1dddd-7b0b-4c47-8a7b-28a5569b4fa5
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 307e262c57409725014a202b4a48143b5228763e
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036308"
---
# <a name="specify-a-breakpoint-filter"></a>중단점 필터 지정

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

중단점 필터는 중단점이 지정된 컴퓨터, 운영 체제 프로세스 및 스레드에서만 작동하도록 제한합니다. 중단점 필터는 일반적으로 병렬 애플리케이션을 디버깅할 때 사용됩니다.

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]
  
##  <a name="filter-considerations"></a><a name="BKMK_ActionConsiderations"></a> 필터 고려 사항

중단점 필터는 일반적으로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거에서는 사용되지 않는데 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 및 저장 프로시저는 병렬 애플리케이션이 아니기 때문입니다.  
  
#### <a name="to-specify-a-breakpoint-filter"></a>중단점 필터를 지정하려면  
  
1.  편집기 창에서 중단점 문자 모양을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **필터** 를 클릭합니다.  
  
     또는  
  
     **중단점** 창에서 중단점 문자 모양을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **필터** 를 클릭합니다.  
  
2.  **중단점 필터** 대화 상자의 **필터** 상자에 컴퓨터 이름을 지정하거나 운영 체제 프로세스 및 스레드를 이름이나 ID 번호로 지정합니다.  
  
    -   **MachineName** 은 데이터베이스 엔진 인스턴스를 실행 중인 컴퓨터입니다.  
  
    -   **ProcessID**및 **ProcessName** 은 데이터베이스 엔진 인스턴스를 실행 중인 운영 체제 프로세스입니다.  
  
    -   **ThreadID** 및 **ThreadName** 은 데이터베이스 엔진 인스턴스에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리, 프로시저 또는 함수를 실행 중인 운영 체제 스레드입니다.  
  
3.  **확인** 을 클릭하여 변경 내용을 구현하거나 **취소** 를 클릭하여 변경 내용을 적용하지 않고 종료합니다.  
  
## <a name="see-also"></a>참고 항목  
 [중단점 조건 지정](./specify-a-breakpoint-condition.md)   
 [적중 횟수 지정](./specify-a-hit-count.md)   
 [중단점 동작 지정](./specify-a-breakpoint-action.md)