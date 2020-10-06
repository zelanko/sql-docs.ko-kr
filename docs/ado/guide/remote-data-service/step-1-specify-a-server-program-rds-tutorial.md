---
description: '1단계: 서버 프로그램 지정(RDS 자습서)'
title: '1 단계: 서버 프로그램 지정 (RDS 자습서) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], specifying server program
ms.assetid: d8bb35b1-c02a-4231-8d55-016e56e53b95
author: rothja
ms.author: jroth
ms.openlocfilehash: 2872340341c6b576a11d52a0b867fdbcd04389b4
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91723015"
---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>1단계: 서버 프로그램 지정(RDS 자습서)
가장 일반적인 경우에는 RDS를 사용 합니다 [. 공간](../../reference/rds-api/dataspace-object-rds.md) 개체 [CreateObject](../../reference/rds-api/createobject-method-rds.md) 방법 기본 서버 프로그램, [RDSServer. DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md)또는 사용자 지정 서버 프로그램 (비즈니스 개체)을 지정 합니다. 서버 프로그램은 서버에서 인스턴스화되고 서버 프로그램 또는 *프록시*에 대 한 참조가 반환 됩니다.  
  
 이 자습서에서는 기본 서버 프로그램을 사용 합니다.  
  
```vb
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](/dotnet/framework/wcf/)로 마이그레이션해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [2 단계: 서버 프로그램 호출 (RDS 자습서)](./step-2-invoke-the-server-program-rds-tutorial.md)   
 [RDS 자습서(VBScript)](./rds-tutorial-vbscript.md)