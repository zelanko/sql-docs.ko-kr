---
title: '태스크 12: 파생 열 변환을 추가 하 여 MDS에 필요한 열 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 98ccb271-04da-4126-9729-67e9a479aaef
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 8eac057177032892ac99f557aa9d18ce497b7b2f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054292"
---
# <a name="task-12-adding-derived-column-transform-to-add-columns-required-by-mds"></a>태스크 12: 파생 열 변환을 추가하여 MDS에 필요한 열 추가
  이 작업에서는 파생 열 변환을 데이터 흐름에 추가합니다. 이 변환에 전달 된 레코드에 두 개의 파생 열 **Importtype** 및 **batchtag**를 추가 합니다. MDS의 준비 테이블에 데이터를 업로드하려면 먼저 이러한 열을 추가해야 합니다. 이러한 두 열은 MDS에서 준비 테이블의 필수 열입니다. 자세한 내용은 [리프 멤버 준비 테이블](../master-data-services/leaf-member-staging-table-master-data-services.md) 을 참조 하십시오.  
  
1.  **SSIS 도구 상자** 의 **공통** 섹션에서 **파생 열 변환을** **데이터 흐름** 탭으로 끌어서 놓습니다.  
  
2.  **데이터 흐름** 탭에서 **파생 열** 변환을 마우스 오른쪽 단추로 클릭 하 고 **이름 바꾸기**를 클릭 합니다. **MDS에 필요한 열 추가** 를 입력 하 고 **enter**키를 누릅니다.  
  
3.  **중복 필터** 를 연결 하 여 파란색 커넥터를 사용 하는 **MDS에 필요한 열을 추가** 합니다. **입력 출력 선택** 대화 상자가 표시 됩니다.  
  
4.  **입력 출력 선택** 대화 상자에서 **고유 레코드**를 선택 하 고 **확인**을 클릭 합니다.  
  
     ![입/출력 선택 대화 상자](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-01.jpg "입/출력 선택 대화 상자")  
  
5.  메뉴 모음에서 **SSIS** 를 클릭 하 고 **변수**를 클릭 합니다.  
  
6.  **변수** 창의 도구 모음에서 **변수 추가** 단추를 클릭 합니다.  
  
     ![SSIS 변수 창](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-02.jpg "SSIS 변수 창")  
  
7.  **이름** 에 **importtype** 을 입력 하 고 **값**으로 **2** 를 입력 합니다. MDS의 엔터티에 새 멤버를 추가하기 때문에 값을 2로 지정합니다. 이 매개 변수에 대 한 자세한 내용은 [리프 멤버 준비 테이블](../master-data-services/leaf-member-staging-table-master-data-services.md)을 참조 하십시오.  
  
8.  **변수 추가** 도구 모음 단추를 다시 클릭 합니다.  
  
9. **이름**에 **batchtag** 를 입력 하 고, **데이터 형식**으로 **문자열** 을 선택 하 고, **값**에 대해 **eimbatch** 를 선택 합니다. **Batchtag** 는 MDS에 제출할 일괄 처리에 대 한 고유 이름입니다.  
  
10. **데이터 흐름** 탭에서 **MDS에 필요한 열 추가**를 두 번 클릭 합니다.  
  
11. **파생 열 변환 편집기** 대화 상자의 **아래쪽 창에 있는 목록 상자**에 **파생 열 이름**에 대 한 **importtype** 을 입력 합니다.  
  
12. 왼쪽 위 창에서 **변수 및 매개 변수** 를 확장 하 고 **User:: Importtype** 을 **식** 열로 끌어 놓습니다.  
  
     ![파생 열 변환 편집기](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-03.jpg "파생 열 변환 편집기")  
  
13. 다음 행에서 **파생 열 이름**으로 **batchtag** 를 입력 합니다.  
  
14. **사용자:: BatchTag** 를 **변수 및 매개 변수** 에서 **식** 열로 끌어서 놓습니다.  
  
15. **확인** 을 클릭 하 여 **파생 열 변환** 대화 상자를 닫습니다.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 13: OLE DB 대상을 추가하여 MDS 준비 테이블에 데이터 쓰기](../../2014/tutorials/task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table.md)  
  
  
