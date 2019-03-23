---
title: CDC 인스턴스에 테이블 추가 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- addTabs
ms.assetid: ad260e19-c021-4035-9311-c02fc96ceaea
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 546f001ac4809a4fb8c455e37bf10f975d84dce8
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388271"
---
# <a name="add-tables-to-a-cdc-instance"></a>CDC 인스턴스에 테이블 추가
  테이블 선택 대화 상자를 사용하여 Oracle 원본에서 CDC 인스턴스로 다른 테이블을 추가할 수 있습니다. 선택한 테이블이 속성 편집기의 **테이블** 탭에 있는 목록에 추가됩니다.  
  
 기본적으로 이 대화 상자의 테이블 목록에는 테이블이 포함되어 있지 않습니다. **(모두 선택)** 확인란을 선택하거나 특정 테이블을 검색할 수 있습니다.  
  
 **특정 테이블을 검색하려면**  
 다음과 같이 검색 조건을 입력한 다음 **검색**을 클릭합니다.  
  
-   **스키마**: 목록에서 데이터베이스 스키마를 선택합니다. 해당 스키마가 있는 테이블만 목록에 포함됩니다.  
  
-   **테이블 이름 패턴**: 임의의 문자열을 입력합니다. 입력된 문자열을 포함하는 테이블만 표시됩니다.  
  
> [!NOTE]  
>  이러한 필드 중 하나 또는 모두에 조건을 입력할 수 있습니다.  
  
-   **표시할 처음 1,000 개의 일치 하는 테이블**: 기본적으로 이 확인란은 선택되어 있습니다. 이 옵션은 처음 1000개의 일치하는 테이블로 표시를 제한합니다. 이 확인란을 선택하지 않으면 조건과 일치하는 모든 테이블이 표시됩니다. 따라서 많은 테이블이 있는 경우 목록을 표시하는 데 많은 시간이 걸릴 수 있습니다.  
  
 **CDC 인스턴스에 포함할 테이블을 선택하려면**  
 포함할 테이블 옆의 확인란을 클릭한 다음 **추가**를 클릭합니다. 테이블이 새 인스턴스 마법사의 **테이블 및 열 선택** 페이지에 있는 목록에 추가됩니다.  
  
 테이블을 추가하지 않고 대화 상자를 닫으려면 **닫기** 를 클릭합니다.  
  
> [!NOTE]  
>  지원되지 않는 데이터 형식을 포함하는 테이블을 선택한 경우 오류 메시지가 표시되고 테이블은 포함되지 않습니다.  
  
> [!NOTE]  
>  뷰어에서 테이블 목록을 볼 수 있습니다. 뷰어를 사용할 때 정보는 읽기 전용입니다. 또한 뷰어에는 테이블에서 캡처된 열 목록이 포함되어 있습니다. 뷰어에 액세스하는 방법은 [How to Manage a CDC Instance](manage-a-cdc-instance.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [CDC 인스턴스 속성을 편집하는 방법](how-to-edit-the-cdc-instance-properties.md)   
 [How to Manage a CDC Instance](manage-a-cdc-instance.md)   
 [변경 내용을 캡처할 Oracle 테이블 선택](select-oracle-tables-for-capturing-changes.md)  
  
  
