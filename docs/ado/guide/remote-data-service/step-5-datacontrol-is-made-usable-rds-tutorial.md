---
description: '5단계: DataControl을 사용 가능하도록 만듭니다(RDS 자습서).'
title: '5 단계: DataControl 사용 가능 (RDS 자습서) | Microsoft Docs'
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 18365d26c9b46fb651d68291dc5fa026f23e3bfb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451915"
---
# <a name="step-5-datacontrol-is-made-usable-rds-tutorial"></a>5단계: DataControl을 사용 가능하도록 만듭니다(RDS 자습서).
반환 된 **레코드 집합** 개체를 사용할 수 있습니다. 다른 **레코드 집합과**마찬가지로이를 검사 하거나 탐색 하거나 편집할 수 있습니다. **레코드 집합** 으로 수행할 수 있는 작업은 환경에 따라 달라 집니다. Visual Basic 및 Visual C++에는 데이터 컨트롤을 사용 하 여 직접 또는 간접적으로 **레코드 집합** 을 사용할 수 있는 시각적 컨트롤이 있습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 예를 들어 Microsoft Internet Explorer에서 웹 페이지를 표시 하는 경우에는 시각적 컨트롤에 **레코드 집합** 개체 데이터를 표시 하는 것이 좋습니다. 웹 페이지의 시각적 컨트롤은 **레코드 집합** 개체에 직접 액세스할 수 없습니다. 그러나 이러한 사용자는 RDS를 통해 **레코드 집합** 개체에 액세스할 수 있습니다 [. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md). **RDS. ** [SourceRecordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) 속성이 **레코드 집합** 개체로 설정 된 경우에는 시각적 컨트롤에서 DataControl을 사용할 수 있습니다.  
  
 시각적 컨트롤 개체의 **DATASRC** 매개 변수는 RDS로 설정 되어야 합니다 **. DataControl**및 해당 **DATAFLD** 속성은 **레코드 집합** 개체 필드 (열)로 설정 됩니다.  
  
 이 자습서에서는 **SourceRecordset** 속성을 설정 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [6 단계: 서버에 변경 내용 전송 (RDS 자습서)](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)   
 [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
