---
title: Visual Basic 응용 프로그램과 함께 VFP FoxPro ODBC 드라이버 사용 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 017e8e7897b2b792d7a864dc336537d76dcad8b9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087984"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>Visual Basic 애플리케이션과 함께 VFP FoxPro ODBC 드라이버 사용
Microsoft® Visual Basic® 응용 프로그램은 Visual FoxPro 데이터 원본에 연결 하는 데이터 컨트롤을 만들어 Visual FoxPro 데이터와 통신할 수 있습니다.  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>Visual Basic에서 데이터 컨트롤을 사용 하 여 Visual FoxPro 데이터에 연결 하려면  
  
1.  Visual FoxPro에 포함 된 TasTrade 예제 데이터베이스에 연결 하는 "test" 라는 데이터 원본을 만듭니다. 기본 Visual FoxPro 설치는 다음 위치에 TasTrade 샘플 데이터베이스를 배치 합니다.  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  Visual Basic에서 새 양식을 만들고 텍스트 상자와 데이터 컨트롤을 추가 합니다.  
  
3.  데이터 컨트롤의 Connect 속성을 다음과 같이 변경 합니다.  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  RecordsetType 속성을 다음과 같이 변경 합니다.  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  RecordSource 속성을 다음과 같이 변경 합니다.  
  
    ```  
    customer  
    ```  
  
6.  텍스트 상자의 DataSource 속성을 데이터 컨트롤의 기본 이름으로 다음과 같이 변경 합니다.  
  
    ```  
    data1  
    ```  
  
7.  텍스트 상자의 DataField 속성을 다음과 같이 변경 합니다.  
  
    ```  
    customer_id  
    ```  
  
8.  폼을 실행 하 고 데이터 컨트롤을 사용 하 여 Visual FoxPro TasTrade 예제 데이터베이스에서 고객 id 필드를 건너뜁니다.
