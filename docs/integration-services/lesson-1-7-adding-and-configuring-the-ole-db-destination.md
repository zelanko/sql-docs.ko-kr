---
title: '7단계: OLE DB 대상 추가 및 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 442c841d-d528-4bf0-8724-7156f909ee50
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c72ac0393733511f63844ae50b20a40e4c12ea4a
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917346"
---
# <a name="lesson-1-7-add-and-configure-the-ole-db-destination"></a>1-7단원: OLE DB 대상 추가 및 구성

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



이제 패키지는 플랫 파일 원본에서 데이터를 추출하여 해당 데이터를 대상과 호환되는 형식으로 변환할 수 있습니다. 다음 작업은 변환된 데이터를 대상에 로드하는 것입니다. 데이터를 로드하려면 데이터 흐름에 OLE DB 대상을 추가합니다. OLE DB 대상은 데이터베이스 테이블, 보기 또는 SQL 명령을 사용하여 다양한 OLE DB 호환 데이터베이스에 데이터를 로드할 수 있습니다.  
  
이 태스크에서는 OLE DB 대상을 추가하고 이전에 만든 OLE DB 연결 관리자를 사용하도록 구성합니다.  
  
## <a name="add-and-configure-the-sample-ole-db-destination"></a>샘플 OLE DB 대상 추가 및 구성  
  
1.  **SSIS 도구 상자**에서 **기타 대상**을 확장하고 **OLE DB 대상** 을 **데이터 흐름** 탭의 디자인 화면으로 끌어 놓습니다. **OLE DB 대상**을 **Lookup Date Key** 변환 바로 아래에 배치합니다.  
  
2.  **Lookup Date Key** 변환을 선택하고 새 **OLE DB 대상** 위로 파란색 화살표를 끌어다 놓아서 두 구성 요소를 함께 연결합니다.  
  
3.  **입/출력 선택** 대화 상자의 **출력** 목록 상자에서 **조회 일치 항목 출력**을 선택한 다음, **확인**을 선택합니다.  
  
4.  **데이터 흐름** 디자인 화면에서 새 **OLE DB 대상** 구성 요소의 이름 **OLE DB 대상**을 선택하고 해당 이름을 **Sample OLE DB Destination**으로 변경합니다.  
  
5.  **Sample OLE DB Destination**을 두 번 클릭합니다.  
  
6.  **OLE DB 대상 편집기** 대화 상자의 **OLE DB 연결 관리자** 상자에서 **localhost.AdventureWorksDW2012**가 선택되어 있는지 확인합니다.  
  
7.  **테이블 또는 보기 이름** 상자에서 **[dbo].[FactCurrencyRate]** 를 입력하거나 선택합니다.  
  
8.  새 테이블을 만들려면 **새로 만들기** 단추를 선택합니다.  스크립트의 테이블의 이름을 **Sample OLE DB Destination**에서 **NewFactCurrencyRate**로 변경합니다.  **확인**을 선택합니다.  
  
9. **확인**을 선택하면 대화 상자가 닫히고 **테이블 또는 보기 이름**이 **NewFactCurrencyRate**로 자동으로 변경됩니다.  
  
10. **매핑**을 선택합니다.  
  
11. **AverageRate**, **CurrencyKey**, **EndOfDayRate**및 **DateKey** 입력 열이 대상 열에 올바르게 매핑되어 있는지 확인합니다. 서로 같은 이름의 열이 매핑되어 있는 경우 매핑이 올바른 것입니다.  
  
12. **확인**을 선택합니다.  
  
13. **Sample OLE DB Destination** 대상을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
14. **속성** 창에서 **LocaleID** 속성이 **영어(미국)** 로 설정되어 있고 **DefaultCodePage** 속성이 **1252**로 설정되어 있는지 확인합니다.  
  
## <a name="go-to-next-task"></a>다음 작업으로 이동
[8단계: 1단원 패키지 주석 달기 및 형식](../integration-services/lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
## <a name="see-also"></a>참고 항목  
[OLE DB 대상](../integration-services/data-flow/ole-db-destination.md)  
  
  
  
