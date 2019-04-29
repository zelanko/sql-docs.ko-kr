---
title: '5단계: DataControl 유용 수행 (RDS 자습서) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], datacontrol made usable
ms.assetid: ed5c4a24-9804-4c85-817e-317652acb9b4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01b7a1b7829ace46cac7be21d33d9837845db9a7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955773"
---
# <a name="step-5-datacontrol-is-made-usable-rds-tutorial"></a>5단계: DataControl을 사용 가능하도록 만듭니다(RDS 자습서).
반환 된 **레코드 집합** 개체는 사용할 수 있습니다. 검사, 탐색 하거나 다른 대로 편집할 수 있습니다 **레코드 집합**합니다. 사용 하 여 수행할 수 있는 작업은 **레코드 집합** 사용자 환경에 따라 달라 집니다. Visual Basic 및 Visual C++ 에서 사용할 수 있는 시각적 컨트롤을 **레코드 집합** 직접 또는 간접적으로 사용 하도록 설정 하면 데이터 컨트롤을 사용 하 여 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 예를 들어 Microsoft Internet Explorer에서 웹 페이지를 표시 하는 경우 하려는 표시 합니다 **레코드 집합** 시각적 컨트롤에 데이터 개체입니다. 시각적 컨트롤이 웹 페이지에 액세스할 수 없습니다는 **레코드 집합** 직접 개체입니다. 그러나 액세스할 수 있습니다 합니다 **Recordset** 개체를 통해를 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)합니다. **rds. DataControl** 시각적 개체에서 사용할 수 있게 됩니다 제어 하는 경우 해당 [SourceRecordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) 속성을 **레코드 집합** 개체.  
  
 시각적 컨트롤 개체가 있어야 해당 **DATASRC** 로 설정 된 매개 변수는 **rds. DataControl**, 및 해당 **DATAFLD** 로 설정 된 속성을 **레코드 집합** 개체 필드 (열).  
  
 이 자습서에서는 설정 된 **SourceRecordset** 속성:  
  
```vb
Sub RDSTutorial5()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DC as New RDS.DataControl  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
   DC.SourceRecordset = RS         ' Visual controls can now bind to DC.  
...  
```  
  
## <a name="see-also"></a>관련 항목  
 [6단계: 변경 내용 (RDS 자습서) 서버로 보내집니다.](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)   
 [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
