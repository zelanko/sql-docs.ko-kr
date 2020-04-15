---
title: 시각적 기본 응용 프로그램과 함께 VFP FoxPro ODBC 드라이버를 사용 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], visual basic applications
- Visual Basic applications [ODBC]
- FoxPro ODBC driver [ODBC], visual basic applications
- Visual FoxPro data [ODBC], visual basic applications
ms.assetid: 5223ca23-5df6-4ebc-aa3b-70682ff27a8c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 871c392166fa2f5726e6f9e8651bf758dc144a00
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292703"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>Visual Basic 애플리케이션과 함께 VFP FoxPro ODBC 드라이버 사용
Microsoft® Visual Basic® 응용 프로그램은 Visual FoxPro 데이터 원본에 연결하는 데이터 컨트롤을 만들어 Visual FoxPro 데이터와 통신할 수 있습니다.  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>비주얼 기본의 데이터 제어를 사용하여 시각적 FoxPro 데이터에 연결하려면  
  
1.  Visual FoxPro에 포함된 TasTrade 샘플 데이터베이스에 연결하는 "테스트"라는 데이터 원본을 만듭니다. 기본 Visual FoxPro 설치는 TasTrade 샘플 데이터베이스를 위치에 배치합니다.  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  시각적 기본에서 새 양식을 만들고 텍스트 상자와 데이터 컨트롤을 배치합니다.  
  
3.  다음과 같이 데이터 컨트롤의 Connect 속성을 변경합니다.  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  RecordsetType 속성을 다음으로 변경합니다.  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  RecordSource 속성을 다음으로 변경합니다.  
  
    ```  
    customer  
    ```  
  
6.  텍스트 상자의 DataSource 속성을 데이터 컨트롤의 기본 이름으로 다음으로 변경합니다.  
  
    ```  
    data1  
    ```  
  
7.  텍스트 상자의 DataField 속성을 다음으로 변경합니다.  
  
    ```  
    customer_id  
    ```  
  
8.  양식을 실행하고 데이터 컨트롤을 사용하여 Visual FoxPro TasTrade 샘플 데이터베이스에서 고객 ID 필드를 건너뜁니다.
