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
ms.openlocfilehash: 541c92cd34b9cbaecdd1001be29dbab8d9b194a0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922419"
---
# <a name="rds-tutorial"></a>RDS 자습서
이 자습서에서는 RDS 프로그래밍 모델을 사용 하 여 데이터 원본을 쿼리하고 업데이트 하는 방법을 보여 줍니다. 먼저이 작업을 수행 하는 데 필요한 단계를 설명 합니다. 그런 다음 자습서는 Microsoft® Visual Basic Scripting Edition (ADO/WFC 클래스의 ADO)에서 반복 됩니다.  
  
 이 자습서는 다음 두 가지 이유로 다른 언어로 코딩 되었습니다.  
  
-   RDS 설명서는 Visual Basic에서 판독기 코드를 가정 합니다. 이렇게 하면 문서를 Visual Basic 프로그래머에 게 편리 하지만 다른 언어를 사용 하는 프로그래머에 게는 유용 하지 않습니다.  
  
-   특정 RDS 기능에 대해 잘 모르는 경우 다른 언어를 알고 있다면 다른 언어로 표시 된 것과 동일한 기능을 찾아 문제를 해결할 수 있습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="how-the-tutorial-is-presented"></a>자습서를 표시 하는 방법  
 이 자습서는 RDS 프로그래밍 모델을 기반으로 합니다. 프로그래밍 모델의 각 단계를 개별적으로 설명 합니다. 또한 Visual Basic 코드 조각으로 각 단계를 설명 합니다.  
  
 코드 예제는 최소한의 토론을 통해 다른 언어로 반복 됩니다. 지정 된 프로그래밍 언어 자습서의 각 단계는 프로그래밍 모델 및 설명 자습서의 해당 단계로 표시 됩니다. 설명 자습서의 설명을 참조 하는 단계 번호를 사용 합니다.  
  
 RDS 프로그래밍 모델은 다음 섹션에 설명 되어 있습니다. 이 자습서를 진행 하면서 로드맵으로 사용 합니다.  
  
## <a name="rds-programming-model-with-objects"></a>개체에서 RDS 프로그래밍 모델  
  
-   서버에서 호출할 프로그램을 지정 하 고 클라이언트에서 참조 하는 방식 (프록시)을 가져옵니다.  
  
-   서버 프로그램을 호출 합니다. 데이터 원본 및 실행할 명령을 식별 하는 서버 프로그램에 매개 변수를 전달 합니다.  
  
-   서버 프로그램은 일반적으로 ADO를 사용 하 여 데이터 원본에서 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 가져옵니다. 필요에 따라 **레코드 집합** 개체가 서버에서 처리 됩니다.  
  
-   서버 프로그램은 최종 **레코드 집합** 개체를 클라이언트 응용 프로그램으로 반환 합니다.  
  
-   클라이언트에서 **레코드 집합** 개체는 필요에 따라 시각적 컨트롤에서 쉽게 사용할 수 있는 폼에 배치 됩니다.  
  
-   **레코드 집합** 개체에 대 한 변경 내용은 서버로 다시 전송 되 고 데이터 원본을 업데이트 하는 데 사용 됩니다.  
  
 이 자습서에는 다음 항목이 포함 되어 있습니다.  
  
-   [1단계: 서버 프로그램 지정(RDS 자습서)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [2단계: 서버 프로그램 호출(RDS 자습서)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [3단계: 서버가 레코드 집합을 가져옵니다(RDS 자습서).](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [4단계: 서버가 레코드 집합을 반환합니다(RDS 자습서).](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [5단계: DataControl을 사용 가능하도록 만듭니다(RDS 자습서).](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [6단계: 서버에 변경 내용이 보내집니다(RDS 자습서).](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>참고 항목  
 [1 단계: 서버 프로그램 지정 (RDS 자습서)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
