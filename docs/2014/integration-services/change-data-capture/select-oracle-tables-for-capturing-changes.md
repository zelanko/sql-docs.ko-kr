---
title: 변경 내용을 캡처할 Oracle 테이블 선택 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- selOraTabDia
ms.assetid: 2e295dc8-999d-4c4d-96cc-1519674b47a4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c0b962db5e005837a2e9d3fe68564fceb5bfc253
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62835268"
---
# <a name="select-oracle-tables-for-capturing-changes"></a>변경 내용을 캡처할 Oracle 테이블 선택
  이 대화 상자를 사용하여 CDC 인스턴스에 포함되는 테이블을 선택할 수 있습니다. 선택된 테이블은 새 인스턴스 마법사의 **테이블 및 열 선택** 페이지의 목록에 추가됩니다. 이 대화 상자에서 다음과 같은 작업을 수행할 수 있습니다.  
  
 기본적으로 이 대화 상자의 테이블 목록에는 테이블이 포함되어 있지 않습니다. 확인란 열의 맨 위에 있는 확인란을 선택하여 모든 테이블을 선택하거나 특정 테이블을 검색할 수 있습니다.  
  
 **특정 테이블을 검색하려면**  
 다음과 같이 검색 조건을 입력한 다음 **검색**을 클릭합니다.  
  
-   **스키마**: 목록에서 데이터베이스 스키마를 선택 합니다. 해당 스키마가 있는 테이블만 목록에 포함됩니다.  
  
-   **테이블 이름 패턴**: 모든 문자열을 입력 합니다. 입력된 문자열을 포함하는 테이블만 표시됩니다.  
  
> [!NOTE]  
>  이러한 필드 중 하나 또는 모두에 조건을 입력할 수 있습니다.  
  
-   **처음 1000개의 일치하는 테이블 표시**: 이 확인란은 기본적으로 선택 됩니다. 이 옵션은 처음 1000개의 일치하는 테이블로 표시를 제한합니다. 이 확인란을 선택하지 않으면 조건과 일치하는 모든 테이블이 표시됩니다. 따라서 많은 테이블이 있는 경우 목록을 표시하는 데 많은 시간이 걸릴 수 있습니다.  
  
 **CDC 인스턴스에 포함할 테이블을 선택하려면**  
 포함할 테이블 옆의 확인란을 클릭한 다음 **추가**를 클릭합니다. 테이블이 새 인스턴스 마법사의 **테이블 및 열 선택** 페이지에 있는 목록에 추가됩니다.  
  
 다른 테이블을 추가하지 않고 대화 상자를 닫으려면 **닫기** 를 클릭합니다.  
  
> [!NOTE]  
>  지원되지 않는 데이터 형식을 포함하는 테이블을 선택한 경우 오류 메시지가 표시되고 테이블은 포함되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 변경 데이터베이스 인스턴스를 만드는 방법](how-to-create-the-sql-server-change-database-instance.md)   
 [Oracle 테이블 및 열 선택](select-oracle-tables-and-columns.md)  
  
  
