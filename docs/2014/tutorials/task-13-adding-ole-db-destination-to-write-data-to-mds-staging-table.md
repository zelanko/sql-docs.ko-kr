---
title: '태스크 13: OLE DB 대상을 추가 하 여 MDS 준비 테이블에 데이터를 쓸 | Microsoft Docs'
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
ms.assetid: e6c67fa9-bb52-44a9-82f6-d86551cf12b2
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 75e77579857852e607b783534d149367a946318f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082583"
---
# <a name="task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table"></a>태스크 13: OLE DB 대상을 추가하여 MDS 준비 테이블에 데이터 쓰기
  이제를 추가한 후 **ImportType** 및 **BatchTag** 를 보내기 위해 통해 MDS 준비에 대 한 준비가 모든 레코드에 사용 되는 값입니다. 이 태스크를 사용 하 여 OLE DB 대상 데이터를 쓸 **stg.supplier_Leaf** 준비 테이블입니다.  
  
1.  끌어서 **OLE DB Destination** 에서 **기타 대상** 섹션은 **SSIS 도구 상자** 에 **데이터 흐름** 탭 놓습니다  **MDS에 필요한 열 추가**합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **OLE DB Destination** 에 **데이터 흐름** 탭을 클릭 **이름 바꾸기**합니다. 형식 **MDS 준비 테이블에 공급자 데이터 쓰기** 누릅니다 **ENTER**합니다.  
  
3.  연결 된 **Add Columns Required by MDS** 를 **MDS 준비 테이블에 공급자 데이터 쓰기** 파란색 커넥터를 사용 하 여 합니다.  
  
4.  두 번 클릭 **MDS 준비 테이블에 공급자 데이터 쓰기** 에 **데이터 흐름** 탭 합니다.  
  
5.  에 **OLE DB 대상 편집기** 대화 상자에서 다음 사항을 확인 **(local). MDS** (또는 **localhost입니다. MDS**)에 대 한 선택은 **OLE DB 연결 관리자** 필드입니다.  
  
6.  선택 **의 경우 Supplier_Leaf** 목록에서 테이블 **테이블 또는 뷰 이름**합니다.  
  
     ![OLEDB 대상 편집기](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-01.jpg "OLEDB 대상 편집기")  
  
7.  전환 하는 **매핑** 페이지를 클릭 하 여 **매핑** 왼쪽 메뉴에서.  
  
8.  지도 **입력** 및 **대상** 다음 표에 나와 있는 것 처럼 열입니다.  
  
     ![OLEDB 대상 편집기-매핑](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-02.jpg "OLEDB 대상 편집기-매핑")  
  
9. 사용 하 고 있는지 확인 **_Output** 입력 열에 대 한 열 하지는 **_source** 또는 **_output** 열입니다. **_Output** 열 DQS 정리 출력 값이 포함 됩니다.  
  
10. 클릭 **확인** 를 닫으려면는 **OLE DB 대상 편집기** 대화 상자.  
  
11. 데이터 흐름은 다음 이미지와 같습니다.  
  
     ![데이터 흐름을 완료](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-03.jpg "데이터 흐름 완료")  
  
## <a name="next-step"></a>다음 단계  
 [태스크 14: 제어 흐름에 SQL 실행 태스크를 추가하여 MDS에 대한 저장 프로시저 실행](../../2014/tutorials/task-14-add-execute-to-control-flow-run-mds-stored-procedure.md)  
  
  