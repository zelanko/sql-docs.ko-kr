---
title: '4 단계: 서버 반환 레코드 집합 (RDS 자습서) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], server returns Recordset
ms.assetid: 3d1855c4-419c-4810-b5ea-6c874b5e2905
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dec3b614f0401160df1310d80265d4a10798eb08
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35274492"
---
# <a name="step-4-server-returns-the-recordset-rds-tutorial"></a>4 단계: 서버 반환 레코드 집합 (RDS 자습서)
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 RDS 검색 변환 **레코드 집합** 클라이언트로 다시 보낼 수 있는 형식으로 개체 (즉, *마샬링하고* 는 **레코드 집합**). 정확한 형식은 변환과 전송 방법을의 서버는 인터넷 또는 인트라넷, 로컬 영역 네트워크에서 또는 여부는 동적 연결 라이브러리에 따라 다릅니다. 이 정보는 투명 합니다; 그러나 문제는 RDS 인지 모든 보냅니다는 **레코드 집합** 다시 클라이언트에 있습니다.  
  
 클라이언트 쪽에서는 **레코드 집합** 개체를 반환 하 고 지역 변수에 할당 합니다.  
  
```  
Sub RDSTutorial4()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "http://yourServer")  
   Set RS = DF.Query("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>관련 항목  
 [5 단계: DataControl 유용 수행 (RDS 자습서)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)   
 [RDS 자습서(VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
