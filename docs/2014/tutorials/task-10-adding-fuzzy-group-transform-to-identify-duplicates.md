---
title: '태스크 10: 유사 항목 그룹화 변환을 추가 하 여 중복 항목 식별 | Microsoft Docs'
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65481257"
---
# <a name="task-10-adding-fuzzy-group-transform-to-identify-duplicates"></a>태스크 10: 유사 항목 그룹화 변환을 추가하여 중복 항목 식별
  이 작업에서는 유사 항목 그룹 변환을 데이터 흐름에 추가합니다. 유사 항목 그룹 변환은 원본 데이터에서 중복 항목을 식별하는 데 도움이 될 수 있습니다. 참조 [Fuzzy Grouping Transformation](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md) 대 한 자세한 내용은 합니다.  
  
1.  끌어서 놓기 **유사 항목 그룹** 변환을 **기타 변환** 에 **SSIS 도구 상자** 하는 **데이터 흐름** 탭  **수정 및 수정 된 레코드 결합**합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **유사 항목 그룹** 에서 변환 된 **데이터 흐름** 탭을 클릭 **이름 바꾸기**합니다. 형식 **Id가 일치 하는 Group Suppliers** 누릅니다 **ENTER**합니다.  
  
3.  연결 **Combine Correct and Corrected Records** 하 **Group Suppliers with 일치 하는 Id** 파란색 커넥터를 사용 하 여 합니다.  
  
     ![Group Suppliers with 일치 하는 Id에 연결](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-01.jpg "Group Suppliers with 일치 하는 Id에 연결")  
  
4.  두 번 클릭 **일치 하는 Id와 Group Suppliers**합니다.  
  
5.  에 **유사 항목 그룹 변환 편집기**, 클릭 **새로 만들기** 옆에 **OLE DB 연결 관리자 드롭 다운 목록** 시작 **OLE DB 연결 구성 관리자** 대화 상자.  
  
6.  대화 상자에서 클릭 **새로 만들기** 시작할 **연결 관리자** 대화 상자.  
  
7.  형식 **(로컬)** 하거나 **기간** (.) 서버 이름에 대 한 합니다.  
  
8.  선택 **MDS** 에 대 한 **데이터베이스 이름 선택 또는 입력** 필드입니다. MDS 데이터베이스에 대 한 임시 저장소로 사용할지 합니다 **유사 항목 그룹 변환**합니다. 합니다 **유사 항목 그룹화** 변환 하는 변환 알고리즘이 작업을 수행 하는 데 필요한 임시 SQL Server 테이블을 만들려면 SQL Server 인스턴스에 대 한 연결이 필요 합니다. 데이터베이스를 만들거나 다른 기존 데이터베이스를 이 목적에 사용할 수 있습니다.  
  
9. 클릭 **연결 테스트** 클릭 하 여 연결 테스트 **확인** 메시지 상자에서.  
  
10. 에 **연결 관리자** 대화 상자, 클릭 **확인**합니다.  
  
11. 선택 **(local). MDS** (또는 **localhost입니다. MDS**)에서 합니다 **데이터 연결 목록** 누릅니다 **확인**합니다.  
  
12. 에 **유사 항목 그룹화 변환 편집기**에 있는지 확인 **(local). MDS** 또는 **localhost입니다. MDS** 가 선택 된 **OLE DB 연결 관리자**합니다.  
  
13. 으로 전환 합니다 **열** 탭 합니다.  
  
14. 선택 (확인란) **SupplierID_Output** 목록에서 **사용 가능한 입력 열**합니다. 변환을 구성하려면 중복 항목을 식별할 때 사용할 입력 열을 선택합니다. 간단한 설명을 위해 이 단계에서는 SupplierID만 사용합니다.  
  
     ![유사 항목 그룹화 변환 편집기](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-02.jpg "유사 항목 그룹화 변환 편집기")  
  
15. 클릭 **확인** 닫으려면 합니다 **유사 항목 그룹 변환 편집기**합니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 11: 중복 필터링 하려면 조건부 분할 변환을 추가](../../2014/tutorials/task-11-adding-conditional-split-transform-to-filter-duplicates.md)  
  
  
