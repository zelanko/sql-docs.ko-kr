---
title: '태스크 10: 중복 항목을 식별 하는 유사 항목 그룹 변환 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 90b2b323-babd-464a-8914-9dc5e66aca74
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 48e233c6f2c7a55bf2420825b9fb3064db6e89e1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65481257"
---
# <a name="task-10-adding-fuzzy-group-transform-to-identify-duplicates"></a>태스크 10: 유사 항목 그룹화 변환을 추가하여 중복 항목 식별
  이 작업에서는 유사 항목 그룹 변환을 데이터 흐름에 추가합니다. 유사 항목 그룹 변환은 원본 데이터에서 중복 항목을 식별하는 데 도움이 될 수 있습니다. 자세한 내용은 [유사 항목 그룹화 변환](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md) 을 참조 하세요.  
  
1.  **SSIS 도구 상자** 의 **기타 변환** 에서 **유사 항목 그룹** 변환을 **올바른 레코드와 수정 된 레코드 결합**아래의 **데이터 흐름** 탭으로 끌어서 놓습니다.  
  
2.  **데이터 흐름** 탭에서 **유사 항목 그룹** 변환을 마우스 오른쪽 단추로 클릭 하 고 **이름 바꾸기**를 클릭 합니다. **Id가 일치 하는 그룹 공급자** 를 입력 하 고 **enter**키를 누릅니다.  
  
3.  연결- **올바른 및 수정 된 레코드** 를 파란색 커넥터를 사용 하 여 **id가 일치 하는 그룹 공급자로** 결합 합니다.  
  
     ![일치하는 ID가 있는 그룹 공급자에 대한 연결](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-01.jpg "일치하는 ID가 있는 그룹 공급자에 대한 연결")  
  
4.  **Id가 일치 하는 그룹 공급자를**두 번 클릭 합니다.  
  
5.  **유사 항목 그룹 변환 편집기**에서 **OLE DB 연결 관리자 드롭다운 목록** 옆에 있는 **새로 만들기** 를 클릭 하 여 **연결 관리자 OLE DB 구성** 대화 상자를 시작 합니다.  
  
6.  대화 상자에서 **새로 만들기** 를 클릭 하 여 **연결 관리자** 대화 상자를 시작 합니다.  
  
7.  서버 이름으로 **(local)** 또는 **마침표** (.)를 입력 합니다.  
  
8.  **데이터베이스 이름 선택 또는 입력** 필드에 대해 **MDS** 를 선택 합니다. 이 경우에는 MDS 데이터베이스를 **유사 항목 그룹 변환**의 임시 저장소로 사용 합니다. **유사 항목 그룹화** 변환에서는 변환 알고리즘에서 작업을 수행 하는 데 필요한 임시 SQL Server 테이블을 만들기 위해 SQL Server 인스턴스에 연결 해야 합니다. 데이터베이스를 만들거나 다른 기존 데이터베이스를 이 목적에 사용할 수 있습니다.  
  
9. 연결 **테스트** 를 클릭 하 여 연결을 테스트 하 고 메시지 상자에서 **확인** 을 클릭 합니다.  
  
10. **연결 관리자** 대화 상자에서 **확인**을 클릭 합니다.  
  
11. **(로컬)을 선택 합니다. MDS** (또는 **localhost) MDS** **)를 클릭 하 고** **확인**을 클릭 합니다.  
  
12. **유사 항목 그룹화 변환 편집기**에서 **(local)을 확인 합니다. MDS** 또는 **localhost MDS** 는 **OLE DB 연결 관리자**에 대해 선택 됩니다.  
  
13. **열** 탭으로 전환 합니다.  
  
14. **사용 가능한 입력 열**목록에서 **SupplierID_Output** (확인란)을 선택 합니다. 변환을 구성하려면 중복 항목을 식별할 때 사용할 입력 열을 선택합니다. 간단한 설명을 위해 이 단계에서는 SupplierID만 사용합니다.  
  
     ![유사 항목 그룹화 변환 편집기](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-02.jpg "유사 항목 그룹화 변환 편집기")  
  
15. **확인** 을 클릭 하 여 **유사 항목 그룹 변환 편집기**를 닫습니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 11: 조건부 분할 변환을 추가하여 중복 항목 필터링](../../2014/tutorials/task-11-adding-conditional-split-transform-to-filter-duplicates.md)  
  
  
