---
title: 변경 내용을 캡처할 Oracle 테이블 선택 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- selOraTabDia
ms.assetid: 2e295dc8-999d-4c4d-96cc-1519674b47a4
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: eb73c91e7f11a0a925b808589dfac77fc4bb7374
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185032"
---
# <a name="select-oracle-tables-for-capturing-changes"></a>변경 내용을 캡처할 Oracle 테이블 선택
  이 대화 상자를 사용하여 CDC 인스턴스에 포함되는 테이블을 선택할 수 있습니다. 선택된 테이블은 새 인스턴스 마법사의 **테이블 및 열 선택** 페이지의 목록에 추가됩니다. 이 대화 상자에서 다음과 같은 작업을 수행할 수 있습니다.  
  
 기본적으로 이 대화 상자의 테이블 목록에는 테이블이 포함되어 있지 않습니다. 확인란 열의 맨 위에 있는 확인란을 선택하여 모든 테이블을 선택하거나 특정 테이블을 검색할 수 있습니다.  
  
 **특정 테이블을 검색하려면**  
 다음과 같이 검색 조건을 입력한 다음 **검색**을 클릭합니다.  
  
-   **스키마**: 목록에서 데이터베이스 스키마를 선택합니다. 해당 스키마가 있는 테이블만 목록에 포함됩니다.  
  
-   **테이블 이름 패턴**: 임의의 문자열을 입력합니다. 입력된 문자열을 포함하는 테이블만 표시됩니다.  
  
> [!NOTE]  
>  이러한 필드 중 하나 또는 모두에 조건을 입력할 수 있습니다.  
  
-   **처음 1,000개의 일치하는 테이블 표시**: 기본적으로 이 확인란은 선택되어 있습니다. 이 옵션은 처음 1000개의 일치하는 테이블로 표시를 제한합니다. 이 확인란을 선택하지 않으면 조건과 일치하는 모든 테이블이 표시됩니다. 따라서 많은 테이블이 있는 경우 목록을 표시하는 데 많은 시간이 걸릴 수 있습니다.  
  
 **CDC 인스턴스에 포함할 테이블을 선택하려면**  
 포함할 테이블 옆의 확인란을 클릭한 다음 **추가**를 클릭합니다. 테이블이 새 인스턴스 마법사의 **테이블 및 열 선택** 페이지에 있는 목록에 추가됩니다.  
  
 다른 테이블을 추가하지 않고 대화 상자를 닫으려면 **닫기** 를 클릭합니다.  
  
> [!NOTE]  
>  지원되지 않는 데이터 형식을 포함하는 테이블을 선택한 경우 오류 메시지가 표시되고 테이블은 포함되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 변경 데이터베이스 인스턴스를 만드는 방법](how-to-create-the-sql-server-change-database-instance.md)   
 [Oracle 테이블 및 열 선택](select-oracle-tables-and-columns.md)  
  
  