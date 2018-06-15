---
title: VFP FoxPro ODBC 드라이버를 사용 하 여 Visual Basic 응용 프로그램과 함께 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], visual basic applications
- Visual Basic applications [ODBC]
- FoxPro ODBC driver [ODBC], visual basic applications
- Visual FoxPro data [ODBC], visual basic applications
ms.assetid: 5223ca23-5df6-4ebc-aa3b-70682ff27a8c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 96107d42ae4923cd1b9f7ad1c16bd492d0203c99
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32907608"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>Visual Basic 응용 프로그램과 함께 VFP FoxPro ODBC 드라이버를 사용 하 여
Microsoft® Visual Basic® 응용 프로그램 Visual FoxPro 데이터 원본에 연결 하는 데이터 컨트롤을 만들어서 Visual FoxPro 데이터와 통신할 수 있습니다.  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>Visual Basic의 데이터 컨트롤을 사용 하 여 Visual FoxPro 데이터에 연결 하려면  
  
1.  "Test" 라는 Visual FoxPro에 포함 된 TasTrade 샘플 데이터베이스에 연결 하는 데이터 원본을 만듭니다. Visual FoxPro 기본 설치 위치에 TasTrade 예제 데이터베이스에 넣습니다.  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  Visual Basic에서 새 양식을 만드는 하 고 텍스트 상자와 데이터 컨트롤에 배치 합니다.  
  
3.  데이터 컨트롤의 연결 속성을 다음과 같이 변경 합니다.  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  다음과 RecordsetType 속성을 변경 합니다.  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  레코드 원본 속성을 다음 변경 사항:  
  
    ```  
    customer  
    ```  
  
6.  다음에 데이터 컨트롤에 대 한 기본 이름에 텍스트 상자에 대 한 데이터 원본 속성을 변경 합니다.  
  
    ```  
    data1  
    ```  
  
7.  다음에 텍스트 상자 DataField 속성을 변경 합니다.  
  
    ```  
    customer_id  
    ```  
  
8.  폼을 실행 하 고 고객 id 필드를 통해 Visual FoxPro TasTrade 예제 데이터베이스에서 건너뛸 데이터 컨트롤을 사용 합니다.
