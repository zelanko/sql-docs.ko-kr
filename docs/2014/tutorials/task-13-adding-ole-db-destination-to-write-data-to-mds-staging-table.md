---
title: '작업 13: MDS 준비 테이블에 데이터를 쓸 OLE DB 대상 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e6c67fa9-bb52-44a9-82f6-d86551cf12b2
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bb39e9d50d135adfedcf307cda2ad703e302eda5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061141"
---
# <a name="task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table"></a>태스크 13: OLE DB 대상을 추가하여 MDS 준비 테이블에 데이터 쓰기
  이제 모든 레코드에 **Importtype** 및 **batchtag** 값을 추가 했으므로 준비를 위해 MDS로 전송할 준비가 되었습니다. 이 태스크에서는 OLE DB 대상을 사용 하 여 데이터를 **stg. supplier_Leaf** 준비 테이블에 기록 합니다.  
  
1.  **SSIS 도구 상자** 의 **다른 대상** 섹션에서 **데이터 흐름** 탭으로 **OLE DB Destination** 을 끌어서 **MDS에 필요한 열 추가**아래에 놓습니다.  
  
2.  **데이터 흐름** 탭에서 **대상 OLE DB** 를 마우스 오른쪽 단추로 클릭 하 고 **이름 바꾸기**를 클릭 합니다. **MDS 준비 테이블에 공급자 데이터 쓰기를** 입력 하 고 **enter**키를 누릅니다.  
  
3.  파란색 커넥터를 사용 하 여 mds **준비 테이블에 공급자 데이터를 기록** 하는 **데 필요한 추가 열을 mds** 에 연결 합니다.  
  
4.  **데이터 흐름** 탭에서 **MDS 준비 테이블에 공급자 데이터 쓰기를** 두 번 클릭 합니다.  
  
5.  **OLE DB 대상 편집기** 대화 상자에서 **(로컬)이 있는지 확인 합니다. MDS** (또는 **localhost) MDS**) **OLE DB 연결 관리자** 필드에 대해 선택 됩니다.  
  
6.  **Stg를 선택 합니다. ** **테이블 또는 뷰의 이름**목록에서 테이블을 Supplier_Leaf 합니다.  
  
     ![OLEDB 대상 편집기](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-01.jpg "OLEDB 대상 편집기")  
  
7.  왼쪽의 메뉴에서 **매핑** 을 클릭 하 여 **매핑** 페이지로 전환 합니다.  
  
8.  다음 표와 같이 **입력** 및 **대상** 열을 매핑합니다.  
  
     ![OLEDB 대상 편집기 - 매핑](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-02.jpg "OLEDB 대상 편집기 - 매핑")  
  
9. **_Status** 또는 **_Source** 열이 아닌 입력 열에 **_Output** 열을 사용 하 고 있는지 확인 합니다. **_Output** 열에는 dqs 정리의 출력 값이 포함 됩니다.  
  
10. **확인** 을 클릭 하 여 **대상 편집기 OLE DB** 대화 상자를 닫습니다.  
  
11. 데이터 흐름은 다음 이미지와 같습니다.  
  
     ![완료된 데이터 흐름](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-03.jpg "완료된 데이터 흐름")  
  
## <a name="next-step"></a>다음 단계  
 [태스크 14: Control Flow에 SQL 실행 태스크를 추가하여 MDS에 대한 저장 프로시저 실행](../../2014/tutorials/task-14-add-execute-to-control-flow-run-mds-stored-procedure.md)  
  
  
