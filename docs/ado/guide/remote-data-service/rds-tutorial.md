---
title: "RDS 자습서 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6cfb12781ca9e7387ea8016de581217ddf95f9c1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="rds-tutorial"></a>RDS 자습서
이 자습서에서는 RDS 프로그래밍 모델을 사용 하 여를 쿼리하고 데이터 소스를 업데이트 합니다. 먼저,이 작업을 수행 하는 데 필요한 단계에 설명 합니다. 다음 자습서는 Microsoft® Visual Basic Scripting Edition (ADO에 대 한 Windows Foundation Class (ADO/WFC) 특징으로)에서 반복 됩니다.  
  
 이 자습서는 다음 두 가지 이유로 다른 언어로 코딩 된:  
  
-   RDS에 대 한 설명서는 Visual Basic의 판독기 코드를 가정합니다. 따라서 설명서 Visual Basic 프로그래머를 위한 편리한 방법 이지만 하지 않는 다른 언어를 사용 하는 프로그래머에 대 한 합니다.  
  
-   특정 RDS 기능에 대 한 확실히 고 조금은 알고 다른 언어를 수 있습니다 다른 언어로 표현 된 동일한 기능을 검색 하 여 질문을 확인할 수 있습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="how-the-tutorial-is-presented"></a>자습서 표시 방법  
 이 자습서는 RDS 프로그래밍 모델을 기반으로 합니다. 개별적으로 프로그래밍 모델의 각 단계를 설명합니다. 각 단계의 Visual Basic 코드 조각 보여 줍니다.  
  
 최소한의 설명과 함께 다른 언어의 코드 예제에서는 반복 됩니다. 특정된 프로그래밍 언어 자습서의 각 단계는 프로그래밍 모델 및 설명이 포함 된 자습서에서의 해당 단계가 표시 됩니다. 설명이 있는 자습서의 설명을 참조 하는 단계 수를 사용 합니다.  
  
 RDS 프로그래밍 모델은 다음 섹션에서 지정 됩니다. 이 자습서를 진행할 때 안내로 사용 합니다.  
  
## <a name="rds-programming-model-with-objects"></a>RDS 프로그래밍 모델 개체와 사용  
  
-   서버에서 호출할 프로그램을 지정 하 고 클라이언트에서 참조 하는 방법 (프록시).  
  
-   서버 프로그램을 호출 합니다. 데이터 원본과를 식별 하는 서버 프로그램에 매개 변수를 전달 합니다.  
  
-   서버를 얻기는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) ADO를 사용 하 여 일반적으로 데이터 원본의 개체입니다. 필요에 따라는 **레코드 집합** 서버에서 개체를 처리 합니다.  
  
-   서버 프로그램 최종 반환 **레코드 집합** 클라이언트 응용 프로그램에는 개체입니다.  
  
-   클라이언트에서의 **레코드 집합** 개체는 필요에 따라 시각적 컨트롤에서 쉽게 사용할 수 있는 형식으로 변환 합니다.  
  
-   변경 내용에서 **레코드 집합** 개체는 서버에 다시 전송 되 고 데이터 소스를 업데이트 하는 데 사용 합니다.  
  
 이 자습서는 다음 항목을 포함합니다.  
  
-   [1단계: 서버 프로그램 지정(RDS 자습서)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [2단계: 서버 프로그램 호출(RDS 자습서)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [3단계: 서버가 레코드 집합을 가져옵니다(RDS 자습서).](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [4단계: 서버가 레코드 집합을 반환합니다(RDS 자습서).](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [5단계: DataControl을 사용 가능하도록 만듭니다(RDS 자습서).](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [6단계: 서버에 변경 내용이 보내집니다(RDS 자습서).](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>관련 항목:  
 [1 단계: 서버 프로그램 (RDS 자습서) 지정](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   

