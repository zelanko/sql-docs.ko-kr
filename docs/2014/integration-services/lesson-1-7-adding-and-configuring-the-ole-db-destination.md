---
title: '7단계: OLE DB 대상 추가 및 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 442c841d-d528-4bf0-8724-7156f909ee50
caps.latest.revision: 24
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9492f985dda337159257257c675fe37d39f162b5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184526"
---
# <a name="step-7-adding-and-configuring-the-ole-db-destination"></a>7단계: OLE DB 대상 추가 및 구성
  이제 패키지는 플랫 파일 원본에서 데이터를 추출하여 대상과 호환되는 형식으로 이 데이터를 변환할 수 있습니다. 다음 태스크에서는 변환된 데이터를 실제로 대상에 로드합니다. 데이터를 로드하려면 데이터 흐름에 OLE DB 대상을 추가해야 합니다. OLE DB 대상은 데이터베이스 테이블, 뷰 또는 SQL 명령을 사용하여 다양한 OLE DB 호환 데이터베이스에 데이터를 로드할 수 있습니다.  
  
 이 절차에서는 OLE DB 대상을 추가하고 이전에 만든 OLE DB 연결 관리자를 사용하도록 구성합니다.  
  
### <a name="to-add-and-configure-the-sample-ole-db-destination"></a>예제 OLE DB 대상을 추가하고 구성하려면  
  
1.  **SSIS 도구 상자**에서 **기타 대상**을 확장하고 **OLE DB 대상** 을 **데이터 흐름** 탭의 디자인 화면으로 끌어 놓습니다. OLE DB 대상을 **Lookup Date Key** 변환 바로 아래에 배치합니다.  
  
2.  **Lookup Date Key** 변환을 클릭하고 새로 추가한 **OLE DB 대상** 위로 녹색 화살표를 끌어 두 구성 요소를 함께 연결합니다.  
  
3.  **입/출력 선택** 대화 상자에서 **출력** 목록 상자의 **조회 일치 항목 출력**을 클릭한 다음 **확인**을 클릭합니다.  
  
4.  **데이터 흐름** 디자인 화면에서 새로 추가한 **OLE DB 대상** 구성 요소의 **OLE DB 대상** 을 클릭한 다음 이름을 **Sample OLE DB Destination**으로 변경합니다.  
  
5.  **Sample OLE DB Destination**을 두 번 클릭합니다.  
  
6.  **OLE DB 대상 편집기** 대화 상자의 **OLE DB 연결 관리자** 상자에서 **localhost.AdventureWorksDW2012** 가 선택되어 있는지 확인합니다.  
  
7.  **테이블 또는 뷰 이름** 상자에서 **[dbo].[FactCurrencyRate]** 를 입력하거나 선택합니다.  
  
8.  새 테이블을 만들려면 **새로 만들기** 단추를 클릭합니다.  스크립트에서 테이블의 이름을 변경하여 **NewFactCurrencyRate**를 읽습니다.  **확인**을 클릭합니다.  
  
9. **확인**을 클릭하면 대화 상자가 닫히고 **테이블 또는 뷰 이름** 이 **NewFactCurrencyRate**로 자동으로 변경됩니다.  
  
10. **매핑**을 클릭합니다.  
  
11. **AverageRate**, **CurrencyKey**, **EndOfDayRate**및 **DateKey** 입력 열이 대상 열에 올바르게 매핑되어 있는지 확인합니다. 서로 같은 이름의 열이 매핑되어 있는 경우 매핑이 올바른 것입니다.  
  
12. **확인**을 클릭합니다.  
  
13. **Sample OLE DB Destination** 대상을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
14. 속성 창에서 확인 하는 `LocaleID` 속성이 **영어 (미국)** 및`DefaultCodePage` 속성이로 설정 되어 **1252**합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [8단계: 1단원 패키지를 쉽게 이해할 수 있도록 만들기](lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
## <a name="see-also"></a>관련 항목  
 [OLE DB 대상](data-flow/ole-db-destination.md)  
  
  