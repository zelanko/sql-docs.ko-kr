---
title: '태스크 13: MDS 준비 테이블에 데이터를 쓸 OLE DB 대상 추가 | Microsoft Docs'
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
ms.topic: conceptual
ms.assetid: e6c67fa9-bb52-44a9-82f6-d86551cf12b2
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dc0bd3ad05ec740299e0cb06def5a439fa87da9c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37234283"
---
# <a name="task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table"></a>태스크 13: OLE DB 대상을 추가하여 MDS 준비 테이블에 데이터 쓰기
  추가한 했으므로 **ImportType** 하 고 **BatchTag** 로 전송할 수 MDS 준비에 대 한 준비가 됩니다 모든 레코드 값입니다. 이 작업을 사용 하 여 OLE DB 대상 데이터를 쓸 **stg.supplier_Leaf** 준비 테이블입니다.  
  
1.  끌어서 **OLE DB Destination** 에서 **기타 대상** 섹션의 **SSIS 도구 상자** 에 **데이터 흐름** 탭 놓습니다  **Required by MDS 열 추가**합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **OLE DB Destination** 에 **데이터 흐름** 탭을 클릭 **이름 바꾸기**합니다. 형식 **MDS 준비 테이블에 공급자 데이터 쓰기** 누릅니다 **ENTER**합니다.  
  
3.  연결 된 **Add Columns Required by MDS** 하 **MDS 준비 테이블에 공급자 데이터 쓰기** 파란색 커넥터를 사용 하 여 합니다.  
  
4.  두 번 클릭 **MDS 준비 테이블에 공급자 데이터 쓰기** 에 **데이터 흐름** 탭 합니다.  
  
5.  에 **OLE DB 대상 편집기** 대화 상자에서 확인 **(local). MDS** (또는 **localhost입니다. MDS**)가 선택 된 **OLE DB 연결 관리자** 필드입니다.  
  
6.  선택 **의 Supplier_Leaf** 목록에서 테이블 **테이블 또는 뷰 이름**합니다.  
  
     ![OLEDB 대상 편집기](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-01.jpg "OLEDB 대상 편집기")  
  
7.  전환할 합니다 **매핑을** 를 클릭 하 여 페이지 **매핑** 왼쪽 메뉴에서.  
  
8.  지도 **입력** 하 고 **대상** 다음 표에 나와 있는 것 처럼 열입니다.  
  
     ![OLEDB 대상 편집기-매핑](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-02.jpg "OLEDB 대상 편집기-매핑")  
  
9. 사용 하 고 있는지 확인 **(_o)** 입력 열에 대 한 열 하지는 **_source** 하거나 **_output** 열. **(_O)** 열 DQS 정리의 출력 값을 포함 합니다.  
  
10. 클릭 **확인** 닫으려면 합니다 **OLE DB 대상 편집기** 대화 상자.  
  
11. 데이터 흐름은 다음 이미지와 같습니다.  
  
     ![데이터 흐름을 완료](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-03.jpg "데이터 흐름 완료")  
  
## <a name="next-step"></a>다음 단계  
 [태스크 14: 제어 흐름에 SQL 실행 태스크를 추가하여 MDS에 대한 저장 프로시저 실행](../../2014/tutorials/task-14-add-execute-to-control-flow-run-mds-stored-procedure.md)  
  
  
