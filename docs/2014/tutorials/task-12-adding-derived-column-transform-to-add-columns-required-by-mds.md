---
title: '태스크 12: 파생 열 변환을 MDS에 필요한 열을 추가 하려면 | Microsoft Docs'
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
ms.assetid: 98ccb271-04da-4126-9729-67e9a479aaef
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b81dd18f0ba79167a66b5cdd09c2059fcd0e0a96
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184162"
---
# <a name="task-12-adding-derived-column-transform-to-add-columns-required-by-mds"></a>태스크 12: 파생 열 변환을 추가하여 MDS에 필요한 열 추가
  이 작업에서는 파생 열 변환을 데이터 흐름에 추가합니다. 두 개의 파생된 열을 추가한 **ImportType** 및 **BatchTag**을이 변환에 전달 되는 레코드입니다. MDS의 준비 테이블에 데이터를 업로드하려면 먼저 이러한 열을 추가해야 합니다. 이러한 두 열은 MDS에서 준비 테이블의 필수 열입니다. 참조 [리프 멤버 준비 테이블](http://msdn.microsoft.com/library/ee633854.aspx) 내용을 확인 합니다.  
  
1.  끌어서 놓기 **파생 열 변환** 에서 **일반적인** 섹션은 **SSIS 도구 상자** 에 **데이터 흐름** 탭 합니다.  
  
2.  마우스 오른쪽 단추로 클릭 **파생 열** 에서 변환 된 **데이터 흐름** 탭을 클릭 **이름 바꾸기**합니다. 형식 **Add Columns Required by MDS** 누릅니다 **ENTER**합니다.  
  
3.  연결 **Filter Duplicates** 를 **Add Columns Required by MDS** 파란색 커넥터를 사용 하 여 합니다. 표시 됩니다는 **입/출력 선택** 대화 상자.  
  
4.  에 **입/출력 선택** 대화 상자에서 **고유 레코드**를 클릭 하 고 **확인**합니다.  
  
     ![출력 선택 대화 상자에 입력](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-01.jpg "출력 선택 대화 상자를 입력 합니다.")  
  
5.  클릭 **SSIS** 클릭 메뉴 모음에서 **변수**합니다.  
  
6.  에 **변수** 창 클릭 **변수 추가** 도구 모음 단추입니다.  
  
     ![SSIS 변수 창](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-02.jpg "SSIS 변수 창")  
  
7.  형식 **ImportType** 에 대 한는 **이름** 및 **2** 에 대 한는 **값**합니다. MDS의 엔터티에 새 멤버를 추가하기 때문에 값을 2로 지정합니다. 이 매개 변수에 대 한 세부 정보를 참조 하십시오. [리프 멤버 준비 테이블](http://msdn.microsoft.com/library/ee633854.aspx)합니다.  
  
8.  클릭 **변수 추가** 도구 모음 단추를 다시 합니다.  
  
9. 형식 **BatchTag** 에 대 한는 **이름**선택, **문자열** 에 대 한는 **데이터 형식**, 및 **EIMBatch** 에 대 한는 **값**합니다. **BatchTag** MDS에 제출할는 일괄 처리에 대 한는 고유 이름입니다.  
  
10. 에 **데이터 흐름** 탭을 두 번 클릭 **Add Columns Required by MDS**합니다.  
  
11. 에 **파생 열 변환 편집기** 대화 상자는 **아래쪽 창의 목록 상자에서에서**, 형식 **ImportType** 에 대 한는 **파생 열 이름**.  
  
12. 확장 **변수 및 매개 변수** 왼쪽 상단 창에서 끌어서 놓기 **User::ImportType** 에 **식** 열입니다.  
  
     ![파생 열 변환 편집기](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-03.jpg "파생 열 변환 편집기")  
  
13. 형식 **BatchTag** 에 대 한 다음 행에는 **파생 열 이름**합니다.  
  
14. 끌어서 놓기 **User::BatchTag** 에서 **변수 및 매개 변수** 에 **식** 열입니다.  
  
15. 클릭 **확인** 를 닫으려면는 **파생 열 변환** 대화 상자.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 13: OLE DB 대상을 추가하여 MDS 준비 테이블에 데이터 쓰기](../../2014/tutorials/task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table.md)  
  
  