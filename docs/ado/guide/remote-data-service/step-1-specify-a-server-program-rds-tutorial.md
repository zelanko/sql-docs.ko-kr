---
title: '1 단계: 서버 프로그램 (RDS 자습서) 지정 | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], specifying server program
ms.assetid: d8bb35b1-c02a-4231-8d55-016e56e53b95
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5583f9b2c5093859e9bb5d3fd0eb9444828cb4bc
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558300"
---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>1단계: 서버 프로그램 지정(RDS 자습서)
가장 일반적인 경우에 사용 된 [rds. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) 개체 [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) 기본 서버 프로그램을 지정 하는 방법 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), 또는 사용자 고유의 사용자 지정 서버 프로그램 (비즈니스 개체). 서버 및 서버 프로그램에 대 한 참조에서 서버 프로그램 인스턴스화될 또는 *프록시*에 반환 됩니다.  
  
 이 자습서에서는 기본 서버 프로그램을 사용합니다.  
  
```vb
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [2 단계: 서버 프로그램 (RDS 자습서) 호출](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)   
 [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
