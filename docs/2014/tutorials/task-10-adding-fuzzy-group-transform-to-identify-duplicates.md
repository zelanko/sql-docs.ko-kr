---
title: '태스크 10: 유사 항목 그룹화 변환을 추가 하 여 중복 항목 식별 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 90b2b323-babd-464a-8914-9dc5e66aca74
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: cf9ad3dff4737d7308e7ec3434985b18015f29d8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091652"
---
# <a name="task-10-adding-fuzzy-group-transform-to-identify-duplicates"></a>태스크 10: 유사 항목 그룹화 변환을 추가하여 중복 항목 식별
  이 작업에서는 유사 항목 그룹 변환을 데이터 흐름에 추가합니다. 유사 항목 그룹 변환은 원본 데이터에서 중복 항목을 식별하는 데 도움이 될 수 있습니다. 참조 [유사 항목 그룹화 변환](http://msdn.microsoft.com/library/ms141764.aspx) 내용을 확인 합니다.  
  
1.  끌어서 놓기 **유사 항목 그룹** 변환을 **기타 변환** 에 **SSIS 도구 상자** 에 **데이터 흐름** 탭의  **수정 및 수정 된 레코드 결합**합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **유사 항목 그룹** 에서 변환 된 **데이터 흐름** 탭을 클릭 **이름 바꾸기**합니다. 형식 **Group Suppliers with 일치 하는 Id** 누릅니다 **ENTER**합니다.  
  
3.  연결 **Combine Correct and Corrected Records** 를 **Group Suppliers with 일치 하는 Id** 파란색 커넥터를 사용 하 여 합니다.  
  
     ![Group Suppliers with 일치 하는 Id에 연결](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-01.jpg "Group Suppliers with 일치 하는 Id에 연결")  
  
4.  두 번 클릭 **Group Suppliers with 일치 하는 Id**합니다.  
  
5.  에 **유사 항목 그룹 변환 편집기**, 클릭 **새로** 옆에 **OLE DB 연결 관리자 드롭 다운 목록** 를 시작 하려면 **OLE DB 연결 구성 관리자** 대화 상자.  
  
6.  대화 상자에서 클릭 **새로** 를 시작 하려면 **연결 관리자** 대화 상자.  
  
7.  형식 **(local)** 또는 **기간** (.) 서버 이름에 대 한 합니다.  
  
8.  선택 **MDS** 에 대 한 **데이터베이스 이름 선택 또는 입력** 필드입니다. MDS 데이터베이스를 사용 하 여에 대 한 임시 저장소로 됩니다는 **유사 항목 그룹 변환**합니다. **유사 항목 그룹화** 변환 하는 변환 알고리즘이 작업을 수행 하는 데 필요한 임시 SQL Server 테이블을 만드는 SQL Server의 인스턴스에 대 한 연결에 필요 합니다. 데이터베이스를 만들거나 다른 기존 데이터베이스를 이 목적에 사용할 수 있습니다.  
  
9. 클릭 **연결 테스트** 하 한 연결을 테스트 하 고 클릭 **확인** 메시지 상자에서 합니다.  
  
10. 에 **연결 관리자** 대화 상자를 클릭 **확인**합니다.  
  
11. 선택 **(local). MDS** (또는 **localhost입니다. MDS**)에서 고 **데이터 연결 목록** 클릭 **확인**합니다.  
  
12. 에 **유사 항목 그룹화 변환 편집기**, 확인 **(local). MDS** 또는 **localhost입니다. MDS** 에 대 한 선택은 **OLE DB 연결 관리자**합니다.  
  
13. 전환 하는 **열** 탭 합니다.  
  
14. 선택 (확인란) **SupplierID_Output** 목록에서 **사용 가능한 입력 열**합니다. 변환을 구성하려면 중복 항목을 식별할 때 사용할 입력 열을 선택합니다. 간단한 설명을 위해 이 단계에서는 SupplierID만 사용합니다.  
  
     ![유사 항목 그룹화 변환 편집기](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-02.jpg "유사 항목 그룹화 변환 편집기")  
  
15. 클릭 **확인** 를 닫으려면는 **유사 항목 그룹 변환 편집기**합니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 11: 조건부 분할 변환을 추가하여 중복 항목 필터링](../../2014/tutorials/task-11-adding-conditional-split-transform-to-filter-duplicates.md)  
  
  