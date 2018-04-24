---
title: '5 단계: DataControl 유용 수행 (RDS 자습서) | Microsoft Docs'
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], datacontrol made usable
ms.assetid: ed5c4a24-9804-4c85-817e-317652acb9b4
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6c152323f13f8f21cef1485f81a81f5a01dcde71
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="step-5-datacontrol-is-made-usable-rds-tutorial"></a>5 단계: DataControl 유용 수행 (RDS 자습서)
반환 된 **레코드 집합** 개체를 사용 하기 위해 사용할 수 있습니다. 검사, 탐색, 또는 다른 대로 편집할 **레코드 집합**합니다. 으로 수행할 수 있는 **레코드 집합** 사용자 환경에 따라 달라 집니다. Visual Basic 및 Visual c + +를 사용할 수 있는 시각적 컨트롤을 포함 한 **레코드 집합** 직접 또는 간접적으로 제어 데이터를 설정 하는 사용 하 여 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 예를 들어 Microsoft Internet Explorer에서 웹 페이지를 표시 하는 경우 수 표시 하려는 **레코드 집합** 시각적 컨트롤에 데이터 개체입니다. 시각적 컨트롤이 웹 페이지에 액세스할 수 없는 **레코드 집합** 개체를 직접 합니다. 그러나 액세스할 수는 **레코드 집합** 개체를 통해는 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)합니다. **.rds입니다 DataControl** 시각적 개체에서 사용할 수 있게 시점을 제어할 해당 [SourceRecordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) 속성이로 설정 되는 **레코드 집합** 개체입니다.  
  
 시각적 컨트롤 개체 있어야 해당 **DATASRC** 로 설정 된 매개 변수는 **.rds입니다 DataControl**, 및 해당 **DATAFLD** 속성이로 설정 된 **레코드 집합** 개체 필드 (열)입니다.  
  
 이 자습서에서 설정 된 **SourceRecordset** 속성:  
  
```  
Sub RDSTutorial5()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DC as New RDS.DataControl  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "http://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
   DC.SourceRecordset = RS         ' Visual controls can now bind to DC.  
...  
```  
  
## <a name="see-also"></a>관련 항목:  
 [(RDS 자습서) 서버에 변경 내용이 보내집니다 6 단계:](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)   
 [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
