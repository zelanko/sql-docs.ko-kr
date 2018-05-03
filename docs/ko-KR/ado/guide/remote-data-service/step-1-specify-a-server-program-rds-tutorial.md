---
title: '1 단계: 서버 프로그램 (RDS 자습서) 지정 | Microsoft Docs'
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
- RDS tutorial [ADO], specifying server program
ms.assetid: d8bb35b1-c02a-4231-8d55-016e56e53b95
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2acdd9c143ebedfc8af600e09b4791fca1620350
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>1 단계: 서버 프로그램 (RDS 자습서) 지정
가장 일반적인 경우에 사용 된 [.rds입니다 DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) 개체 [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) 기본 서버 프로그램 지정할 메서드가 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), 또는 사용자 고유의 사용자 지정 서버 프로그램 (비즈니스 개체). 서버 프로그램은에서 서버에 서버 프로그램에 대 한 참조 인스턴스화되며 또는 *프록시*, 반환 됩니다.  
  
 이 자습서에서는 기본 서버 프로그램을 사용합니다.  
  
```  
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "http://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [2 단계: 서버 프로그램 (RDS 자습서) 호출](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)   
 [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
