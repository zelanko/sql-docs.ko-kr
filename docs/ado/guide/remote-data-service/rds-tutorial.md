---
title: RDS 자습서 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c9136f1fc1fdf7538744501984af50e2ca52f04
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62929882"
---
# <a name="rds-tutorial"></a>RDS 자습서
이 자습서에서는 쿼리 및 데이터 원본을 업데이트 하려면 RDS 프로그래밍 모델을 사용 하 여 보여 줍니다. 먼저,이 작업을 수행 하는 데 필요한 단계에 설명 합니다. 다음 자습서는 Microsoft® Visual Basic Scripting Edition (ADO에 대 한 Windows Foundation Class (ADO/WFC) 포함)에서 반복 됩니다.  
  
 이 자습서는 두 가지 이유로 여러 언어로 코딩은:  
  
-   RDS에 대 한 설명서는 Visual Basic 코드를 판독기를 가정합니다. 따라서 설명서 Visual Basic 프로그래머를 위한 편리 하지만 덜 유용한 다른 언어를 사용 하는 프로그래머에 대 한 합니다.  
  
-   특정 RDS 기능에 대 한 확실 하지 않은 경우와 약간 알고 다른 언어를 수 있습니다 다른 언어로 표현 된 동일한 기능에 대 한 확인 하 여 질문을 해결 하려면.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="how-the-tutorial-is-presented"></a>자습서 표시 하는 방법  
 이 자습서는 RDS 프로그래밍 모델을 기반으로 합니다. 개별적으로 프로그래밍 모델의 각 단계를 설명합니다. 또한 Visual Basic 코드 조각 사용 하 여 각 단계를 설명합니다.  
  
 코드 예제에서는 최소한의 설명과 함께 다른 언어에서 반복 됩니다. 지정 된 프로그래밍 언어 자습서의 각 단계는 프로그래밍 모델 및 설명이 포함 된 자습서에서 해당 단계를 사용 하 여 표시 됩니다. 단계 번호를 사용 하 여 설명이 포함 된 자습서의 설명을 참조 하세요.  
  
 RDS 프로그래밍 모델은 다음 섹션에서 지정 됩니다. 이 자습서를 진행할 때 로드맵을으로 사용 합니다.  
  
## <a name="rds-programming-model-with-objects"></a>개체에서 RDS 프로그래밍 모델  
  
-   서버에서 호출 프로그램을 지정 하 고 클라이언트에서 참조 하는 방법 (프록시).  
  
-   서버 프로그램을 호출 합니다. 데이터 원본 및 실행 하는 명령을 식별 하는 서버 프로그램에 매개 변수를 전달 합니다.  
  
-   서버를 얻기를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) ADO를 사용 하 여 일반적으로 데이터 원본의 개체입니다. 필요에 따라 합니다 **레코드 집합** 서버의 개체를 처리 합니다.  
  
-   서버 프로그램 반환 최종 **레코드 집합** 클라이언트 응용 프로그램 개체입니다.  
  
-   클라이언트에서의 **레코드 집합** 개체는 필요에 따라 시각적 컨트롤에서 쉽게 사용할 수 있는 형식으로 변환 됩니다.  
  
-   변경 된 **레코드 집합** 개체 서버에 다시 전송 되 고 데이터 소스를 업데이트 하는 데 사용 합니다.  
  
 이 자습서는 다음 항목을 포함합니다.  
  
-   [1단계: (RDS 자습서) 서버 프로그램 지정](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [2단계: (RDS 자습서) 서버 프로그램 호출](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [3단계: 서버 (RDS 자습서) 레코드 집합을 가져옵니다.](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [4단계: 서버 (RDS 자습서) 레코드 집합을 반환합니다.](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [5단계: DataControl 유용 수행 (RDS 자습서)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [6단계: 변경 내용 (RDS 자습서) 서버로 보내집니다.](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>관련 항목  
 [1단계: (RDS 자습서) 서버 프로그램 지정](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
