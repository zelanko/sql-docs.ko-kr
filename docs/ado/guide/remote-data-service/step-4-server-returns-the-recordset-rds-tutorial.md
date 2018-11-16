---
title: '4 단계: 서버 반환 레코드 집합 (RDS 자습서) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], server returns Recordset
ms.assetid: 3d1855c4-419c-4810-b5ea-6c874b5e2905
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f111fab97b81ed847870f6535399c58bd856ab99
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559660"
---
# <a name="step-4-server-returns-the-recordset-rds-tutorial"></a>4단계: 서버가 레코드 집합을 반환합니다(RDS 자습서).
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 RDS 검색 변환 **레코드 집합** 클라이언트로 다시 보낼 수 있는 폼에 개체 (이므로 *마샬링할* 는 **레코드 집합**). 변환 및 전송 되는 방법의 정확한 형식은 서버 인터넷 또는 인트라넷 local area network, 아니면 인지 여부는 동적 연결 라이브러리에 따라 달라 집니다. 이 정보는 투명 합니다; 그러나 RDS 문제는 모든 전송 합니다 **레코드 집합** 클라이언트로 다시 합니다.  
  
 클라이언트 쪽에는 **레코드 집합** 개체를 반환 하 고 로컬 변수에 할당 합니다.  
  
```vb
Sub RDSTutorial4()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>관련 항목  
 [5 단계: DataControl 유용 수행 (RDS 자습서)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)   
 [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
